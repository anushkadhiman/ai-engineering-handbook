# **Transformer model**

The Transformer model is a neural network architecture for sequential data that uses self-attention mechanisms to process entire sequences in parallel, rather than sequentially like RNNs. Key components include encoder-decoder stacks, multi-head attention, positional encoding, and feed-forward networks, enabling superior context understanding and faster training for tasks like translation and generation.

**Core Structural Blocks**
The original architecture is a "sequence-to-sequence" model consisting of two primary stacks:

- **Encoder Stack:** Processes the input sequence (e.g., an English sentence) into a "context vector"—a high-dimensional, compressed representation that captures the meaning and relationships of all tokens.
- **Decoder Stack:** Takes the encoder's output and, one token at a time, generates the output sequence (e.g., a French translation), using previous outputs to inform the next prediction.

**Key Internal Components**
Within each encoder and decoder layer, several sub-layers perform specific mathematical transformations:

- Self-Attention Mechanism: The most critical feature, allowing the model to weigh the importance of every word in a sequence relative to every other word. It uses three vectors—Query (Q), Key (K), and Value (V)—to determine context dynamically.
- Multi-Head Attention: Runs several self-attention operations in parallel, allowing the model to capture different types of relationships simultaneously (e.g., grammar in one head and semantic meaning in another).
- Positional Encoding: Since Transformers process all words at once, they lack an inherent sense of word order. Positional encodings (often using sine and cosine functions) are added to the input embeddings to inject information about each token's position.
- Feed-Forward Networks (FFN): Each attention output is passed through a position-wise fully connected network, adding non-linear transformation power to refine the representations of each token independently.
- Layer Normalization & Residual Connections: These "shortcut" connections add the original input of a layer back to its output, helping to stabilize training, speed up convergence, and prevent vanishing gradient problems in deep models.
- Masked Self-Attention: Specifically used in the decoder to ensure the model only looks at previous tokens when predicting the next one, preventing it from "cheating" by seeing future tokens during training.

---

## **Attention mechanisms in Transformer models**

It enable neural networks to dynamically focus on relevant parts of an input sequence, assigning weighted importance to different words to capture context regardless of distance. By computing Query, Key, and Value vectors for each word, the model calculates attention scores via dot products to determine how much focus each token receives.

**Core Concepts and Components**

- **Self-Attention:** The mechanism enables a token to interact with all other tokens in a sequence, allowing it to gather contextual information from far-away words.
- **Q, K, V Vectors:** For each word, three vectors—Query (what I am looking for), Key (what I offer), and Value (what I actually contain)—are learned during training.
- **Attention Scores & Scaling:** The model computes the similarity between a Query and all Keys via dot product, then scales these scores to avoid large gradients.
- **Softmax:** The scores are passed through a softmax function to produce normalized probabilities (attention weights) that sum to 1.
- **Weighted Sum:** These weights are multiplied by the Value vectors to generate the final representation, highlighting crucial information.
- **Key Advantages**
  - **Long-Range Dependencies:** Unlike RNNs, Transformers can connect distant tokens directly, improving comprehension of context.
  - **Parallelization:** Because the model doesn't process tokens sequentially, it can process the entire input at once, speeding up training on GPUs.
  - **Contextual Understanding:** The mechanism allows words to have different meanings based on surrounding words, addressing polysemy (e.g., "bank" in "river bank" vs. "bank deposit").

---

## **Positional encodings**

- It is fundamental component of Transformer-based Large Language Models (LLMs) that inject information about the order of tokens into the model. Because the self-attention mechanism processes tokens in parallel, it lacks an intrinsic notion of sequence order; without positional encodings, "dog bites man" and "man bites dog" would appear identical to the model.
- It assigns a unique representation to each position in a sequence, allowing the model to distinguish between tokens based on their location, such as attending to the i-th token.

**Why Positional Encoding is Essential**

**1. Order Awareness:** Transformers are permutation-invariant; positional encodings provide necessary structural information to understand syntax and sequence.
**2. Handling Long Sequences:** They allow the model to understand the distance between tokens, crucial for interpreting long-range dependencies in texts.
**3. Overcoming Parallel Processing Limits:** They bridge the gap between parallel token processing and sequential language understanding.

**Key Types of Positional Encoding Methods**

**1. Absolute Positional Encoding (APE):** Each position is assigned a specific, fixed, or learned vector that is added to the token embedding.
**2. Sinusoidal (Original Transformer):** Uses fixed sine/cosine functions of different frequencies to generate unique vectors, allowing for potential extrapolation to unseen lengths.
**3. Learned:** Treats positions as trainable parameters, which performs well on training lengths but struggles to extrapolate to longer sequences.
**4. Relative Positional Encoding (RPE):** Instead of encoding the absolute position, these methods encode the relative distance between pairs of tokens.
**5. Bias-Based (e.g., T5):** Adds a learnable bias term to the attention scores based on the distance between keys and queries.
**6. ALiBi (Attention with Linear Biases):** Adds a static penalty to attention scores that is proportional to the distance between tokens, enabling robust generalization to unseen lengths.
**7. Rotary Position Embedding (RoPE):** The current standard for modern LLMs (e.g., LLaMA, PaLM, GPT-NeoX), RoPE encodes absolute positions by applying a rotational transformation to the Query and Key vectors in the self-attention mechanism. Advantages: Naturally models relative distances, is computationally efficient, and enables strong extrapolation, allowing models to handle sequences much longer than their training length.
**8. Context Extension:** Techniques like RoPE scaling (e.g., YaRN, NTK-aware interpolation) are used to stretch the effective context window of models.
**9. NoPE (No Positional Encoding):** Some research suggests that modern decoder-only LLMs might implicitly learn order from causal masking, allowing them to function without explicit positional encodings, though this is still a developing area.
**10. Contextual Position Encoding (CoPE):** Emerging methods that allow positions to be conditioned on context (e.g., counting only nouns or specific words rather than just token positions).

---

## BERT (Bidirectional Encoder Representations from Transformers)

BERT (Bidirectional Encoder Representations from Transformers) is a groundbreaking machine learning framework for natural language processing developed by Google in 2018. It fundamentally changed how AI understands human language by shifting from sequential processing to a simultaneous, bidirectional approach.

**Key Characteristics**

- **Bidirectional Context:** Unlike earlier models that read text strictly left-to-right or right-to-left, BERT considers the entire context of a word by looking at the words both before and after it.
- **Transformer Architecture:** It utilizes the encoder portion of the Transformer model, which allows it to process words in relation to all other words in a sentence.
- **Pre-training & Fine-tuning:** BERT is first pre-trained on massive unlabeled datasets like Wikipedia and then "fine-tuned" for specific tasks such as sentiment analysis or question answering.

**How It Was Trained**
BERT's training involves two primary unsupervised tasks:

- **Masked Language Modeling (MLM):** The model hides (masks) 15% of the words in a sentence and tries to predict them based on the context provided by the surrounding words.
- **Next Sentence Prediction (NSP):** The model learns to identify if two sentences follow each other logically, helping it understand the relationship between different parts of a text.

**Common Applications**

- **Google Search:** BERT powers Google Search to better understand the intent behind complex queries.
- **Sentiment Analysis:** It can determine if a review is positive or negative by understanding the nuances of language.
- **Question Answering:** BERT is used to build systems that find specific answers within large bodies of text.

---

## Next Sentence Prediction (NSP)

Next Sentence Prediction (NSP) is a core part of BERT's training that **helps the model understand the logical flow between sentences**, rather than just individual words.

**How It Works**
During pre-training, BERT is shown pairs of sentences (Sentence A and Sentence B) and must predict if Sentence B actually followed Sentence A in the original text.

- **IsNextSentence (50% of the time):** The model sees two consecutive sentences from the dataset (e.g., "The sun was setting." → "The sky turned orange.").
- **NotNextSentence (50% of the time):** The model sees Sentence A followed by a randomly chosen sentence from a different part of the document (e.g., "The sun was setting." → "The engine started loudly.").

**Why It’s Important**
NSP teaches the model to recognize "discourse" and coherence, which is critical for complex tasks like:

- **Question Answering (QA):** Identifying if a specific passage in a document contains the answer to a user's question.
- **Natural Language Inference (NLI):** Determining if one statement logically entails or contradicts another.
- **Summarisation:** Ensuring that a generated summary maintains the original's logical sequence.

**The Mechanism**
To perform this task, BERT uses a special [CLS] token (Classification token) at the start of every input. The model processes the whole pair, and the final output of this [CLS] token is used to make the "Yes/No" binary prediction.

---

## RoBERTa and ALBERT

RoBERTa and ALBERT significantly refined BERT's approach after researchers discovered that the original Next Sentence Prediction (NSP) task was surprisingly easy for the AI to "cheat" on.

**1. RoBERTa: Removing NSP Entirely**
RoBERTa (Robustly Optimized BERT approach) was created by researchers at Meta who found that removing the NSP task actually improved performance on most downstream benchmarks.

**The Problem with BERT's NSP:** In the original BERT, negative examples were sentences pulled from completely different documents. This made the task a "topic prediction" test rather than a "coherence" test. The model could guess correctly just by noticing the sentences were about different subjects (e.g., sports vs. cooking) without actually understanding how sentences link together.

**The RoBERTa Solution:** It focuses solely on Masked Language Modeling (MLM) but uses Dynamic Masking, where the masked words change every time the model sees a sentence during training.

**2. ALBERT: Harder "Sentence Order Prediction" (SOP)**
Google’s ALBERT (A Lite BERT) argued that while BERT's version of NSP was too easy, the concept of inter-sentence coherence was still valuable. It replaced NSP with Sentence Order Prediction (SOP).

**The SOP "Swap" Trick:** Instead of using a random sentence from another document, ALBERT takes two consecutive sentences from the same document and simply swaps their order for negative examples.

**The Result:** Because both sentences are about the same topic, the model can no longer "cheat" by looking at the subject matter. It is forced to learn much finer-grained logical cues to determine which sentence should naturally come first.

---

## Segment Embeddings

Segment Embeddings are a specific layer of data added to BERT’s input to help the model distinguish between two different sentences in a single input.
Since BERT is often fed pairs of sentences at once (like in the Next Sentence Prediction task), it needs more than just a [SEP] divider to keep track of which word belongs to which thought.

**How They Work**

When you feed a pair of sentences into BERT, the model assigns a binary "segment" value to every single token:
Sentence A: Every word in the first sentence is assigned a Segment 0 embedding.
Sentence B: Every word in the second sentence is assigned a Segment 1 embedding.
These embeddings are represented as numerical vectors that are mathematically added to the word embeddings before the data enters the Transformer layers.

**Why They Are Necessary**

- **Sentence Identity:** Without them, the model might struggle to realize that a pronoun in Sentence B (like "it") should be linked back to a noun in Sentence A.
- **Structural Clarity:** While the [SEP] token acts like a visual "fence" between sentences, Segment Embeddings act like "team jerseys," tagging every word so the model knows exactly which sentence "team" it belongs to throughout the entire deep-learning process.
- **Task Performance:** For tasks like Question Answering, Segment Embeddings are vital because they help the model differentiate between the Question (Segment A) and the Paragraph containing the answer (Segment B).

---

## DistilBERT

DistilBERT is the "lite" version of BERT. It was created by the team at Hugging Face to solve the problem of BERT being too big and slow for everyday apps.
Think of it as a concentrated version of the original: it keeps about 97% of BERT's performance but is 40% smaller and 60% faster.

**How it works: Knowledge Distillation**
It uses a "Teacher-Student" technique:

- **The Teacher:** A full-sized, pre-trained BERT model.
- **The Student:** DistilBERT, which has fewer layers (6 layers instead of BERT's 12).
- **The Process:** During training, the student doesn't just look at the raw data; it tries to mimic the teacher's exact output probabilities. It learns the "nuances" of how the big model thinks without needing all the extra brain cells.

**The Key Differences**

- **Lower Latency:** Because it has half the layers, it processes text much faster, making it perfect for mobile phones or real-time chatbots.
- **Smaller Footprint:** It takes up significantly less disk space and requires less RAM, reducing cloud hosting costs.
- **No NSP:** DistilBERT removes the Next Sentence Prediction task entirely, focusing only on the language modeling.

**When should you use it?**

- Use BERT if you need the highest possible accuracy for complex research.
- Use DistilBERT if you are building a production app where speed and cost matter more than a 2-3% difference in score.

---

## Transformers as Feature Extractors

Transformers as feature extractors involves taking a pre-trained Transformer model, "freezing" its weights, and using the numerical representations (embeddings) it produces as input for another model. This technique is a form of transfer learning that leverages the "general knowledge" a model has already gained from massive datasets.

**Key Approaches**

- **Frozen Weights:** Unlike fine-tuning, the weights of the Transformer remain unchanged. This is computationally efficient and requires significantly less power and time.
- **Hidden State Extraction:** The output of the last hidden layer (or a specific token like the [CLS] token) is typically used as the feature vector.
- **Downstream Tasks:** These extracted features are then fed into simpler, task-specific models like linear classifiers, Support Vector Machines (SVMs), or light neural network heads.

**Applications Across Modalities**

- **Natural Language Processing (NLP):** Extracting semantic meanings from text for sentiment analysis, emotion detection, or document similarity.
- **Computer Vision (CV):** Vision Transformers (ViTs) process images as sequences of patches. They excel at capturing global context and long-range dependencies that traditional CNNs might miss.
- **Audio & Signal Processing:** Preparing input features from raw audio signals (e.g., Log-Mel Spectrograms) or complex data like EEG signals for specialized classification.

**Advantages:**

- no need for expensive retraining.
- Works well even with very small target datasets.
- Complexity Simplifies machine learning pipelines.

**Limitations:**

- Performance may be slightly lower than a fully fine-tuned model.
- Transformer backbones themselves require massive data to be effective initially.
- Quadratic complexity relative to input length can be memory-intensive.

---

## Scaling Transformers

Scaling Transformers is the pursuit of better performance by increasing the size of the model, the data, or the compute. This field is governed by "Scaling Laws," which suggest that as you increase these three variables, the model's error (loss) decreases in a highly predictable, logarithmic way.

**1. The Three Dimensions of Scaling**
To scale a Transformer effectively, you generally adjust three specific knobs:

- **Parameters:** Increasing the number of layers, hidden dimensions, and attention heads.
- **Data:** Increasing the number of tokens the model sees during training (the "training budget").
- **Compute:** The total floating-point operations (FLOPs) available, usually dictated by the number of GPUs and training time.

**2. The Chinchilla Optimality**
For a long time, the industry followed "Kaplan’s Scaling Laws," which prioritized model size over data. However, DeepMind’s Chinchilla research corrected this:

- **The Rule:** To be "compute-optimal," for every doubling of model size, you should also double the amount of training data.
- **The Result:** Many early models (like GPT-3) were actually "over-parameterized" and "under-trained." Modern models like Llama 3 scale by training relatively smaller models on massive amounts of data (up to 15 trillion tokens) to make them more efficient for users.

**3. Architectural Scaling Techniques**
Simply making a model bigger can lead to instability or hardware bottlenecks. Engineers use these techniques to manage scale:

- **Mixture of Experts (MoE)** Only activates a fraction of the total parameters (e.g., 2 out of 8 "experts") for each token. Massive parameter count (e.g., Mixtral 8x7B) with the inference speed of a much smaller model.
- **FlashAttention** Optimizes how the GPU memory handles the Attention mechanism. Allows scaling to much longer Context Windows (128k+) without crashing.
- **Parallelism (TP/PP)** Splits the model across multiple GPUs (Tensor or Pipeline parallelism). Enables training models too large to fit in a single GPU's VRAM.

**4. Challenges of Extreme Scale**

- **Diminishing Returns:** Eventually, the gain in performance for each extra million dollars spent on compute starts to level off.
- **Data Exhaustion:** We are running out of high-quality, human-written text on the public internet. This has led to a focus on Synthetic Data generation.
- **Post-Training Bottlenecks:** A "scaled-up" model is harder to fine-tune, align with RLHF, and deploy on standard consumer hardware.

**5. Emerging Trend: "Scaling Down"**
While the frontier moves toward "Trillion-parameter" models, there is a massive counter-movement toward Small Language Models (SLMs) like Microsoft’s Phi-3. These use high-quality, textbook-grade data to achieve the reasoning capabilities of much larger models at a fraction of the size.

---

## T5

## GPT

## GPT 2

## DeepSeek

## LLAMA

## Mixture of Experts
