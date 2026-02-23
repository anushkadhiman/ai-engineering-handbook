mage segmentation is a high-precision computer vision technique that partitions an image into discrete groups of pixels called segmentation masks. While object detection uses rectangular "bounding boxes" to locate items, segmentation identifies the exact shape and boundary of every object at the pixel level.
The Three Core Types
Computer vision tasks are typically divided based on how they handle "things" (countable objects like cars) and "stuff" (uncountable regions like sky).
Semantic: Assigns a class label to every pixel (e.g., "road," "sky," "person").	Groups all instances of a class into one "blob." Multiple people are just one "person" segment.
Instance:	Identifies and masks individual objects of interest.	Differentiates between separate objects of the same class (e.g., Person 1 vs. Person 2).
Panoptic:	A hybrid approach that labels every pixel in the scene.	Combines semantic (for "stuff" like sky) and instance (for "things" like cars) for holistic scene understanding.
