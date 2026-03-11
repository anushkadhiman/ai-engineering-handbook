## LoRA and QLoRA

Parameter-Efficient Fine-Tuning (PEFT) that allow you to adapt massive AI models (like LLMs) to specific tasks using a fraction of the memory and compute power required for traditional training.

**LoRA (Low-Rank Adaptation)**
LoRA works by freezing the original weights of the pre-trained model and adding small, trainable "adapter" matrices to specific layers (usually attention layers).

- **How it works:** Instead of updating a giant weight matrix (e.g., ), LoRA decomposes the update into two much smaller matrices (e.g., and , where is a small rank like 8 or 16).
- **Key Advantage:** It reduces the number of trainable parameters by up to 10,000 times. Because the original weights are frozen, it also prevents "catastrophic forgetting" where the model loses its original general knowledge.
- **Inference:** The adapters can be merged back into the main model, meaning there is zero added latency during use.

**QLoRA (Quantized LoRA)**
QLoRA is an advanced version that adds quantization to LoRA to save even more memory, allowing you to fine-tune massive models (like Llama-65B) on a single consumer GPU.

- **How it works:** It compresses the base model's weights into a 4-bit format (specifically NormalFloat4) to drastically reduce storage. The LoRA adapters are then trained in higher precision (16-bit) to correct any errors introduced by this compression.
- **Key Features:** It introduces techniques like Double Quantization (compressing the compression constants themselves) and Paged Optimizers (moving data to CPU RAM when VRAM is full) to push hardware limits.
- **Trade-off:** It is slightly slower than LoRA due to the constant quantization/dequantization steps but requires significantly less VRAM.
