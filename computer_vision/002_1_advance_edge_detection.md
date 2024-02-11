# Week 02: Advance Edge Detection

- **What can cause intensities changes?** There can be different reasons based on geometric or non-geometric events.
    - Based on the application, it's worth it to think about the possible reason.
- **Usefulnesss of Edge Detection** It allows us to discern important features in the image (e.g. corners, lines, curves), which can be later used in higher-level computer vision algorithms (recognition, tracking, etc)
- **Edge Descriptors**: Edges are described by 
    - their direction (perpendicular to the direction of maximum intensity change), 
    - strength (related to local image contrast - magnitude), 
    - and position (the specific location in the image).
- Main Steps in Edge Detection
    1. Smoothing (Noise Filtering)
    2. Enhancement (Gradient Calculations 1st or 2nd order)
    3. Thresholding (Applying in some cases)
    4. Localization (determine exact location). It the process of distinguish an edge, while more thinner better localization.
- **Gaussian Derivation trick** helps us to save one operation by taking the derivative of the Gaussian filter. Then, instead of applying gaussian filter + edge filter, we apply first the edge filter to the gaussian filter, and with that result built the solution.
    - Practically, the **derivative of the Gaussian** is applying the Edge filter to the Gaussian Filter
    - Depending on the method used we have different results:
        - Using Laplacian (2nd order derivative), we have: $I \circledast LoG \rightarrow \text{0-crossing}$
        - Using Sobel (1st order derivative), we have:
            - $S_x \circledast G = \text{Derivative Gauss}_x$
            - $S_y \circledast G = \text{Derivative Gauss}_y$
            - $I = \sqrt{\text{Derivative Gauss}_x^2 + \text{Derivative Gauss}_y^2}$
- Edge Detection steps using gradient in slides
    - **NOTE:** For computational efficiency, it's preferred to use absolute values to approximate the magnitude.
- Practical Issues:
    1. **Noise suppression-localization tradeoff**
        - More kernel size (or std in Gaussian Filter) => more smoother (blur) image => No thinner edges (worse localization)
    2. **Threshold choice**
        - Too much threshold => suppress important edges => bad localization
        - Too low threshold => thicker edges => bad localization
    - Criteria for Optimal Edge Detection
        - Good Detection (minimize false positive and false negatives)
        - Good Localization => thin edges
        - Single Response

## Canny Edge Detector
This advance edge detector assume the noise distribution is Gaussian. Then, the process consits in
1. Get the derivative of the gaussian using any 1st order derivative method (Sobel)
    - Apply the derivative of the gaussian x and y to the image
2. Compute the magnitude using absolute val
3. Compute direction 
4. Apply non-maxima suppression (using the gradient direction).
5. Apply hysteresis thresholding/edge linking

### Non-Maxima Suppression
In the direction of the gradient check if the current pixel location is a local maximum or not. If it is a local maximum, we keep the pixel.
- In the direction of the gradient, we will have prev_pixel -> current_pixel -> next_pixel. If the current pixel is greater than prev and next, then we keep it, otherwise 0.

### Hysteresis thresholding
It is a process that consists of using two thresholds a high and low threshold. Normally, the high threshold is the double of the low threshold.

- Process: 
    1. If the pixels are greater than the high threshold, mark them as an edge (strong edge)
    2. If the pixels are between the low and high threshold, mark them as a maybe (maybe edge)
    3. Starting from the strong edges, check proximal pixels in the direction of the gradient, and if the pixel is a maybe pixel.
        - mark it as an edge, if the neighbors are edges,
        - repeat the process until you don't find more edge neighbors.
    - Notice you always keep the direction of the gradient to analyze each pixel.

## Questions to ask

1. In LoG, do we convolve L over G or G over L?