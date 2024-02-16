# Week 03: Registration
Image registration is a process in computer vision and image processing that involves aligning two or more images of the same scene. 

- These images might be taken at different times, from different viewpoints, or by different sensors. 
- **Goal**: The goal of image registration is to spatially align these images so that they are in the same coordinate system, allowing for a direct comparison or combination of the images. To do that, we are trying to discover the transformation $T$ that maps a source image to a target image.

$$\text{source I} \xrightarrow{\overset{T}{}} \text{target J}$$

$$T = \underset{p}{\text{argmin}} \sum_k \text{sim}(I(x_k),J(T_p(x_k))$$
,where each k is a pixel

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
    - affine: semi-deformative (includes translation, rotation, scaling and shearing)
    - piecewise affine: applying affines to different components of the image.
    - and non-rigid (elastic or deformable transformations), based on points and physics models.

3. **Transform Evaluation:**: Establish a similarity criterion to compare the quality of the transformation.
    - Mean Square Difference (MSD): simplest but inefficient when deal with highly different intensities
    - Join Similarity: based on a joint histogram (which defines a joint probability) between the intensities of both images.
    - Mutual Information:
        - Use the joint similarity too.
    - Normalised cross-correlation: TODO review

3. **Transform Model Estimation**: Search algorithm to find minimum T.

4. **Interpolation method**: Applying the determined transformation to the images to align them. This step often involves interpolating the pixel values in the images to new locations according to the transformation model.