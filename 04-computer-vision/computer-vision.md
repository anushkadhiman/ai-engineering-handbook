# Computer vision

Computer vision is a field of artificial intelligence (AI) that enables computers to interpret, analyze, and understand visual information from the world, such as digital images and videos. By leveraging deep learning and neural networks, machines can identify, classify, and react to objects, simulating human visual capabilities.

**How it Works:** It uses algorithms to process, segment, and detect patterns in visual data (pixels), often requiring massive datasets to train models.
**Core Tasks:** Key functions include image classification (what is in the image), object detection (where is the object), segmentation (defining object boundaries), and facial recognition.
**Technologies:** Popular frameworks for developing these systems include OpenCV, TensorFlow, and PyTorch, with algorithms like YOLO allowing for real-time detection.

**Common Applications**

- **Healthcare:** Analyzing medical images (X-rays, MRIs) for diagnosis.
- **Autonomous Vehicles:** Enabling cars to recognize lanes, obstacles, and traffic signs.
- **Security & Surveillance:** Facial recognition and monitoring for unauthorized access.
- **Manufacturing:** Automating quality control by identifying defects on production lines.
- **Retail:** Powering "just walk out" technology and tracking inventory.

**Why it Matters**
Computer vision is transforming industries by automating tasks that previously required human sight, increasing efficiency, enhancing safety, and enabling new, automated AI-driven processes.

---

## Computer vision tasks

Computer vision tasks are the specific functions that enable machines to "see" and interpret visual data from images and videos. These tasks range from simple categorization to complex 3D scene reconstruction.

**Core Computer Vision Tasks**

- Image Classification: The most foundational task, where the system assigns a single label to an entire image (e.g., "this is a cat").
- Object Detection: This task identifies specific objects within an image and locates them by drawing bounding boxes around them.
- Image Segmentation: A more granular version of detection that outlines the exact pixels belonging to an object. It includes:
- Semantic Segmentation: Groups all pixels of the same category (e.g., all "car" pixels) without distinguishing between individual cars.
- Instance Segmentation: Differentiates between individual objects of the same class (e.g., identifying Car A vs. Car B).
- Panoptic Segmentation: A hybrid approach that identifies both object instances and the overall background.
- Object Tracking: Used in video analysis to follow a specific object across consecutive frames, maintaining its identity as it moves.
- Facial Recognition: A specialized form of object recognition focused on identifying or verifying an individual's identity based on their facial features.
- Pose Estimation: Determines the spatial position and orientation of objects or human body parts, often by tracking key points like joints.

**Advanced and Specialized Tasks**

- Optical Character Recognition (OCR): Extracts and converts text from images or scanned documents into a machine-readable format.
- Scene Reconstruction: Computes a 3D model of a real-world object or environment from 2D images or video sequences.
- Image Generation: Uses generative AI (like GANs) to create new images from text prompts or to transform existing ones.
- Anomaly Detection: Specifically looks for patterns that deviate from "normal" data, often used for defect detection in manufacturing or spotting health issues in medical scans.
- Feature Matching: Finds corresponding points or regions across multiple images, which is essential for tasks like creating panoramic photos.

---

## Image processing

Image processing involves applying algorithms to digital images to enhance, analyze, or manipulate them for improved quality or data extraction. It treats images as signals or 2D matrices (pixels) to perform tasks like noise reduction, contrast adjustment, segmentation, and compression. Common applications include medical imaging, remote sensing, and computer vision.

**Main Techniques:**

- **Image Enhancement:** Improving visual quality, such as contrast adjustment or brightness correction.
- **Image Restoration:** Removing noise or degradation to recover image quality.
- **Image Segmentation:** Dividing an image into segments or regions to identify objects or features.
- **Image Compression:** Reducing image size for storage and transmission.
- **Image Analysis:** Extracting information, such as detecting patterns or recognizing objects.

**Applications:**

- **Medical Imaging:** X-rays, MRI scans, and ultrasound.
- **Satellite/Remote Sensing:** Weather prediction and environmental monitoring.
- **Computer Vision:** Industrial inspection, autonomous navigation, and facial recognition.
- **Consumer Software:** Adobe Photoshop, filters, and photo editing.

**Digital image processing (DIP)** is a subfield of signal processing that focuses on manipulating digital images using computers, offering significant advantages over analog methods, such as increased flexibility and precision.

---

## Image transformation

Image transformation processes, analyzes, and modifies digital images using geometric (spatial) or pixel-level adjustments. Key techniques include rotation, scaling, shearing, translation, and cropping to alter shape, size, or orientation. These operations are crucial for computer vision, image preprocessing, and computer graphics to enhance or correct images.

**Key Types of Image Transformations**

- **Geometric Transformations (Warping):** Alters the shape and position of an image. Examples include rotation (rotating around an axis), translation (shifting positions), and scaling (resizing).
- **Affine Transformations:** A subset of geometric transformations that preserves lines and parallelism, commonly used to correct perspective.
- **Pixel-level/Intensity Transformations:** Modifies pixel values rather than their positions, often used for brightness, color correction, and filtering.
- **Linear Algebra Approach:** Uses transformation matrices to apply mathematical operations, such as rotation matrices or translation matrices, to image coordinates.

**Common Transformation Operations**

- **Rotation:** Turning an image by a specific angle.
- **Scaling:** Changing the dimensions (resizing).
- **Translation:** Shifting the image horizontally or vertically.
- **Shearing:** Distorting the image to create a slant or skew.
- **Reflection:** Flipping the image horizontally or vertically.

**Common Use Cases**

- **Image Preprocessing:** Preparing data for machine learning models (e.g., resizing, normalizing).
- **Image Correction:** Straightening, deskewing, or correcting distortion (e.g., fisheye removal).
- **Graphic Design:** Creating visual effects, merging images, and applying filters.

---

## Image enhancement in image processing

Image enhancement in image processing improves digital image quality, contrast, and clarity for better visual interpretation or analysis without altering intrinsic data. It utilizes spatial domain (direct pixel manipulation) and frequency domain (Fourier transform) techniques to remove noise, sharpen edges, and adjust brightness.

**Key Techniques and Approaches**

**Spatial Domain Methods (Direct Pixel Manipulation):**

- **Intensity/Point Transformations:** Adjusting brightness and contrast using techniques like image negation, log transformations, and power-law (gamma) transformations.
- **Histogram Equalization:** A technique that spreads out intensity values to improve global contrast, often used to make hidden details visible.
- **Spatial Filtering:** Utilizing masks or kernels to perform smoothing (noise reduction/blurring) or sharpening (edge enhancement) directly on pixel neighborhoods.

**Frequency Domain Methods (Transforming Images):**

- Manipulates the Fourier transform of an image to enhance features. Low-pass filters smooth images, while high-pass filters sharpen them.
- Homomorphic Filtering: A technique used to normalize brightness and increase contrast across an image, often used to remove multiplicative noise.

**Primary Objectives**

• **Contrast Enhancement:** Techniques like contrast stretching increase the distinction between light and dark areas.
• **Noise Reduction:** Removing unwanted, random variation in brightness or color (denoising).
• **Sharpening:** Highlighting edges and fine details, often used in forensic analysis or imaging.
• **Color Correction:** Adjusting color balance to make images appear more natural or vibrant.

**Common Applications**

• **Medical Imaging:** Improving X-rays, CT scans, and MRIs for better diagnosis.
• **Satellite Imagery:** Enhancing aerial photographs for analysis.
• **Photography & Video:** Improving visual quality and reducing digital noise.

---

## Thresholding

Thresholding is a fundamental image segmentation technique that converts grayscale images into binary (black and white) images by separating pixels into foreground and background based on a specific intensity value. Pixels above the threshold become white, while those below become black, crucial for object detection, binarization, and noise reduction.

**Key Concepts and Types**

- **Simple (Global) Thresholding:** A single, fixed threshold value is applied to the entire image. If , it is assigned the maximum value (foreground); otherwise, it becomes (background).
- **Adaptive (Local) Thresholding:** The threshold is calculated for smaller regions of the image, allowing for better handling of varying lighting conditions and uneven illumination.
- **Otsu's Method:** An automatic thresholding technique that finds the optimal value by maximizing the variance between foreground and background pixels, ideal when the image histogram has two distinct peaks.

**Applications**

- **Image Segmentation:** Separating objects from the background.
- **Optical Character Recognition (OCR):** Converting scanned text documents into binary for character identification.
- **Medical Imaging:** Segmenting organs or tumors in scans.

**Limitations**
Simple thresholding struggles with images that have low contrast, noise, or uneven lighting, often requiring advanced adaptive techniques to achieve good results.

---

## Image noise reduction in image processing

Image noise reduction in image processing involves filtering techniques to enhance image quality by reducing undesired noise (e.g., Gaussian, salt-and-pepper). Common techniques include spatial domain filtering like Mean (smoothing), Gaussian (weighted smoothing), Median (salt-and-pepper removal), and Bilateral filters (edge-preserving), as well as advanced methods like Non-Local Means (NLM) and Block Matching 3D (BM3D).

Here are the primary noise reduction techniques:

- **Spatial Domain Filters (Spatial Filtering)**
  These filters work by modifying pixels based on their local neighborhood (e.g., a 3x3 or 5x5 window ).

- **Mean Filter (Average Filter):** Replaces each pixel's value with the average of its neighbors, reducing Gaussian noise but blurring edges.
- **Gaussian Filter:** Similar to the mean filter, but applies weights based on a Gaussian distribution, producing smoother results with less blurring than simple averaging.
- **Median Filter:** Replaces a pixel with the median value of its neighborhood, which is exceptionally effective at removing "salt-and-pepper" noise while preserving edges.
- **Bilateral Filter:** A sophisticated non-linear filter that averages neighboring pixels based on both spatial proximity and intensity similarity, smoothing flat areas while maintaining sharp edges.

**Frequency Domain Filters**
These methods transform the image to the frequency domain (using Fourier Transform), filter out high-frequency components (which often represent noise), and inverse transform it back.

- **Wiener Filtering:** A linear technique that estimates the desired image by minimizing the mean square error between the estimated and original image.

**Advanced/Non-Local Denoising**

- **Non-Local Means (NLM) Denoising:** Instead of just looking at immediate neighbors, this algorithm searches for similar patches throughout the entire image to replace pixel values, reducing noise more effectively while keeping textures.
- **Block Matching 3D (BM3D) Filter:** A highly effective technique that groups similar image blocks into 3D arrays, transforms them, applies hard thresholding, and then inverts the transform.

**Deep Learning-Based Denoising**

- **CNN-based models:** Convolutional Neural Networks (CNNs) can learn to remove complex noise patterns by training on noisy-clean image pairs, often outperforming traditional filters, especially with high-density noise.
- **Noise2Void:** A technique that allows training denoising networks using only noisy images, without needing clean ground-truth data

---

## Morphological operations

Morphological operations are non-linear image processing techniques that probe and transform images based on shapes, using a small template called a structuring element. Primarily used on binary and grayscale images for noise removal, object isolation, and boundary detection, they apply structuring elements to define, alter, or analyze shape, size, and structure.

**Key Morphological Operations**

- **Dilation:** Adds pixels to object boundaries, expanding regions and filling small holes.
- **Erosion:** Removes pixels on object boundaries, shrinking foreground objects and removing small noise particles.
- **Opening:** An erosion followed by a dilation. It removes small noise, breaks thin connections, and cleans up bright spots.
- **Closing:** A dilation followed by an erosion. It fills in small holes, gaps, and cracks in objects.

**Core Concepts**

- **Structuring Element (Kernel):** A small matrix that determines the shape and effect of the operation (e.g., box, disk, line).
- **Application:** Essential in image pre-processing, post-processing for segmentation, and feature extraction.

**Common Applications**

- **Noise Removal:** Opening removes small background noise (salt-and-pepper).
- **Object Segmentation:** Separating distinct objects that are barely connected.
- **Filling Holes:** Closing fills in gaps within an object.
- **Boundary Detection:** Using erosion or gradient operations to define edges.

---

## Feature extraction in computer vision

Feature extraction in computer vision is the process of reducing raw image data into smaller, manageable, and informative sets of features (edges, corners, textures, shapes). By transforming high-dimensional pixel data into concise, structured vectors, it enhances the performance, speed, and accuracy of machine learning models for tasks like object recognition, classification, and detection.

**Key Techniques in Feature Extraction**
Feature extraction methods can be categorized into classical, handcrafted methods and automated deep learning techniques:

- **Classical/Handcrafted Feature Descriptors:** These are algorithm-based methods designed to identify specific structures.
- **SIFT (Scale-Invariant Feature Transform):** Identifies local points, invariant to image scaling and rotation.
- **HOG (Histogram of Oriented Gradients):** Captures structure by analyzing gradients in localized portions, frequently used in object detection.
- **SURF (Speeded-Up Robust Features):** A faster, robust alternative to SIFT.
- **LBP (Local Binary Pattern):** Used for texture analysis.
- **Edge/Corner Detection:** Methods like Canny edge detection or Harris corner detection locate key points and shapes.

**Automated/Deep Learning Feature Extraction:**

- **Convolutional Neural Networks (CNNs):** Modern CNNs automatically learn to extract relevant hierarchical features (from low-level edges to high-level object parts) directly from image pixels.
- **Autoencoders:** Neural networks designed for data dimensionality reduction.

**Importance in Computer Vision**

- **Dimensionality Reduction:** Converts large pixel-level data into a compact representation, reducing computational complexity.
- **Improved Performance:** Allows algorithms to focus on essential patterns, leading to more accurate classification and object recognition.
- **Data Interpretation:** Turns unorganized pixels into meaningful information for further AI analysis.

**Typical Workflow**

- **Preprocessing:** Gray-scaling, noise reduction.
- **Extraction:** Applying filters (e.g., Canny) or models (e.g., CNNs).
- **Representation:** Organizing extracted data into feature vectors or maps.

---

## Edge detection in computer vision

Edge detection in computer vision identifies sharp intensity changes (boundaries) in images using gradient-based (e.g., Sobel, Prewitt, Roberts) or Laplacian methods, with Canny being the most robust. These techniques are crucial for object detection, image segmentation, and feature extraction by reducing image noise and highlighting structural boundaries.

**Key Edge Detection Techniques**

- **Canny Edge Detector:** Regarded as the standard, it is a multi-stage process involving Gaussian smoothing (noise reduction), finding gradients, non-maximum suppression (thinning edges), and hysteresis thresholding to link edges.
- **Sobel Operator:** A gradient-based method using
  convolution masks to calculate the first derivative, effectively detecting horizontal and vertical edges.
- **Prewitt Operator:** Similar to Sobel, it is used to detect horizontal and vertical edges, though it is slightly less precise in detecting diagonal edges.
- **Roberts Cross Operator:** A simple
  gradient operator that is quick but very sensitive to noise.
- **Laplacian of Gaussian (LoG):** A second-order derivative method that highlights rapid intensity changes (zero-crossings) after smoothing the image to reduce noise.
- **Scharr Operator:** Similar to Sobel but optimized for better gradient magnitude estimation.

**Core Approaches**

- **Gradient-Based (First-Order Derivative):** Finds maximum/minimum in the first derivative to locate edges, ideal for clear, high-contrast images.
- **Zero-Crossing (Second-Order Derivative):** Finds where the second derivative equals zero, better at detecting finer details but more sensitive to noise.

**Steps in Edge Detection**

- **Smoothing:** Reducing noise using filters (e.g., Gaussian).
- **Enhancement:** Applying operators to identify pixels with high gradient values.
- **Thresholding:** Determining which intensity changes are significant enough to be considered edges.
- **Localization:** Pinpointing the exact edge location, often using non-maximum suppression to create single-pixel wide lines.

---

## Corner and interest point detection

Corner and interest point detection identifies specific, invariant points in images (e.g., corners, blobs, edges) for tasks like stereo matching, image stitching, and object recognition. Key techniques include the Harris Corner Detector (measures intensity change), Shi-Tomasi, and scale-invariant detectors like SIFT. These methods enhance computational efficiency by focusing on high-information, distinct regions.

**Key Concepts and Techniques**

- **Harris Corner Detector:** Calculates the auto-correlation matrix to identify locations where both eigenvalues (
  ) of the intensity change are large, indicating a corner.
- **Shi-Tomasi Detector:** A variation of the Harris detector that often provides better results by using a different scoring function.
- **Scale-Invariant Feature Transform (SIFT):** A method to detect and describe local features, ensuring stability across scale, rotation, and illumination changes.
- **FAST (Features from Accelerated Segment Test):** A high-speed algorithm used for real-time applications.

**Applications**

- **Image Registration:** Aligning multiple images of the same scene.
- **Motion Tracking:** Following feature points across video frames.
- **Object Recognition:** Identifying objects based on characteristic, invariant features.
- **Stereo Matching:** Determining 3D structure from multiple 2D views.

**Methodology**
Detection generally involves calculating image gradients (using, for example, the Sobel filter), determining a corner response function, and applying non-maximum suppression to filter out weak or redundant points.

---

## Feature descriptors

Feature descriptors are numerical "fingerprints" (vectors) that represent image regions, keypoints, or textures, enabling computer vision tasks like object recognition, tracking, and image stitching. They encode local information such as gradients, edges, or intensities to ensure invariance to image transformations like scaling, rotation, and lighting changes.

**Local vs. Global:**
**Local Descriptors:** Describe a small patch around a specific point (e.g., SIFT, SURF, ORB, BRISK, FREAK). These are highly robust for matching and recognition.
**Global Descriptors:** Describe the entire image (e.g.Shape MatricesInvariant MomentsHOGCo-HOG).

**Common Algorithms:**

- **SIFT (Scale-Invariant Feature Transform):** Robust to scale and rotation changes.
- **SURF (Speeded-Up Robust Features):** A faster, approximation-based alternative to SIFT.
- **ORB (Oriented FAST and Rotated BRIEF):** A free, efficient, and computationally fast alternative to SIFT/SURF.
- **HOG (Histogram of Oriented Gradients):** Used primarily for object detection, particularly pedestrian detection.
- **LBP (Local Binary Patterns):** Excellent for texture analysis and face recognition.

**Common Applications:**

- **Image Stitching:** Matching features between images to align them.
- **Object Recognition:** Identifying objects regardless of their orientation or size.
- **Tracking:** Following a feature across frames.
- **3D Reconstruction:** Building 3D models from 2D images.

---
