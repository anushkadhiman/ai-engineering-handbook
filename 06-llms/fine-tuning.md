# Fine-tuning an LLM

Fine-tuning an LLM is the process of further training a pre-trained model on a smaller, domain-specific dataset to improve performance on specialized tasks, align with specific formats, or reduce hallucinations. It adapts model weights for better accuracy without requiring the vast, costly data of initial pre-training. Key methods include Supervised Fine-Tuning (SFT) and parameter-efficient techniques like LoRA/QLoRA.

**Key Aspects of Fine-Tuning**

- Purpose: To specialize a general-purpose model for specific industries (legal, medical) or tasks (chatbots, code generation), improving accuracy and lowering operational costs.

- Methods:
  - Full Fine-Tuning: Updates all model parameters, which is computationally expensive.
  - Parameter-Efficient Fine-Tuning (PEFT/LoRA): Freezes most weights and only trains a small, subset of added parameters, reducing memory usage and speeding up training.
  - Instruction Fine-Tuning: Trains the model to better follow user instructions.

- When to Use: Use fine-tuning when prompt engineering is insufficient, you need specialized behavior, or high accuracy in a specific domain is required.

**Fine-Tuning Process**

1. Select Base Model: Select a foundation model based on task needs and available compute.
2. Prepare Dataset: Curate a high-quality, labeled dataset (e.g., prompt-response pairs) for the specific task.
3. Training: Utilize frameworks like PyTorch or Hugging Face Transformers to run training.
4. Evaluation: Use a separate dataset to test the model's performance on the new task.

**Fine-Tuning vs. Alternatives**

- Prompt Engineering: Low cost, no training, uses model's existing knowledge.
- RAG (Retrieval-Augmented Generation): Connects the model to external data for real-time, factual information retrieval.
- Fine-Tuning: Changes model behavior and style, learns new behaviors.

**Benefits**

- Domain Expertise: Enhances understanding of specific terminology.
- Data Control: Allows for self-hosting and privacy, ensuring data does not leave your infrastructure.

---

## Parameter-efficient fine-tuning (PEFT)

Parameter-efficient fine-tuning (PEFT) techniques, such as LoRA and Prefix Tuning, adapt large language models (LLMs) to new tasks by updating only a tiny subset of parameters (often &lt;1%) while freezing the base model. PEFT drastically reduces computational and storage costs, allowing high-performance tuning on consumer hardware.

**Key Aspects of PEFT:**

- Reduced Resource Requirements: By freezing the majority of pre-trained parameters, PEFT saves significant GPU memory and storage, making it possible to fine-tune large models like 12B parameter models on a single 80GB GPU.
- Comparable Performance: Despite training fewer parameters, PEFT methods often deliver performance comparable to, or even matching, full fine-tuning.
- Mitigates Catastrophic Forgetting: Since the original model weights are frozen, the model retains its foundational knowledge while adapting to new tasks.

**Common PEFT Methods:**

- LoRA (Low-Rank Adaptation): Injects trainable, low-rank decomposition matrices into the transformer architecture, reducing the number of trainable parameters.
- Prefix Tuning: Prepends small, trainable virtual tokens to the input, allowing the model to adapt without changing its core parameters.
- Adapter Layers: Inserts small neural network modules between existing layers.
- BitFit: Only tunes the bias parameters of the model.

PEFT is widely used across various tasks, including image classification, stable diffusion customization, and natural language understanding.

---

## LoRA and QLoRA

Parameter-Efficient Fine-Tuning (PEFT) that allow you to adapt massive AI models (like LLMs) to specific tasks using a fraction of the memory and compute power required for traditional training.

**LoRA (Low-Rank Adaptation)**
LoRA works by freezing the original weights of the pre-trained model and adding small, trainable adapter matrices to specific layers (usually attention layers).

- **How it works:** Instead of updating a giant weight matrix, LoRA decomposes the update into two much smaller matrices (e.g., and , where is a small rank like 8 or 16).
- **Key Advantage:** It reduces the number of trainable parameters by up to 10,000 times. Because the original weights are frozen, it also prevents catastrophic forgetting where the model loses its original general knowledge.
- **Inference:** The adapters can be merged back into the main model, meaning there is zero added latency during use.

**QLoRA (Quantized LoRA)**
QLoRA is an advanced version that adds quantization to LoRA to save even more memory, allowing you to fine-tune massive models (like Llama-65B) on a single consumer GPU.

- **How it works:** It compresses the base model's weights into a 4-bit format (specifically NormalFloat4) to drastically reduce storage. The LoRA adapters are then trained in higher precision (16-bit) to correct any errors introduced by this compression.
- **Key Features:** It introduces techniques like Double Quantization (compressing the compression constants themselves) and Paged Optimizers (moving data to CPU RAM when VRAM is full) to push hardware limits.
- **Trade-off:** It is slightly slower than LoRA due to the constant quantization/dequantization steps but requires significantly less VRAM.

---

## Prompt tuning

Prompt tuning is a parameter-efficient adaptation technique where you keep a large pre-trained model entirely frozen and only train a small set of special, continuous vectors called soft prompts.
Unlike traditional hard prompts (actual text you write), soft prompts are high-dimensional vectors that the model learns through training to steer its behavior toward a specific task.

**How It Works**

- **Frozen Backbone:** The billions of weights in the original model remain unchanged, preserving all its general knowledge.
- **Soft Prompt Addition:** A sequence of virtual tokens (soft prompts) is prepended to the input.
- **Gradient-Based Learning:** During training, the model's error (loss) is backpropagated to update only these soft prompt vectors, not the model itself.
- **Task Switching:** At inference, you simply plug in the small set of learned vectors for the task you want (e.g., sentiment analysis vs. summarization) while using the same base model.

**Why Choose Prompt Tuning?**

- **Massive Efficiency:** You only store and update a few thousand parameters (kilobytes) instead of gigabytes for a full model copy.
- **Scalability:** Performance often matches full fine-tuning as models get larger (10B+ parameters).
- **Stability:** Since the base model is frozen, it won't forget its original abilities (catastrophic forgetting) during the tuning process.
  **Low Data Needs:** It can achieve strong results even with relatively small labeled datasets.

---

## Prefix Tuning

Prefix Tuning is a parameter-efficient fine-tuning (PEFT) method that adapts large language models to specific tasks by adding a set of trainable, continuous vectors (called a prefix) to the beginning of the input at every layer of the model.
While it shares the same goal as prompt tuning—steering a frozen model without retraining all its weights—it is more expressive because its influence goes deeper into the model's architecture.

**How It Works**

- **Frozen Backbone:** The original billions of parameters in the pre-trained model remain completely unchanged.
- **Multi-Layer Injection:** Instead of just adding a soft prompt to the input layer, prefix tuning prepends learned vectors to the Key (K) and Value (V) matrices in the self-attention mechanism of every transformer layer.
- **Virtual Tokens:** The model treats these learned vectors as virtual tokens. When the model processes your text, it attends to these virtual tokens as if they were part of the input, allowing them to guide the generation process.
- **Bottleneck MLP:** To make training more stable, the prefix is often generated through a small Multi-Layer Perceptron (MLP) that is discarded after training, leaving only the optimized prefix vectors.

**Why Use It?**

- **Performance:** Achieves results comparable to full fine-tuning while updating less than 1% of the model's total parameters.
- **Modularity:** You can store different tiny prefixes for different tasks (e.g., one for translation, one for summarization) and simply swap them out while using the same base model.
- **Efficiency:** Drastically reduces the computational and storage costs of maintaining multiple task-specific models.

---

s
