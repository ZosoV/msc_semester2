# Week 2.3: Motion

- Vision is inferential, which means that **experience (pior knowledge)** plays a big deal in how analyze the data that you have and what you deduce from it.
- The notion of motion can be used to solve different issues such as:
    - tracking
    - optical flow
    - video mosaics -> panoramic photos
    - video compression

## Classical and Deep Learning Approach

- The fundamental classical approach is:
    1. Initially, the focus was indeed on extracting meaningful edges and contours from images through filters (like Sobel, Canny). 
    2. Subsequently, algorithms (such as Harris Corner Detector, SIFT, and SURF) were applied to these filtered images to detect and describe features that are invariant to changes in scale, rotation, or illumination.
    3. These features could then be used for various applications, including motion capture, object recognition, and scene reconstruction.
- Other possible classical approaches directly apply feature detection algorithms on images without the preliminary requirement for edge filtering, as many feature detectors inherently analyze changes in intensity and spatial relationships to identify features. 
- Lastly, modern approaches often leverage machine learning and deep learning, which can directly learn feature representations from raw pixel data without explicit filtering or feature extraction steps.

## Basic Motion

The basic knowledge consists of a simple difference between two consecutive frames. It can be used for optical flow issues.

Process:
1. Apply an edge detector
2. Select a feature (described by a white box representing that feature in the image).
3. Detect movement by subtracting two images of different consecutive frames.
$$D P_{12}(x, y)= \begin{cases}1 & \text { if }|F(x, y, 1)-F(x, y, 2)|>\tau \\ 0 & \text { otherwise }\end{cases}$$
where $F(x,y,i)$ is the intensity of the image at time i, at point x,y

- **Drawback 1 (Random Noise)**: There could be problems with `random` noise because not always is possible to eliminate all the noise in an image.
    - The noise is practically found in the binarized image.
    - Common solution like threshold and noise filter doesn't work.
        - threshold could eliminate important frequencies of the feature of interest.
        - noise filter doesn't eliminate all the noise
    - **Solution**: take into account the **connectedness** between pixel.

### Connectedness
The idea is to get rid of isolated pixels that can be noised. It makes sense because our feature of interest will consists of a group of pixels (not isolated pixels).

There are different ways to account connectedness in a binarized image. The next are three options
- Two pixels are 4-neighbours if they share a common boundary
- Two pixels are 8-neighbours if they share at least a common corner
- Two pixels are 8 connected if we can create a path of 8-neighbours from one to the other. 
    - The two pixels are not immediately connected

Process:
1. Analyze a pair of pixels (p1 and p2)
2. Check if the pixels are connected (in any way 4-neighbours, 8-neighbours, 8 connected path).
    - You can use any of those methods.
3. Pixels not in a **connected cluster** of a certain size (defined beforehand) are removed from the difference image.


- **Drawback 2 (Aperture Problem)** There is not enough information on the **local intensity** changes 
in an image to determine the motion.
    - For example with an edge, **locally** we only see the horizontal component of the motion.
    - We need something more informative than edges.
    - **Solution**: take into account corner points using a corner detector, such as **Moravec Operator**.

# Advance Motion: Moravec Operator and Motion Correspondance

## Moravec Operator
The Moravec operator defines corner points as points where there is a large intensity change in every direction.
    - Notice it makes sense because, in the corner, it is possible to find intensity in both vertical and horizontal directions.
    - However, it is sensitive to isolated pixels because you could get even more intensity variations (in all directions) on those pixels. Then, it's important to reduce the noise.

Process:
1. Define an operator size (3x3, 5x5, 7x7 pixels)
2. Center two operator (static $A$ and shifted $B$) in each non-zero pixel
3. Move the shifted operator in every possible direction.
    - Measure the intensity change by $V=\sum_{i=1}^9\left(A_i-B_i\right)^2$
4. Repeat the process for every non-zero pixel
5. Filter to only consider intensity changes greater than a threshold value.
    - Or by keeping the local maxima if there are closed corners.

## Motion Correspondance
Once we have the corners, we are interested in getting the best possible pair combination that gives us the motion.
    - This is achieved by matching the corners from the first and second frames by a similarity function, and consequently a probability of matching.
    - There are three principles for matching in motion correspondence: Discreteness, similarity and consistency.

Process:
1. Get the interest points in each image (Moravec Operator)
2. Pair each feature point in the first image **with every feature point in the other image** within some distance.
3. Calculate the degree of similarity between the images for each possible match, using $w_{i j}=\frac{1}{1+\alpha s_{i j}}$
4. Normalize the previous weights to get the likelihood of each match.
    - It provides for each corner $i$ in frame 1, a set of probabilities of matching with each corner j of the frame 2.
    $$4(t) = [0.89, 0.04, 0.04, 0.03] \text{ match of corner 4 in frame 1 and all the other corners in frame 2}$$
5. Now revise the match likelihood for each point using the nearby matches

Given two corners from frame 1: i and for frame 2 j, we can calculate the **similarity** weight as follows
1. super-impose (or center) the corner j in the same position of the corner i.
2. count the pixels that don't overlap after superimposing. 
    - This count is $s_{ij}$, which provides a kind of notion of dissimilarity
3. Then, the weights provide a notion of similarity because it's the reciprocal of $s_{ij}$
$$w_{i j}=\frac{1}{1+\alpha s_{i j}}$$

**Extra Takeaways**
- It's need to adjust the equations to handle rotation situations
- It could work with multiple features from frame 1 and frame 2.
- Voxel is the smallest distinct unit for an image in 3D image space. In the same way as a pixel is the smallest unit for a 2D image.

## Question for me

1. What is a Fourier Transform? 