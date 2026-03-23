# LLM Inference Optimization Techniques

LLM inference optimization techniques are generally categorized into model-level, algorithmic, and system-level strategies to overcome the two primary bottlenecks: compute-bound prefill (processing the prompt) and memory-bound decoding (generating tokens one-by-one).

**1. Model-Level Optimizations (Compression)**
These techniques reduce the size of the model to fit into smaller GPU memory and accelerate computation.

- **Quantization:** Reduces numerical precision (e.g., from FP16 to INT8, INT4, or FP8). It typically yields 2x–4x memory reduction and significant speedups with minimal accuracy loss.
- **Knowledge Distillation:** Training a smaller "student" model to mimic a larger "teacher" model. A distilled model can be 700x smaller while retaining high performance.
- **Pruning:** Removing redundant weights or entire layers. Structured pruning removes hardware-friendly blocks (e.g., 2:4 sparsity) to skip zero-value calculations.
- **Low-Rank Adaptation (LoRA):** Using lightweight adapters for specific tasks rather than full model weights, enabling efficient [Multi-LoRA serving].

**2. Algorithmic Optimizations (Attention & Decoding)**
These methods optimize the mathematical operations within the Transformer architecture.

- **FlashAttention**: An "exact" attention algorithm that tiles the computation to fit into fast on-chip SRAM, reducing slow memory (VRAM) reads/writes by 10–20x.
- **Attention Variants:** Grouped-Query Attention (GQA) and Multi-Query Attention (MQA) reduce the KV cache size by sharing Key/Value heads across multiple Query heads.
- **Speculative Decoding:** A small "draft" model predicts multiple future tokens, which the large model verifies in a single parallel step, often speeding up generation by 2x–3x.
- **FlashInfer:** Uses JIT-compiled kernels and block-sparse formats to reduce long-context latency by up to 30%.
  **3. System & Serving Optimizations**
  These strategies manage how requests are scheduled and how memory is allocated.
- **PagedAttention:** Allocates KV cache in fixed-size "pages" (like OS virtual memory) to eliminate fragmentation and waste, enabling much larger batch sizes.
- **Continuous (In-flight) Batching:** Dynamically replaces finished requests in a batch with new ones immediately, keeping the GPU near 100% utilization.
- **Prefix (Prompt) Caching:** Stores the KV cache for common prompt prefixes (e.g., system instructions) so they never need to be recomputed for new requests.
- **Prefill-Decode Disaggregation:** Separates the compute-heavy prompt processing (prefill) onto different GPUs from the memory-heavy generation (decode) to scale each independently.
  **4. Parallelism Strategies**
  For models too large for a single GPU, workloads are split across devices.
- **Tensor Parallelism:** Splits individual layers (sharding weights) across GPUs.
- **Pipeline Parallelism:** Splits the model vertically by layers; different GPUs handle different stages of the model.
- **Expert Parallelism:** In Mixture-of-Experts (MoE) models, only specific "expert" sub-networks are activated per token, improving efficiency.

---

## KV Cache (Key-Value Cache)

KV Cache (Key-Value Cache) is an optimization technique used in Transformer-based Large Language Models (LLMs) to accelerate the text generation process. During inference, it stores the intermediate Key and Value vectors of previously processed tokens so they do not need to be recomputed for every new token generated.

**Why do we use it?**

- **Speed:** It can make inference 5–10x faster by avoiding redundant calculations.
- **Efficiency:** It reduces the computational complexity of generating a new token from quadratic to linear relative to the sequence length.
- **Real-time Interaction:** It enables smooth, human-like response times in long, multi-turn conversations.

**How it works mathematically**
In a standard Attention mechanism, for a sequence of length :
Query (Q), Key (K), and Value (V) matrices are computed for all tokens.
Attention Scores are calculated.
With KV Caching at step t+1 :
Query (Q): Only computed for the single new token .
Key (K): The model retrieves from the cache and concatenates the new .
Value (V): Similarly, it retrieves and appends .
Calculation: The model only performs one row of the attention matrix multiplication (the new Query against all cached Keys) instead of recalculating the entire matrix.

**Pros**

- Massive speed-up in text generation (latency reduction).
- Makes long-context generation feasible.
- Eliminates redundant operations.

**Cons**

- Adds complexity to the model's implementation and code.
- Requires significant VRAM; the cache can grow larger than the model itself.
- Becomes a memory bandwidth bottleneck as the GPU must constantly load the growing cache.

---

**PagedAttention**
PagedAttention is a memory management algorithm designed to solve the biggest problem with KV caches: memory fragmentation and waste. It was introduced by the team behind vLLM and is inspired by how operating systems handle virtual memory.

**The Problem**
Before PagedAttention, LLM serving frameworks allocated a static, contiguous block of GPU memory for the KV cache of every request. This led to three major inefficiencies: - **Internal Fragmentation:** We had to pre-allocate space for the maximum possible sequence length (e.g., 2048 tokens), even if the model only generated 50 tokens. - **External Fragmentation:** Memory gaps between different requests couldn't be used effectively. - **Reservation Waste:** Even if we knew a request wouldn't reach the max length, the system "reserved" that memory just in case.

In practice, standard systems wasted 60% to 80% of available GPU memory.

**How PagedAttention Works?**
PagedAttention treats the GPU memory like a book with pages rather than a single long scroll.

- **Logical Partitioning:** The KV cache of a single request is divided into fixed-size blocks (e.g., each block holds the data for 16 tokens).
- **Physical Mapping:** These blocks do not need to be stored next to each other in the GPU memory. A "Block Table" (similar to an OS Page Table) maps the logical sequence of tokens to physical locations in memory.
- **Dynamic Allocation:** As the model generates new tokens, the system grabs a new block from a "free pool" only when the current block is full.

**Why do we use?**

- **Near-Zero Waste:** Memory waste is reduced to less than 4% (only the very last block of a sequence might be partially empty).
- **Higher Throughput:** Because you aren't wasting memory, you can pack 2x to 4x more requests onto the same GPU simultaneously.
- **Efficient Sharing:** For complex tasks like Parallel Sampling (generating five different endings to one prompt) or Beam Search, PagedAttention allows multiple requests to "point" to the same physical memory blocks for the initial prompt, saving massive amounts of space.

It is worth noting that while PagedAttention fixes where we store data (memory management), FlashAttention fixes how we compute attention (speed/IO efficiency). Most modern LLM engines use both together to achieve maximum performance.

---

## Multi-Query Attention

Multi-Query Attention (MQA) is a variant of the attention mechanism designed specifically to reduce the memory footprint and bandwidth bottlenecks of the KV cache.
While PagedAttention manages how memory is allocated, MQA changes the architecture of the model to ensure there is less data to store in the first place.

**The Concept: One Key, Many Queries**
In standard Multi-Head Attention (MHA), if you have 8 attention heads, you have 8 sets of Queries, 8 sets of Keys, and 8 sets of Values.

- MHA: Each Query head has its own dedicated Key and Value head.
- In Multi-Query Attention, you keep multiple Query heads, but all of them share a single Key and a single Value head.
- MQA: All Query heads look at the same Key and Value.

**Why do we use it?**
The primary bottleneck in LLM inference isn't usually "compute" (math operations); it is Memory Bandwidth (the speed at which data moves from VRAM to the GPU cores).

- **KV Cache Shrinkage:** Since we only store one Key and one Value per layer (instead of heads), the KV cache size is reduced by a factor equal to the number of heads (e.g., a 16x or 32x reduction).
- **Faster Loading:** During generation, the GPU only needs to load one KV pair from memory to satisfy all query heads. This significantly speeds up the "decoding" phase.
- **Increased Throughput:** Smaller KV caches mean you can fit significantly more concurrent users/sequences on a single GPU.

**The Trade-off: Accuracy vs. Speed**
There is no "free lunch" in AI. By forcing all heads to share the same Keys and Values:

- **Cons:** The model loses some "expressive power." In MHA, different heads can focus on different relationships (e.g., one head for grammar, one for logic). In MQA, they are all forced to look at the same compressed representation of the context.
- **Result:** Small drop in accuracy/perplexity, but massive gains in speed.

---

## Grouped-Query Attention

Grouped-Query Attention (GQA) is the modern standard for attention in large-scale LLMs (like Llama 3, Mistral, and Gemma). It acts as a middle ground that balances the high quality of Multi-Head Attention (MHA) with the extreme speed of Multi-Query Attention (MQA).

**The Balanced Architecture**
GQA divides the many Query heads into a smaller number of Groups. Each group of Query heads shares a single Key and Value head.
**MHA (Multi-Head):** 1 Query : 1 Key : 1 Value (e.g., 32 Q, 32 K, 32 V) — High quality, heavy cache.
**MQA (Multi-Query):** Many Queries : 1 Key : 1 Value (e.g., 32 Q, 1 K, 1 V) — Fastest, but lower quality.
**GQA (Grouped-Query)**: Many Queries : Shared Key/Value per Group (e.g., 32 Q divided into 8 groups, each group sharing 1 K and 1 V).

**Key Benefits**
**Memory Bandwidth Efficiency:** LLM inference is often "memory-bound," meaning the bottleneck is moving data from VRAM to GPU cores. GQA reduces the amount of KV data to be loaded by up to 80–90% compared to MHA, significantly speeding up token generation.
**Near-MHA Quality:** Because the model still has multiple distinct Key/Value heads (just fewer than the Query heads), it retains most of the "expressive power" of MHA, avoiding the significant accuracy drops seen in MQA.
**Higher Throughput:** By drastically shrinking the KV Cache size, GQA allows for much larger batch sizes and longer context windows (e.g., 128k tokens) on the same hardware.

**Mathematical Intuition**

- In GQA, if you have Query heads and groups, each group has heads. For a given group :
- The Queries are distinct.
- They all perform attention against the same and for that group.
- This effectively averages out the "lookup" information for that group, which empirical studies show is often redundant across all heads anyway.

---

## Multi-Head Latent Attention

Multi-Head Latent Attention (MLA) is a specialized attention mechanism introduced by DeepSeek (first in DeepSeek-V2) to solve the "memory wall" of the KV cache.
While GQA (Grouped-Query Attention) reduces cache size by sharing heads, MLA uses low-rank compression to shrink the entire KV space into a small "latent" vector, achieving even greater memory savings without sacrificing model quality.

**The Core Innovation: Low-Rank Compression**
In standard attention, every token’s Key (K) and Value (V) are stored as large vectors. In MLA, these are compressed into a single, much smaller latent vector .

- **Compression:** A "down-projection" matrix turns the high-dimensional hidden state into a small latent vector .
- **Decompression:** During the attention calculation, this latent vector is "up-projected" back into the full Key and Value heads only when needed.
- **Result:** You only cache the compressed latent vector, which is often 90%+ smaller than a standard KV cache.

**Mathematical Intuition & The "Absorption Trick"**

- MLA doesn't just store less; it computes smarter using matrix absorption.
- Standard Logic: MLA Logic: Since is derived from the latent vector , the math becomes:
- The Trick: During inference, (the up-projection matrix) can be absorbed directly into the Query matrix .
- This means the model can compute the attention score directly against the compressed latent cache without ever explicitly reconstructing the full keys in memory.

**Decoupled RoPE (Rotary Positional Embeddings)**
Position embeddings like RoPE are usually applied to Keys and Queries. However, RoPE is sensitive to position and breaks the "absorption trick" mentioned above.
To fix this, MLA decouples the attention into two parts:

- **Content Part:** Uses the compressed latent vectors (no RoPE) and supports matrix absorption for maximum speed.
- **Position Part:** A small, separate set of vectors carries the RoPE information. These are concatenated to the content vectors just before the dot product.
  **Pros**
- Memory: Reduces KV cache size by ~93% compared to MHA.
- Quality: Maintains or surpasses MHA quality; GQA usually loses some accuracy.
- Throughput: Massively increases generation speed by overcoming memory bandwidth limits.
  **Cons**
- Higher computational (FLOP) cost during the "prefill" phase.
- Extremely complex to implement and optimize (requires custom kernels like FlashMLA).
- Incompatible with standard RoPE; requires the "decoupled" architecture.

---

## Continuous Batching

Continuous Batching (also known as Iteration-level Batching) is an inference scheduling technique that dynamically manages multiple requests at each token generation step.
While other optimizations like KV Caching or MQA reduce the amount of data processed per token, Continuous Batching ensures the GPU never sits idle by maximizing the number of tokens being generated in every cycle.

**Why do we use it?**

- **Eliminates "Stragglers":** In static batching, if one request in a batch takes 500 tokens togenerate and another takes 10, the finished request stays "locked" in the GPU, wastingresources until the longest request is done.
- **Reduces Padding:** Static batching requires padding all sequences to the length of the longestone in the batch. Continuous batching processes only the actual tokens needed for each request.
- **Massive Throughput:** It can increase the number of tokens processed per second by 10x to 23xcompared to naive batching.

**How it works**
The core innovation, first introduced by the Orca paper (OSDI '22), is changing the scheduling unit from a whole request to a single iteration.

- **Request Queue:** Incoming requests wait in a queue.
- **Iteration Step:** At every single generation cycle, the scheduler checks if any request has finished (e.g., generated an <EOS> token).
- **Dynamic Swapping:** If a request finishes, it is immediately removed from the batch. The scheduler then pulls a new request from the queue to fill that specific "slot".
- **Token Generation:** The GPU performs one forward pass for the current "mixed" batch, where one request might be on its 5th token while another is on its 200th.
  **Pros**
- Utilization Keeps the GPU active at near-100% capacity.
- Latency Dramatically reduces "Time to First Token" (TTFT) for new users.
- Efficiency Works seamlessly with vLLM's PagedAttention for optimal memory use.
  **Cons**
- Requires a complex scheduler to manage the "prefill" vs "decode" states.
- Can cause jitter in token delivery speed for active users as new requests join.
- Extremely memory-intensive; requires robust VRAM management.

---

## Speculative Batching

Speculative Batching (or Batch Speculative Decoding) is a high-performance inference technique that combines Speculative Decoding with Batching to maximize GPU utilization.
While standard speculative decoding speeds up a single request by guessing future tokens, speculative batching allows a system to speed up multiple concurrent requests at once by verifying all their guesses in a single parallel step.

**Intuition**
The "Slow Expert" (Target Model): A massive LLM that is very smart but takes a long time to "think" for every single word.
The "Fast Assistants" (Draft Models): Smaller, faster models that can quickly guess the next 5–10 words.

**Why do we use it?**

- **Overcoming Memory Bottlenecks:** LLM inference is usually limited by how fast weights can be loaded from memory (VRAM), not by the GPU's raw math power. Since verifying 5 tokens takes nearly the same time as generating 1, we use the "idle" math power to check multiple guesses for multiple users simultaneously.
- **Maximum Throughput:** It aims to provide the low latency of speculative decoding while maintaining the high efficiency of batching.

**How it works?**
The process follows a "Propose-Verify-Correct" loop across the entire batch:

- **Drafting:** For every request in the batch, a small draft model (or a fast heuristic) generates candidate tokens.
- **Parallel Verification:** The large target model takes all tokens from all requests and runs a single forward pass.
- **Acceptance:** For each request, the target model accepts the longest prefix of tokens that match its own internal logic.
- **Correction:** If a guess is wrong, the target model provides the correct token at the first point of failure, and the draft model starts again from that new point.

**Pros**

- Speed Can achieve 2x–3x speedup in token generation.
- Efficiency Squeezes every bit of performance out of idle GPU cores.
- Quality Lossless: The output is identical to what the large model would have produced alone.

**Cons**

- Diminishing Returns: As the batch size grows, the GPU becomes "compute-bound," and the benefits of speculation shrink.
- The "Ragged Tensor" Problem: Requests accept different numbers of tokens, making it hard to keep the batch perfectly aligned in memory.
- Overhead: Managing two models (draft and target) and synchronizing their KV caches adds significant architectural complexity.

---

## Prefix Caching

Prefix Caching (also known as Prompt Caching) is an optimization that allows different inference requests to reuse the same KV cache if they share an identical starting sequence of tokens.
While standard KV caching works within a single request to speed up decoding, prefix caching works across different requests to skip the expensive prefill phase for recurring instructions or context.

**Why do we use it?**

- **System Prompts:** Large, static instructions (e.g., "You are a helpful assistant...") are processed once and never again.
- **Multi-Turn Chat:** In a long conversation, only the newest message needs to be processed; the entire prior chat history is pulled from the cache.
- **Few-Shot Examples:** If you provide 10 examples of a task in your prompt, those examples are cached for all future similar queries.
- **RAG (Retrieval-Augmented Generation):** When querying the same long document multiple times with different questions, the document's KV state is reused.

**How it works**
Modern frameworks like vLLM use a Radix Tree or a Hash-based system to identify shared prefixes:

- **Hashing:** Every block of tokens (often in 16-token chunks) is hashed based on its content and the hash of all tokens preceding it.
- **Lookup:** When a new request arrives, the engine checks its hash table to find the longest matching prefix already in memory.
- **Reuse:** The engine "points" the new request to the existing physical memory blocks. It avoids the prefill math for those tokens entirely.

**Pros**

- Performance Up to 85% reduction in Time to First Token (TTFT).
- Cost Some providers (like Anthropic) offer 90% lower costs for cached tokens.
- Throughput Significantly increases total system capacity by reducing redundant math.

**Cons**

- Only works for exact matches. A single extra space or typo breaks the cache.
- Requires large amounts of VRAM to store long-term context.
- Security Risk: Can create "timing side-channels" where an attacker can guess if a prefix was previously used based on response speed.

---

## vllm

vLLM (Virtual Large Language Model) is an open-source, high-throughput inference and serving engine for LLMs. Developed by researchers at UC Berkeley, it is designed to run models with significantly higher efficiency and lower costs by solving the "memory wall" of KV caching.

**Key Innovations**

- **PagedAttention:** Its flagship feature, inspired by operating system virtual memory, which divides the KV cache into non-contiguous "pages". This reduces memory waste from ~60-80% down to less than 4%, allowing for much larger batch sizes.
- **Continuous Batching:** Instead of processing static groups of requests, vLLM dynamically adds new requests and removes completed ones at each iteration, keeping the GPU utilization near 100%.
- **Automatic Prefix Caching:** It automatically detects shared prompt prefixes across different requests and reuses their KV caches to skip redundant computation.

**Performance & Scale**

- **Throughput:** Achieves up to 24x higher throughput than standard Hugging Face Transformers and 3.5x higher than Text Generation Inference (TGI).
- **Distributed Inference:** Supports massive models across multiple GPUs using Tensor Parallelism and Pipeline Parallelism.
- **Broad Support:** Compatible with nearly all popular open-source architectures (Llama, Mistral, Mixtral, DeepSeek) and various hardware including NVIDIA/AMD GPUs, TPUs, and Intel/AWS accelerators.

**Developer Features**

- OpenAI-Compatible API: Provides a drop-in REST server that matches the OpenAI API schema, making it easy to integrate with existing tools like LangChain.
- Quantization: Supports various compression formats (GPTQ, AWQ, FP8, INT8) to fit larger models into less VRAM.
- Flexibility: Includes features for Multi-LoRA serving, speculative decoding, and streaming outputs.

---

## Knowledge Distillation

Knowledge Distillation is a machine learning technique where a small, compact model (the Student) is trained to reproduce the behavior and performance of a large, complex, pre-trained model (the Teacher).

**How It Works**

- In standard training, a model is told: "This image is a Cat (100%), not a Dog (0%)." This is called a Hard Target.
- In Distillation, the Student looks at the Teacher’s Soft Targets. The Teacher might say: "I am 90% sure this is a Cat, but it has a 9% chance of being a Dog because it has floppy ears, and 1% chance of being a Car."
- The "Dark Knowledge": That 9% "Dog" probability is the "Dark Knowledge." It tells the Student that a Cat looks more like a Dog than it looks like a Car.
- The Benefit: This extra information helps the Student learn the underlying structure of the data much faster and with fewer "neurons" (parameters).

**The Three Components**

- **The Teacher:** A large, high-performing model (like BERT-Large) that is already fully trained.
- **The Student:** A smaller architecture (like DistilBERT) with fewer layers or smaller hidden dimensions.
- **The Distillation Loss:** A mathematical formula that measures how much the Student’s guesses differ from the Teacher’s "soft" guesses. The Student tries to minimize this difference.

**Temperature (T)**
In Knowledge Distillation, Temperature (T) is a mathematical "smoothing" tool, and Soft Targets are the blurred, information-rich results that come from it.

**What are Soft Targets?**
In a standard AI model, the final layer (called Softmax) tries to be as confident as possible. It might output:
Cat: 0.999
Dog: 0.001
Car: 0.000001
This is a Hard Target. It’s very "peaky" and hides the relationship between categories.

A Soft Target "flattens" those numbers. It looks like this:
Cat: 0.70
Dog: 0.25
Car: 0.05

By looking at these Soft Targets, the Student model learns that a cat is kind of like a dog (both have fur/ears) but nothing like a car. This "hidden" similarity is the Dark Knowledge that makes the Student smarter.

**What is Temperature (T)?**
Temperature is the "knob" you turn to create those Soft Targets. It’s a value added to the Softmax formula:

- Standard: The model is very confident. It picks one winner and ignores the rest.
- Higher Temperature: This "softens" the probability distribution. The higher the T, the more the "losing" categories (like "Dog") get a share of the probability.
- Lower Temperature: This makes the model even more confident and "sharp," which isn't helpful for distillation.

**Why use Temperature?**

- If the Student only sees the "Hard" 0.999 Cat result, it learns to be a copycat but doesn't understand why the Teacher made that choice. By raising the Temperature, we force the Teacher to reveal its internal uncertainty. This uncertainty is exactly what the Student needs to learn the nuances of language or images with fewer parameters.
- In Knowledge Distillation, we divide every logit by the Temperature (T) before applying the exponential.
- How the value of T changes the result:
  - When T=1 : The formula is identical to the standard Softmax.
  - When T>1 (e.g., T=5): The differences between the scores are "shrunk."
  - Using our example (z (cat) = 10, z (dog)=5):
  - Instead of 10 and 5, the math now uses 2 and 1.
  - is only about 2.7 times larger than .

- The Result: The "Dog" class now has a much higher probability (a Soft Target), allowing the Student to see that the Teacher thought it was "almost a dog."

**The Training Loop**
When training a model like DistilBERT, the "Loss Function" actually looks at two things at once:

- Distillation Loss: The difference between the Student's soft output and the Teacher's soft output (both using the same T).
- Student Loss: The difference between the Student's hard output and the actual "correct" label (using T=1).
  By balancing these two, the Student learns both the facts (it is a cat) and the logic (it looks a bit like a dog).

## llama.cpp and Ollama

While vLLM is built for high-scale enterprise serving, llama.cpp and Ollama are the kings of the "Local LLM" world, designed to run models on your own laptop or desktop.

**llama.cpp:**
llama.cpp is a low-level, high-performance inference engine written in pure C/C++. It is the "brain" that many other local AI tools use under the hood.

- **Maximum Portability:** It is designed to run on almost anything—your CPU, Apple M-series chips, or standard NVIDIA/AMD GPUs—without needing massive data-center setups.
- **GGUF Format:** It pioneered the GGUF file format, which allows large models to be compressed (quantized) so they fit into consumer RAM.
- **The "Bare Metal" Experience:** It is a command-line tool. You have total control over threads, GPU layers, and memory mapping, but it has a steep learning curve.
- **Performance:** Often faster than wrappers for single-user tasks because it has zero overhead.
  **Ollama:**
  If llama.cpp is the engine, Ollama is the sleek, user-friendly car built around it. It is a high-level manager that makes running AI as easy as installing an app.
- **One-Click Simplicity:** It provides a simple installer for macOS, Linux, and Windows. You don't need to know what a "tensor" is to use it.
- **Model Library:** Instead of hunting for files on Hugging Face, you just type ollama run llama3, and it automatically downloads and starts the model for you.
- **API by Default:** It automatically sets up a local server that other apps (like Open WebUI or VS Code plugins) can talk to immediately.
- **Customization:** You can create "Modelfiles" to give your AI specific personalities or system prompts in just a few lines of text.

---

### Cpu Offloading

Cpu Offloading is a memory management trick that moves model data (weights, gradients, or optimizer states) from the GPU VRAM to the System RAM (CPU) when they aren't actively being used.
Think of it as using your computer's RAM as an "overflow parking lot" for your graphics card.

**How it Works**
Modern AI models are often too large to fit entirely on a single GPU. CPU offloading manages this by:

- **Storage:** Keeping the bulk of the model in the much larger (but slower) system memory.
- **Swapping:** Moving only the specific layer or data needed for the current calculation onto the GPU.
- **Execution:** Performing the heavy math on the GPU, then moving the results back to the CPU to make room for the next piece.

**When to Use It**

- **Massive Models:** It is the primary way to run 70B+ parameter models on consumer GPUs that only have 8GB or 12GB of VRAM.
- **Training (Optimizer Offloading):** In tools like DeepSpeed, optimizer states (which take up 2-3x more space than the model itself) are offloaded to the CPU to free up GPU space for larger batch sizes or longer sequences.
- **Inference:** Using Hugging Face Accelerate, you can load a model that exceeds your VRAM by "mapping" parts of it to the CPU and even the hard drive (disk offloading).

**The Catch: The "Bottleneck"**
The main downside is speed. Moving data between the GPU and CPU over the PCIe bus is much slower than keeping everything in VRAM. While it prevents "Out of Memory" errors, it can make training or generation significantly slower.

**Popular Implementations**

- **ZeRO-Offload (DeepSpeed):** Specifically designed to offload both optimizer states and gradients to the CPU.
- **FSDP (Fully Sharded Data Parallel):** A PyTorch technique that supports offloading parameters to the CPU when not in use during the forward/backward pass.
- **Llama.cpp:** Uses CPU offloading to allow users to run LLMs using a mix of GPU and System RAM, making local AI accessible on standard PCs.
