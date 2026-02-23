Image enhancement in image processing involves modifying digital images to improve their visual quality, contrast, or, for specific applications, to highlight crucial features for better human interpretation or machine analysis. It acts as a preprocessing step to remove noise, sharpen edges, or adjust intensity levels, without increasing the inherent information content. 
Key Image Enhancement Techniques
Spatial Domain Methods: These techniques directly manipulate pixel values within the image’s coordinate system.
Contrast Stretching & Adjustment: Redistributes pixel values to improve contrast.
Histogram Equalization: Spreads out intensity values to enhance image contrast, making it a commonly used, effective method.
Spatial Filtering (Smoothing & Sharpening): Reduces noise (e.g., mean/Gaussian filters) or enhances edges, making them crisper.
Intensity Transformations: Includes logical, power-law, and log transformations to brighten or highlight specific gray-level ranges.
Frequency Domain Methods: These methods modify the image's Fourier transform to enhance, such as with low-pass (blurring) or high-pass (sharpening) filters. 
Common Applications
Noise Removal: Cleaning up images to make details clearer.
Feature Extraction: Enhancing specific details for, e.g., medical imaging, satellite, or computer vision tasks.
Image Preprocessing: Preparing images for segmentation, recognition, or further analysis, often improving performance.
Brightness/Saturation Correction: Balancing the visual quality of an image. 
Difference from Restoration
Unlike image restoration, which attempts to reverse known degradation (e.g., blur, sensor noise) to reconstruct a "true" image, image enhancement is generally a subjective process intended to produce a more visually appealing or useful result for a specific, often subjective, need.

Image smoothing is a fundamental image processing technique used to reduce noise, remove unwanted artifacts, and blur images by suppressing high-frequency components (sharp edges and fine details). It works by applying low-pass filters in the spatial or frequency domain, where each pixel is replaced with a weighted average of its neighbors, enhancing visual quality and aiding image segmentation. 
Key Concepts in Image Smoothing
Goal: To remove noise and create a smoother, less pixelated image.
Mechanism: Typically, a kernel (mask) moves across the image, computing a new pixel value based on the surrounding pixels.
Side Effects: While effective at removing noise, aggressive smoothing can result in a loss of, or blurry, important image edges. 
Common Smoothing Techniques
Mean Filtering (Average Blurring): Replaces each pixel with the average value of its neighborhood (e.g., in a or kernel).
Gaussian Smoothing: Uses a kernel based on the Gaussian distribution (bell curve), providing a more natural smoothing effect by giving more weight to closer pixels.
Median Filtering: A non-linear filter that replaces a pixel with the median value of its neighborhood, which is highly effective at removing "salt-and-pepper" noise.
Bilateral Filtering: An advanced technique that reduces noise while preserving edges by considering both pixel proximity and pixel intensity differences. 
Applications
Image smoothing is essential for:
Noise Reduction: Cleaning up speckled or grainy images.
Preprocessing: Preparing images for segmentation or object recognition.
Blurring/Softening: Removing fine, irrelevant details. 
Spatial vs. Frequency Domain
Spatial Domain Filtering: Direct operation on image pixels (e.g., convolution with a blur kernel).
Frequency Domain Filtering: Transforming the image (e.g., via Fourier Transform) to the frequency domain to attenuate high frequencies, then transforming back.

Thresholding is a fundamental image segmentation technique that converts grayscale images into binary (black and white) images by separating pixels into foreground and background based on a specific intensity value. Pixels above the threshold become white (
), while those below become black (), crucial for object detection, binarization, and noise reduction. 
Key Concepts and Types
Simple (Global) Thresholding: A single, fixed threshold value () is applied to the entire image. If , it is assigned the maximum value (foreground); otherwise, it becomes (background).
Adaptive (Local) Thresholding: The threshold is calculated for smaller regions of the image, allowing for better handling of varying lighting conditions and uneven illumination.
Otsu's Method: An automatic thresholding technique that finds the optimal value by maximizing the variance between foreground and background pixels, ideal when the image histogram has two distinct peaks. 
Applications
Image Segmentation: Separating objects from the background.
Optical Character Recognition (OCR): Converting scanned text documents into binary for character identification.
Medical Imaging: Segmenting organs or tumors in scans. 
Limitations
Simple thresholding struggles with images that have low contrast, noise, or uneven lighting, often requiring advanced adaptive techniques to achieve good results. 
