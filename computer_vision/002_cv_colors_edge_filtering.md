# Week 01: Human Vision: Colors and Edge Detection

## 1. Human Vision: Color
- **Color Perception**: Humans perceive colors through electromagnetic radiation with wavelengths between 380-760nm. This spectrum is visible to the human eye.
- **Color Mixing Theory (Trichromatic Coding)**: This theory, proposed by Young, suggests that the eye has three types of receptors (cones), each sensitive to one of three primary colors (red, green, blue). This theory explains how we discriminate different wavelengths, match colors, and understand some types of color blindness.
    - Black absorbs all the colors, then no light coding 0.
    - White reflect all the colors, then full light coding 255.
    - **Drawback:** This theory doesn't account for colour blending, which consists in creating an area between two colors, where they gradually mix.
- **Opponent Process Coding**: Proposed by Hering, this theory introduces the concept of 'opponent colors' (Yellow-Blue, Red-Green). It explains why certain color combinations (like reddish-green or bluish-yellow) are impossible to perceive and how certain colors blend while others do not.
    - It is based on the idea that the ganglion cells perceive two opposite colors (which cannot be signal at the same time).
    - Yellow-blue ganglions don't allow to perceive a bluish-yellow.

## 2. Edge Detection
- **Intensity in Images**: The concept of intensity in images relates to the brightness or darkness **of each pixel** in a matrix that represents the image.
    - RGB images are encoded in a matrix with 3-dimension (width, height, and channels).
- **Intensity Gradients** we can detect edges by calculating the intensity change (gradient) across the image 
    - The gradient is a vector that points in the direction of the greatest rate of change of intensity. 
    - Mathematically, it involves derivatives $G_x$​ and $Gy$​, which approximate the gradient in the horizontal and vertical directions, respectively. 
    - The magnitude $M = \sqrt{G_x^2 + G_y^2}$​ and direction $θ=tan^{⁡−1}(\frac{Gy}{Gx})$ help in distinguishing edges.
    - **Kernels** are used to calculate these derivatives. The kernels represent the weights of the closer pixels, and the change calculated between those closer pixels. Then,
        - $G_x = K_x * I$ is gotten by convolving a kernel $K_x$ to the image $I$.
        - $G_y = K_y * I$ in the same way.


### Sobel Filter
- Uses convolution with 3x3 kernels to approximate image intensity gradients, highlighting edges. The kernel are:

$$S_x = \begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix} \quad S_y = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}
$$

- Notice $G_x$ and $G_y$ corresponds to the derivatives after convolving $S_x$ and $S_y$
- **Process**: Convolution (Derivatives x and y) + Magnitude (M) + Threshold

### 3. Noise Filtering
- **Mean Filter**: Averages pixels in a neighborhood, reducing noise but blurring (smoothing) edges.
- **Gaussian Filter**: Applies a Gaussian kernel, reducing noise while preserving edges better than mean filter because it applies a kind of weighted average.
    - Applying the gaussian filter results in a smoother image, consequently, applying an edge detector returns better results.
    - We can replace a 2D Gaussian filter with 2, 1D Gaussian filters in sequence
- **Process:** Only Convolution 

### 4. Laplacian Operator
- The Laplacian operator is used to find areas of rapid intensity change (edges) in images. 
- It's a second-order derivative operator, making it **more sensitive to noise** compared to first-order methods like the Sobel filter.
    - For that reason, commonly a gaussian noise filter is applied before applying laplacian $I \circledast G \circledast L \rightarrow \text{0-crossing}$
    - Laplacian of Gaussian $LoG$ combines the Laplacian and Gaussian by convolving the Laplacian with the Gaussian Filter. $I \circledast LoG \rightarrow \text{0-crossing}$
- In contrast to 1st order operators, laplacian doesn't need threshold.
- It finds the edge by directly seeing the zero-crossing in the second-derivative of the image. In this process, you are finding actually the edge objectively.
    
- **Process**: 
    - Almost never: Convolution (2nd Derivative directly) + zero-crossing
    - $I \circledast G \circledast L \rightarrow \text{0-crossing}$
    - $I \circledast LoG \rightarrow \text{0-crossing}$

### Summary Table

| Topic              | Key Points                                                                                           |
|--------------------|------------------------------------------------------------------------------------------------------|
| Color Perception   | - Trichromatic Coding: Red, Green, Blue receptors. <br> - Opponent Process: Pairs of opposing colors. |
| Edge Detection     | - Gradients measure change in intensity. <br> - Sobel Filter for detecting edges using convolution.   |
| Noise Filtering    | - Mean Filter for basic smoothing. <br> - Gaussian Filter for noise reduction with edge preservation. |
| Laplacian Operator | - Second-order derivative for edge detection. <br> - Sensitive to noise, may blur without pre-filtering. |
