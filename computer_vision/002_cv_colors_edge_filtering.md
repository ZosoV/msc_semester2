# Human Vision: Colors and Edge Detection

### 1. Human Vision: Color
- **Color Perception**: Humans perceive colors through electromagnetic radiation with wavelengths between 380-760nm. This spectrum is visible to the human eye.
- **Color Mixing Theory (Trichromatic Coding)**: This theory, proposed by Young, suggests that the eye has three types of receptors (cones), each sensitive to one of three primary colors (red, green, blue). This theory explains how we discriminate different wavelengths, match colors, and understand some types of color blindness.
    - Black absorves all the colors, then no light coding 0.
    - White reflect all the colors, then full light coding 255.
    - **Drawback:** This theory doesn't account for colour blending, which consists in creating an area between two colors, where they gradually mix.
- **Opponent Process Coding**: Proposed by Hering, this theory introduces the concept of 'opponent colors' (Yellow-Blue, Red-Green). It explains why certain color combinations (like reddish-green or bluish-yellow) are impossible to perceive and how certain colors blend while others do not.
    - It based on the idea that the ganglion cells perceive two opposive colors (which cannot be signal at the same time).
        - Yellow-blue ganglions doesn't allow to perceive a bluish-yellow.

### 2. Edge Detection
- **Intensity in Images**: The concept of intensity in images relates to the brightness or darkness **of each pixel** in a matrix that represents the image.
    - RGB images are encoded in a matrix with 3-dimension (width, height, and channels).
- **Intensity Gradients**: The idea of s 


- **Sobel Filter**: The Sobel filter is used to detect edges in images. It works by highlighting regions with high intensity gradients, indicating a change in color or brightness.
- **Convolution**: This process involves overlaying a matrix (filter) onto an image and computing a sum of the product of overlapping elements, crucial for detecting edges and gradients.
- **Linear Filtering Algorithm**: This algorithm is used to enhance images by emphasizing certain features like edges. It's a key component in edge detection processes.

### 3. Noise Filtering
- **Mean Filter**: This filter smoothens an image by averaging the pixels within a neighborhood, reducing noise but also blurring edges.
- **Gaussian Filter**: A more sophisticated filter that gives more weight to the central pixels in the averaging process. It's effective in noise reduction while preserving edges better than the mean filter.

### 4. Laplacian Operator (for Edge Filtering)
- The Laplacian operator is used to find areas of rapid intensity change (edges) in images. It's a second-order derivative operator, making it more sensitive to noise compared to first-order methods like the Sobel filter.

### Summary Table

| Topic                  | Key Points                                                        |
|------------------------|-------------------------------------------------------------------|
| Human Vision: Color    | - Electromagnetic spectrum (380-760nm) visibility                 |
|                        | - Trichromatic Theory: RGB color receptors                        |
|                        | - Opponent Process Coding: Incompatible color combinations        |
| Edge Detection         | - Intensity and gradients in images                               |
|                        | - Sobel Filter: Highlighting intensity gradients                  |
|                        | - Convolution: Overlaying a matrix to compute sums                 |
|                        | - Linear Filtering Algorithm: Enhancing image features             |
| Noise Filtering        | - Mean Filter: Averaging pixels, reduces noise, blurs edges        |
|                        | - Gaussian Filter: Weighted averaging, better edge preservation   |
| Laplacian Operator     | - Second-order derivative for finding rapid intensity changes     |

