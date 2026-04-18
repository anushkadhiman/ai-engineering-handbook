# Diffusion Model

A diffusion model is a class of generative AI that learns to create high-quality data (like images, audio, or video) by reversing a process of gradual destruction. Inspired by non-equilibrium thermodynamics, it treats data points like molecules that disperse into random noise over time.

**Core Mechanism**
The model operates through two distinct phases:

- **Forward Diffusion (Noising):** The model systematically adds Gaussian noise to a training image in a series of small steps. By the end of this Markov chain, the original data is completely "destroyed" and turned into pure random static.
- **Reverse Diffusion (Denoising):** A neural network—typically a U-Net or Transformer—is trained to predict and remove the noise added at each step. Once trained, the model can start with a sample of pure noise and "denoise" it step-by-step to "hallucinate" a brand-new, high-fidelity image.

**Popular Applications & Models**
Diffusion models have recently overtaken Generative Adversarial Networks (GANs) in popularity due to their superior stability and output diversity.

- **Image Generation:** Powering tools like Stable Diffusion, DALL-E 3, and Midjourney.
- **Image Editing:** Capabilities like inpainting (filling in missing parts of an image) and outpainting (extending an image beyond its borders).
- **Scientific Research:** Used for drug design, molecule generation, and modeling complex physical simulations.
- **Video & Audio:** Emerging as the standard for high-fidelity video synthesis and 44.1kHz stereo audio production.

**Key Advantages vs. Limitations**

- **Pros:** They avoid "mode collapse" (where a model repeats the same few outputs), are easier to train than GANs, and capture much more intricate details in complex data distributions.
- **Cons:** Generating a single image is computationally expensive and slow because the model must run hundreds or thousands of denoising iterations. Techniques like Latent Diffusion (LDMs) and Consistency Models are currently being developed to speed up this process.

## Mathematical intution

The intuition behind a diffusion model is to learn how to un-break data. It systematically destroys the structure of an image with noise and then trains a neural network to restore that structure step-by-step.

The model is formulated as a Markov chain—a sequence of steps where each state depends only on the one before it.

<div style="text-align: center;">
  <img src=".\forward process.PNG" alt="Centered image">
</div>

<div style="text-align: center;">
  <img src=".\reverse_process.PNG" alt="Centered image">
</div>

---

## Variance Schedule

Variance schedule is the blueprint for how we destroy the data. It defines exactly how much noise is added at each discrete step of the process.

Think of it as a volume knob for the static: if you turn it up too fast, the model loses the image structure too quickly to learn anything; if you turn it up too slow, you waste computational power on thousands of redundant steps.

**The Mathematical Definition**
The variance schedule is a sequence of values denoted by (beta), where ranges from 1 to T (often T=1000).

<div style="text-align: center;">
  <img src=".\variance_schedule.PNG" alt="Centered image">
</div>

**Common Schedule Types**
Choosing how beta changes over time is a critical hyperparameter.

There are three common strategies:

1. **Linear:** The beta increases steadily from a small value (e.g. 0.0001) to a larger one (eg., 0.02).It's simple and effective; used in the original DDPM paper.
2. **Cosine:** It follows a cosine curve, adding very little noise at the start and end. It prevents the "image information" from dropping to zero too quickly in the middle steps.
3. **Sigmoid:** S-shaped curve; starts slow, speeds up in the middle, and levels off. Useful for high-resolution images where early structure is precious.

**Why do we need a schedule?**
The schedule ensures a smooth transition of information.

- **For the Forward Process:** We need the final state to be indistinguishable from pure white noise. The schedule ensures that by the time we reach step, the original signal has decayed to nearly zero.
- **For the Reverse Process:** If the noise added at each step is too large, the "jump" between and is too great for the neural network to accurately predict. A schedule allows the model to learn incremental refinements, making the generation process stable.

---

## what are the assumptions?

Diffusion models rely on several key mathematical and structural assumptions to ensure that the complex task of creating data from noise remains solvable.

**The Markov Assumption**
The most fundamental structural assumption is that the diffusion process (both forward and backward) is a Markov Chain.

- Definition: Each state in the process depends only on the state immediately preceding it and not on any earlier history.
- Why it matters: This simplifies the joint probability of all diffusion steps into a product of individual transitions, making the math tractable for deep learning.

**The Gaussian Transition Assumption**
The model assumes that the "jumps" between steps are Gaussian (Normal) distributions.

- Forward process: Each step is assumed to add a small amount of Gaussian noise.
- Reverse process: It is assumed that if the noise added at each step is sufficiently small and the number of steps is large, the reverse step is also approximately Gaussian. This allows the neural network to be trained simply to predict the mean and variance of a Gaussian distribution.

**The Isotropic Gaussian Prior**
At the end of the forward process (step), the data is assumed to have evolved into a pure isotropic Gaussian noise distribution.

- Requirement: The variance schedule must be "well-behaved" enough to ensure that the original signal is almost entirely destroyed by step.
- Application: This allows the model to "start from scratch" during generation by sampling random noise from a standard normal distribution .

**Variance Schedule**
In standard implementations like DDPM, the variance schedule is typically assumed to be a fixed hyperparameter rather than a learned parameter.
This removes the need to calculate gradients for the noising process itself, drastically simplifying the loss function to a straightforward mean squared error between predicted and actual noise.

**Manifold Hypothesis**
While not a formal "equation" assumption, diffusion models operate under the Manifold Hypothesis: the idea that high-dimensional data (like images) actually lies on a much lower-dimensional "surface" within that space.

---

## Time Embedding

In a diffusion model, the network (U-Net) is a multi-tasker. It has to know how to denoise an image that is 99% noise (t=99) and an image that is 1% noise (t=1). Since the weights of the neural network are shared across all steps, we use Time Embeddings to tell the model exactly where it is in the process.

**Why do we need it?**
A denoising network sees different features at different times:

- **Large (High Noise):** The model needs to focus on global structure (e.g., "Is this a dog or a mountain?").
- **Small (Low Noise):** The model needs to focus on fine details (e.g., fur texture or eye reflections).

Without a time embedding, the model wouldn't know whether to sculpt a general shape or polish a detail.

**How it works: Sinusoidal Positional Embeddings**

Diffusion models typically borrow the Sinusoidal Embedding technique from the Transformer architecture.

Instead of just passing the integer (like 452), we transform it into a high-dimensional vector using sine and cosine functions of different frequencies:

**Why this math?**

- **Uniqueness:** Every timestep gets a unique fingerprint.
- **Relative Distance:** The model can easily learn that step 450 is close to step 451.
- **Extrapolation:** It allows the model to handle a range of timesteps it might not have seen perfectly during training.

**Integration into the U-Net**

- Once the time integer is converted into a vector (the embedding), it is processed through a couple of MLP (Multi-Layer Perceptron) layers to match the width of the U-Net's layers.
- It is then injected into the network in two main ways:
  - Addition: The time vector is added directly to the feature maps of the Residual Blocks.
  - Adaptive Normalization (AdaGN): The time embedding is used to scale and shift the hidden layers (similar to how StyleGAN uses styles).

**The Intuition**
Think of the Time Embedding as a context key. When the U-Net receives a noisy image, it checks the "key" (the time embedding).
• If the key says "Step 900," the U-Net activates its "big-picture" neurons.
• If the key says "Step 20," the U-Net activates its "refinement" neurons.

---

## Controlnet

While a standard diffusion model uses a text prompt to guide what an image should contain, a ControlNet allows you to use an image-based spatial condition to guide the structure.
It is the difference between telling an artist "Paint a man sitting on a chair" and giving that artist a sketch or a pose and saying "Paint exactly this, but make it a man."

**The Architecture:**
ControlNet works by making a "locked" and a "trainable" copy of the diffusion model's encoding layers (the U-Net).

- **The Locked Model:** The original Stable Diffusion model is frozen. This preserves the high-quality generation capabilities it already learned from billions of images.
- **The Trainable Copy:** A clone of the U-Net's encoder blocks. This copy is trained on a specific task (like understanding edges or human skeletons).
- **Zero Convolutions:** These are convolutional layers initialized with weights of zero. They connect the trainable copy back to the locked model.

**Why zeros?** At the very start of training, the ControlNet outputs nothing, so the original model behaves exactly as it normally would. This prevents "noise" from the new training from breaking the base model's knowledge.

**How it Processes Data**

- **Input:** You provide a text prompt AND a conditioning image (e.g., a Canny edge map, a depth map, or a Pose skeleton).
- **Feature Extraction:** The ControlNet trainable copy processes the conditioning image.
- **Injection:** The features extracted by the ControlNet are added to the features of the main U-Net.
- **Denoising:** The main U-Net denoises the image, but its "path" is now physically constrained by the spatial data injected from the ControlNet.

**Common Types of Control**
ControlNet is modular. You can download different "weights" depending on what kind of control you need:

- Canny / SoftEdge: Turning a sketch into a photo.
- OpenPose Human skeleton (joints/limbs): Exact control over a character's stance.
- Depth 3D distance/geometry: Keeping the spatial layout of a room.
- Scribble Rough hand-drawn lines: Creating art from a 10-second doodle.
- Segmentation Color-coded areas (sky, grass, car): Precise layout of complex scenes.

---

## Stable Diffusion

Stable Diffusion is the speed-optimized evolution of diffusion models. While standard models like DDPM are computationally heavy because they work directly on pixel data, Stable Diffusion performs the entire process in a compressed mathematical space.

**The Core Innovation: Latent Space**

The biggest bottleneck in image generation is the sheer number of pixels (e.g., an image has 262,144 pixels). Stable Diffusion solves this by using a Latent Diffusion Model (LDM).

- **The VAE (Variational Autoencoder):** Instead of working on pixels, the model uses a VAE to compress the image into a "latent" representation that is 8x or 64x smaller.
- **Denoising in Latents:** The diffusion process (the U-Net) happens entirely within this tiny, compressed space. This is why Stable Diffusion can run on a consumer laptop, whereas older models required massive server farms.
- **Decoding:** Once the "latent" is denoised, the VAE decoder blows it back up into a full-resolution pixel image.

**The Three Key Components**

Stable Diffusion is like a three-part orchestra:

- **CLIP Text Encoder:** This takes your prompt (e.g., "a cat in a space suit") and turns it into a mathematical vector (embedding) that the U-Net can understand. It acts as the director.
- **U-Net (The Denoiser):** This is the "brain." It receives the noisy latents and the text embedding. Guided by the text, it predicts the noise to remove at each step.
- **VAE (The Translator):** As mentioned above, it handles the compression from pixels to latents and back again.

**Conditioning & Cross-Attention**
How does the model actually "see" your text? It uses a mechanism called Cross-Attention.

Inside the U-Net, the image features "look" at the text features. For every pixel, the model asks: "Which word in the prompt should I be paying attention to right now?" This ensures that if you type "red hat," the "red" and "hat" concepts are applied to the correct spatial area of the image.

**Benefit**

- **Efficiency:** It brought high-end AI generation to home GPUs (8GB VRAM is often enough).
- **Versatility:** Because it works in latent space, it is incredibly easy to extend with tools like ControlNet, LoRA (for style training), and Inpainting.

---

## ComfyUI

ComfyUI is a powerful, node-based graphical user interface (GUI) and backend for Stable Diffusion that allows us to create custom, complex AI image and video generation workflows locally. It provides fine-grained control over the generation process—including ControlNet and inpainting—by connecting individual functional blocks, or nodes.

**Why do we use ComfyUI?**

• Node-Based Workflow: Instead of simple text prompts, you design a flowchart (graph) connecting components (e.g., Load Checkpoint -&gt; Prompt -&gt; KSampler -&gt; VAE Decode).
• Local & Free: Runs on your own computer (NVIDIA GPU recommended), ensuring privacy and no generation costs.
• Highly Efficient: Known for being lightweight and efficient, often enabling faster generation than other GUIs.
• Reproducibility: Workflows can be saved within generated PNG images, allowing you to drag and drop images back into the app to restore the exact creation process.
• Customization: Supports extensive customization via custom nodes for specialized tasks, including image-to-video, upscaling, and advanced AI techniques.

ComfyUI is designed for power users seeking detailed control over AI imagery rather than quick, simple generation.

---
