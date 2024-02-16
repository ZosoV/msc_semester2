# Week 03: Registration
Image registration is a process in computer vision and image processing that involves aligning two or more images of the same scene. 

- These images might be taken 
    - at different times,
    - from different viewpoints,
    - by different sensors,
    - from the same individual,
    - or a group from different individuals. 
- **Goal**: The goal of image registration is to spatially align these images so that they are in the same coordinate system, allowing for a direct comparison or combination of the images. To do that, we are trying to discover the transformation $T$ that maps a source image to a target image.
$$\text{source I} \xrightarrow{\overset{T}{}} \text{target J}$$
$$T = \underset{p}{\text{argmin}} \sum_k \text{sim}(I(x_k),J(T_p(x_k)), \quad \quad \text{where each k is a pixel}$$

- **Minimizing the dissimilarity**: Although **sim** (metric) is technically measuring dissimilarity, the process of minimizing these measures during the registration process is aimed at maximizing the actual similarity
    - In other words, we are minimizing the difference between the source and target image.

## Registration Keypoints:
The process typically involves different things to consider:

0. Feature Detection: Identifying key points or features within the images that can be used for matching. These features should be detectable in all the images to be registered.
    - This can be done with methods explained in previous classes.

1. **Feature Matching**: Associating the detected features in one image with their counterparts in the other image(s). 
    - This can be done by complex algorithm automatically or manually.
    - Possible features are:
        - Landmark / control points
        - Image values
        - Features images detected with other algorithms (e.g. edges, corners)
        - Even you can create features from features (e.g. line intersections)
        - Combination of the above

2. **Transformations**: Determining the type of spatial transformation that needs to be applied to align the images. Common models include:
    - rigid: non-deformative (translation and rotation)
        - can be represented as matrix multiplication
    - affine: semi-deformative or semi-rigid (includes translation, rotation, scaling and shearing)
        - can be represented as matrix multiplication
    - piecewise affine: applying different affine transformations to different components of the image.
    - non-rigid (elastic or deformable transformations)
        - it is based on points and physics models.

3. **Transform Evaluation:**: Establish a similarity criterion to compare the quality of the transformation.
    - Mean Square Difference (MSD): simplest, but inefficient when dealing with highly different intensities
    - Mutual Information: more efficient when dealing with different intensities values,
        - Use the joint similarity to maximize the mutual information
        - Join Similarity: based on a joint histogram (which defines a joint probability) between the intensities of both images.
            - poor alignments are reflected in the joint histogram as zones with high variability
            - good aligments are reflected in the joint histogram as sharpest zones with less variability.
    - Normalised cross-correlation: TODO review

3. **Transform Model Estimation**: Search algorithm to find minimum T.
    - In `skimage`, we use `transform.estimate_transform`.

4. **Interpolation method**: Applying the determined transformation to the images to align them. This step often involves interpolating the pixel values in the images to new locations according to the transformation model.

## MSE, MI and NCC
- **MSE** is excellent for exact pixel-by-pixel comparison but is sensitive to intensity and exposure variations.
- **Mutual Information** is robust against intensity changes and captures information about the distribution of intensities, indirectly reflecting some spatial information due to the nature of joint distributions.
- **Normalized Cross-Correlation** focuses on the similarity of patterns and structures across images, considering both the arrangement and the normalized intensity values of pixels, making it effective for comparing images that may have undergone intensity or exposure shifts.
- **NOTE**:** For more detailed explanations check [ChatGPT chat](https://chat.openai.com/share/611cf408-7462-4661-ad29-9cefbf2700eb)

## Extra Takeaways
- There is a good diagram at the end of the slides that shows how the algorithms should work for estimating the $T$

- **Mutual information** is a concept from information theory that measures the amount of information obtained about one random variable through observing another random variable. Essentially, it quantifies the mutual dependence between the two variables, indicating how much knowing the value of one variable reduces uncertainty about the other, and viceversa.
