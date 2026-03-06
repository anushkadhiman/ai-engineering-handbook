### Image segmentation

Image segmentation is a high-precision computer vision technique that partitions an image into discrete groups of pixels called segmentation masks. While object detection uses rectangular "bounding boxes" to locate items, segmentation identifies the exact shape and boundary of every object at the pixel level.

**The Three Core Types**
Computer vision tasks are typically divided based on how they handle "things" (countable objects like cars) and "stuff" (uncountable regions like sky).

1. **Semantic:** Assigns a class label to every pixel (e.g., "road," "sky," "person"). Groups all instances of a class into one "blob." Multiple people are just one "person" segment.
2. **Instance:** Identifies and masks individual objects of interest. Differentiates between separate objects of the same class (e.g., Person 1 vs. Person 2).
3. **Panoptic:** A hybrid approach that labels every pixel in the scene. Combines semantic (for "stuff" like sky) and instance (for "things" like cars) for holistic scene understanding.

#### Segment Anything Model (SAM)

The Segment Anything Model (SAM), developed by Meta AI, is a foundational artificial intelligence model designed to "cut out" any object in any image with a single click. Unlike traditional models trained for specific categories (like "cats" or "cars"), SAM is promptable, meaning it can segment objects it has never seen before by following simple user inputs.

How SAM Works
SAM uses a high-performance encoder-decoder architecture that separates heavy image processing from lightweight user interaction:
Image Encoder: A powerful Vision Transformer (ViT) processes the entire image once to create a "dense embedding"—a mathematical representation of the image's features. This part is computationally heavy but only happens once per image.
Prompt Encoder: This component translates user inputs into "sparse embeddings". It supports:
Points: A click on or off an object.
Bounding Boxes: A rectangle drawn around an area.
Text: Describing the object (though less common in basic versions).
Masks: Using an existing rough mask to refine a shape.
Mask Decoder: A fast, lightweight neural network that combines the image embedding with the prompt embedding. Because it is efficient, it can generate the final segmentation mask in real-time (about 50ms) as you move your mouse or change prompts.
Key Strengths
Zero-Shot Generalization: SAM can segment novel objects in unfamiliar domains (like medical or satellite imagery) without any additional training.
Handling Ambiguity: If a prompt is unclear (e.g., clicking on a shirt could mean the "shirt" or the "person"), SAM can output multiple valid masks representing different interpretations.
Massive Training Data: It was trained on the SA-1B dataset, containing over 1.1 billion masks across 11 million images, the largest of its kind.
Evolution of SAM
SAM 2: Introduced in July 2024, it adds a memory mechanism to track and segment objects across video frames, even if they are temporarily hidden.
SAM 3: Announced in late 2025, it focuses on Concept Segmentation, allowing users to find and track every instance of a specific concept (like "every yellow bus") throughout a video using text or example images.

#### SAM 2 (Segment Anything Model 2)

SAM 2 (Segment Anything Model 2), released by Meta AI in July 2024, is the first unified foundation model capable of segmenting and tracking any object across both images and videos in real-time.
How SAM 2 Works
SAM 2 extends the original "Segment Anything" task to the video domain. While the first SAM could only process static images, SAM 2 treats an image as a "single-frame video" and uses a streaming architecture to handle temporal data.
Core Architecture Components
Image Encoder (Hiera): It uses a hierarchical Vision Transformer (Hiera) to extract feature embeddings from each video frame one by one. This new encoder is much faster, making SAM 2 roughly 6x faster than the original SAM for image segmentation.
Memory Bank: This is the "secret sauce" of SAM 2. It maintains a FIFO (First-In, First-Out) queue of:
Past frame features: Recent frames to track movement.
Prompted frames: Information from frames where you specifically clicked or provided a box.
Memory Attention Module: When a new frame arrives, this module "attends" to the information in the memory bank to understand where the object was and how it looked previously. This allows the model to maintain temporal consistency.
Occlusion Head: A specialized component that predicts whether the target object is currently visible or hidden behind something else (occluded). This helps the model "pick up" the object again once it reappears.
Mask Decoder: This produces the final segmentation mask for the current frame by combining current image features, user prompts, and context from the memory attention module.
Key Improvements Over SAM 1
Video Tracking: You can click an object in just one frame, and SAM 2 will automatically track and mask it throughout the entire video timeline.
Interactive Refinement: If the tracking drifts or makes a mistake, you can simply click on a future frame to correct it. The model will then re-propagate the improved mask forward and backward through the video.
Open Source: Meta has open-sourced the code and weights under the Apache 2.0 license and released the SA-V dataset (51,000+ videos) for the research community.
