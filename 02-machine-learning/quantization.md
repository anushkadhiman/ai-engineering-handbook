# Quantization

Quantization is an optimization technique that reduces the precision of a model's weights and activations to make it smaller and faster. By converting high-precision numbers (typically 32-bit floating point) into lower-precision formats like 8-bit integers (INT8) or even 4-bit (INT4), you significantly cut down on memory usage and speed up inference, especially on edge devices like smartphones.

**Why Quantize?**

- **Reduced Memory Footprint:** A model quantized from 32-bit to 8-bit is roughly 4x smaller, allowing large models to fit on consumer hardware.
- **Faster Inference:** Integer arithmetic is less computationally expensive than floating-point math, leading to quicker response times.
- **Energy Efficiency:** Lower precision requires fewer clock cycles and less power, which is critical for battery-powered devices.

**Core Types of Quantization**
Practitioners generally choose between two main workflows:

- **Post-Training Quantization (PTQ):** Applied to a model after it has been fully trained. It's fast and doesn't require the original training pipeline, making it the most common choice for deploying pre-trained models.
- **Dynamic:** Quantizes weights once, but computes activation ranges "on the fly" during inference.
- **Static:** Uses a small "calibration" dataset to pre-calculate activation ranges for even faster execution.
- **Quantization-Aware Training (QAT):** Simulates quantization effects during the training or fine-tuning process. The model "learns" to compensate for the lost precision, typically resulting in higher final accuracy than PTQ.
  Popular Modern Techniques
- **GPTQ:** A popular method for LLMs that quantizes weight matrices layer-by-layer to 4-bit precision with minimal accuracy loss.
- **AWQ (Activation-aware Weight Quantization):** Identifies and protects "salient" weights (those most important for performance) from heavy quantization based on activation patterns.
- **QLoRA:** Combines 4-bit quantization with Low-Rank Adaptation (LoRA), allowing you to fine-tune massive models on a single GPU.

Most major frameworks provide built-in support for these workflows:

- PyTorch: Offers a comprehensive Quantization API for PTQ and QAT.
  TensorFlow / TFLite: Specifically optimized for deploying mobile and edge models via the Model Optimization Toolkit.
- NVIDIA TensorRT: A high-performance inference SDK that uses symmetric quantization to maximize GPU throughput.
- Hugging Face: Their bitsandbytes library is the industry standard for loading large models in 8-bit or 4-bit mode with just one line of code.

---

## Quantization

Quantization can be categorized by when it occurs, how it maps values, and its granularity.
**1. By Timing (When it's applied)**

- **Post-Training Quantization (PTQ):** Applied to a model after it is fully trained. It is fast and requires little data but can lead to accuracy loss.
- **Dynamic PTQ:** Calculates the quantization range for activations on the fly during inference.
- **Static PTQ:** Uses a small calibration dataset to pre-calculate ranges for faster inference.
- **Quantization-Aware Training (QAT):** Simulates quantization effects during training. This allows the model to adjust to the lower precision, typically yielding the highest accuracy.

**2. By Mapping Scheme (How values are converted)**

**Uniform vs. Non-Uniform:**

- **Uniform:** Divides the input range into equal-sized steps. It is the simplest to implement and ideal for evenly distributed data.
- **Non-Uniform:** Uses variable step sizes, providing higher precision for frequently occurring values. This is common for speech and audio where small amplitudes are more frequent.

**Symmetric vs. Asymmetric (Affine):**

- **Symmetric:** The floating-point range is centered around zero, mapping 0.0 directly to the integer 0. It is computationally efficient but can waste precision if data is skewed.
- **Asymmetric:** Uses a "zero-point" to map the input range to the full integer spectrum. This is more accurate for non-centered distributions, such as ReLU activations.

**3. By Granularity (Scope of the conversion)**

- **Per-Tensor (Layer-wise):** One set of quantization parameters (scale and zero-point) is used for an entire layer/tensor.
- **Per-Channel:** Separate parameters are used for each output channel of a layer, which helps handle outliers and improves accuracy.
- **Per-Block (Group-wise):** Divides a tensor into even smaller blocks (e.g., 64 or 128 weights) to minimize the impact of extreme outliers.

**4. By Target Data Type (Precision level)**

- **Integer Quantization:** Converting to INT8 (most common) or INT4.
- **Float Quantization:** Using lower-precision float formats like FP8, FP4, or specialized types like NormalFloat 4 (NF4) used in QLoRA.

---

## Post‐Training Quantization (PTQ)

Post-Training Quantization (PTQ) is a model compression technique used to convert a pre-trained, high-precision model (typically 32-bit float) into a lower-precision format (like 8-bit integer) without retraining the original model. It is widely used to reduce model size, speed up inference, and lower power consumption for deployment on edge devices.

**How PTQ Works**
The goal of PTQ is to find the best mapping between high-precision values and low-precision integers by determining two key parameters for each layer: a Scale (step size) and a Zero-point (the offset representing 0.0).

- **Weight Quantization:** This is straightforward because weights are constant. Their range (min/max) is already known, so they can be converted to integers offline before deployment.
- **Activation Quantization:** Activations change based on the input data. PTQ handles this in two main ways:
- **Dynamic Quantization:** The range for activations is calculated "on the fly" during inference. This is easy to implement but adds a small computational overhead.
- **Static Quantization:** The range is pre-calculated during a Calibration phase. A small "representative dataset" (usually 100–500 samples) is run through the frozen model to record typical activation ranges.

**Key Benefits**

- **Ease of Use:** You don't need the original training code, high-end GPU clusters, or the full dataset. You only need the final model and a few data samples.
  **Significant Compression:** Moving from 32-bit (FP32) to 8-bit (INT8) reduces the model's memory footprint by 4x.
- **Hardware Compatibility:** Many low-power chips (like those in phones or IoT devices) are optimized specifically for integer math rather than floating-point math.

**Limitations**

- **Accuracy Loss:** Because the model wasn't "taught" to handle lower precision, PTQ can cause a drop in accuracy, especially in smaller or more sensitive models.
- **Calibration Bias:** If the small calibration dataset isn't truly representative of real-world inputs, the pre-calculated ranges might be wrong, leading to poor performance.

---

## Quantization‐Aware Training (QAT)

Quantization-Aware Training (QAT) is a method where a model is trained or fine-tuned while simulating the effects of low-precision storage (like INT8).
Unlike Post-Training Quantization (PTQ), which converts a model after it’s finished, QAT introduces quantization errors during the training process so the model can learn to compensate for them.

**How It Works: "Fake Quantization"**
Since actual integer math isn't differentiable (you can't do standard calculus on discrete integers), QAT uses fake quantization modules:
Forward Pass: Weights and activations are rounded to low-precision values (e.g., INT8) to simulate how the model will behave on edge hardware.

- **Loss Calculation:** The model sees the "damage" caused by rounding and calculates its error based on these degraded values.
- **Backward Pass:** The gradients are calculated using high-precision floats (FP32) using a trick called the Straight-Through Estimator (STE). This allows the model to update its weights in a way that minimizes the rounding error.

**Why Use QAT?**

- **Superior Accuracy:** It is the "gold standard" for quantization. Because the model "practices" being low-precision during training, it usually suffers almost zero accuracy loss compared to the original FP32 model.
  Essential for Low Bit-Widths: If you are trying to compress a model down to 4-bit or 2-bit, PTQ often fails completely. QAT is usually required to keep the model functional at these extreme levels.
- **Robustness:** It handles "outlier" weights better than PTQ because the model can shift its weight distribution to avoid values that would be clipped or rounded poorly.

**The Trade-offs**

- **Computationally Expensive:** You are essentially performing a full training or fine-tuning run, which requires GPUs, time, and the original training dataset.
- **Complexity:** It requires more engineering effort to set up the "fake quantization" layers correctly within the training pipeline.

**Popular Tools**

- PyTorch: Offers Quantization-Aware Training APIs that automatically swap standard layers for quantized versions.
- TensorFlow: The Model Optimization Toolkit provides a simple wrapper to make a model "quantization aware" with a few lines of code.
- NVIDIA TensorRT: Supports QAT by importing "QDQ" (Quantize/Dequantize) nodes from ONNX models.

---

## Mixed Precision Training

Mixed Precision Training is a technique that speeds up deep learning by using both 16-bit (half precision) and 32-bit (single precision) floating-point numbers during the same training session.
It gives you the best of both worlds: the speed of lower precision and the accuracy of higher precision.

- **How It Works:**
  The key challenge is that 16-bit floats (FP16) have a very narrow range. If a gradient is too small, it becomes zero (underflow); if too large, it becomes "NaN" (overflow).

Mixed precision solves this using three steps:

- **The Half-Precision Pass:** The model performs the heavy math (forward and backward passes) in FP16. This is significantly faster on modern GPUs with NVIDIA Tensor Cores.
- **The Master Weights:** The optimizer maintains a "master copy" of the weights in FP32. After the FP16 gradients are calculated, they are used to update these high-precision master weights to ensure numerical stability.
- **Loss Scaling:** To prevent small gradients from disappearing (underflow), the loss is multiplied by a large scale factor before backpropagation. It is then scaled back down before the weights are updated.

**Why Use It?**

- **Faster Training:** You can see speedups of 2x to 5x depending on your hardware and model architecture.
- **Reduced VRAM Usage:** FP16 tensors take up half the memory of FP32, allowing you to double your batch size or train much larger models on the same GPU.
- **No Accuracy Loss:** When implemented correctly with loss scaling, the final model accuracy is typically identical to full FP32 training.

**BF16:** If you are using newer hardware (like NVIDIA A100/H100 or TPU), you likely to use BF16 (Brain Floating Point).

- FP16 has a small range but high precision.
- BF16 has the same range as FP32 but lower precision.

The Benefit: BF16 is much more stable because it handles large numbers easily, often making Loss Scaling unnecessary.

---

## Weight Pruning Methods

Weight pruning methods reduce the size and computational load of neural networks by identifying and removing redundant or less significant parameters. These methods are generally categorized by their granularity (what is removed) and their timing (when they are applied).

**1. Granularity: Structured vs. Unstructured**

- **Unstructured Pruning (Fine-Grained):** Individual weights are zeroed out based on criteria like low magnitude.
  - Pros: Can achieve extreme sparsity (e.g., 90–99%) with minimal accuracy loss.
  - Cons: Often results in irregular sparse matrices that require specialized hardware or libraries to see real-world speedups.

- **Structured Pruning (Coarse-Grained):** Entire structural units are removed, such as neurons, convolutional filters, channels, or even whole layers.
  - Pros: Hardware-friendly; results in dense matrices that immediately accelerate inference on standard CPUs and GPUs without custom software.
  - Cons: More aggressive than unstructured pruning, which can lead to a more significant drop in accuracy if not carefully managed.

**2. Selection Criteria (What to Prune)**

- **Magnitude-Based:** The most common method; it assumes weights with the smallest absolute values (near-zero) contribute the least to model performance and can be safely removed.
- **Gradient-Based:** Evaluates weight importance by their sensitivity to the loss function during training; weights with small gradients are considered less significant for optimization.
- **Activation-Based:** Uses a calibration dataset to estimate importance based on which parts of the model activate the most.
- **Movement Pruning:** Specifically for transfer learning, this method identifies weights that "shrink" toward zero during fine-tuning on a new task as being less significant than those that grow.

**3. Timing and Process**

- **One-Shot Pruning:** The model is pruned in a single step after full training, followed by fine-tuning to recover performance.
- **Iterative Pruning:** A "prune-train-repeat" cycle that gradually increases sparsity, allowing the model to adapt and recover accuracy at each stage.
- **Train-Time (Dynamic) Pruning:** Pruning occurs simultaneously with training, often encouraged by regularization techniques (like L1/L2 penalties) that force weights toward zero.
- **Lottery Ticket Hypothesis:** Proposes that large networks contain "winning ticket" subnetworks that can reach the same accuracy as the original when trained from the same initial state.

---
