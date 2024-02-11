# Week 04.1: Hough Transform

## Standard Hough Transform

In a nutshell, the Hough Transform allows us to detect lines in an image by analyzing the different lines that pass through each edge pixel and taking out the most voted lines from different pixels.

Particularly, the process is as follows:

1. Apply an edge filter algorithm (e.g. Canny operator) because (HT) works on a binarized image.
    - the edge pixels are those non-zero pixels that form the edges of the binarized image.
2. Multiple lines can pass through each edge pixel. To define each of these lines, we represent the lines in polar coordinates $(w,\theta)$, where
    - $w$ is the distance from the origin to the closest point to the line (forming a perpendicular angle wrt to the line).
    - $\theta$ is the angle that the distance $w$ makes wrt to the x-axis.
    - In this process, we are practically mapping each edge pixel to different lines $(w,\theta)$, which live in a parameter space (Hough Space $M \times N$), where $M$ corresponds to different values of distances $w$ and $N$ different values of angles $\theta$.
3. **Voting Process**: Note that we can get the same lines from different pixels. Those lines are more possible actual lines in the original space
    - Then, for each edge pixel, several lines are computed and voted in an accumulator matrix $A$ ($M \times N$), representing possible values of ($w$,$\theta$). $$\text{per each pixel, } (x,y)\text{ we have } \theta \text{ and get } w = x \text{cos}(\theta) + y \text{sin}(\theta)$$
    - Notice the multiple votes for the same line are evidenced in the Hough Space as an interception.
4. **Filter Top Lines**: Using a threshold we can filter the highest voted lines (also called peaks).
    - Notice you can also ask to return the n-th top-voted lines.

Using `skimage.transform import hough_line, hough_line_peaks`
- The function `hough_line` performs the voting process.
- The function `hough_line_peaks` performs the filtering top lines process.

**Other Takeaways**
- The lines corresponding to a particular edge pixel form a sinusoidal curve in the Hough Space. In other words, one in image space corresponds to a sinusoidal curve in hough space.
    - Then, the multiple votes for the same line are evidenced in the Hough Space as an interception of these sinusoidal curves.
- Instead of saving several lines per each pixel, the algorithm uses an accumulator matrix $A$ that represents all the possible pairs $(w, \theta)$, so that we only need to iterate through this matrix filling the votes that each pixel provides to each line.
- In theory, we could use the algorithm with different shapes. There are generalised version for ellipses and circles. (e.g. in circles the space parameter would be  3-dimensional $(a,b,R)$)
- During the algorithm, can be also applied a non-local maxima suppression to get a more straight line.
- The algorithm will still fail in the face of certain textures.

**What is the effect of applying different edge detectors?**

- I evaluated different edge detectors canny, laplacian of gaussian, sobel, roberts, and prewitt. The best results are obtained by using canny and laplacian of gaussian. It is because they allow a better localization of the edges by returning thinner edges which are easier to recognize than ticker edges produced by sobel, rober, or prewitt.
- The problem with thicker edges is that the hough transform defines several lines in an enclosed space around each edge pixel, which makes it difficult to distinguish between actual lines. In other words, multiple lines in a confined space around an edge pixel will produce a lot of votes to lines with only small variations of angle. Consequently,  by only taking the higher voted lines, it’s more difficult to distinguish the actual lines.


## Probabilistic Hough Transform (PHT)
The Probabilistic Hough Transform aims to reduce the computation complexity while speeding the process without losing much accuracy.

The idea is that by using a subset of the edge pixels, it is still possible to return a good approximation of the actual results. There are two ways to achieve that PHT and RHT.

1. Probabilistic Hough Transform (PHT) uses a random subsample of the pixel edges of size $k$, where the minimum $k$ used is well-defined for some tasks. Then, the same algorithm as before is executed but now uses this subset of pixel edges.
2. Randomized Hough Transform (RHT) uses two random sampling edge pixels $p_1$, $p_2$ (extracted from the big set of edge pixels), and look through the rest of the edge pixels that pass through the line defined by $p_1$ and $p_2. 
    - The line that passes through $p_1$ and $p_2$ is defined by $(m,b)$, where $m$ is the slope and $b$ the intercept.
    - This is other way to perform the algorithm, which only needs to save a list of lines by $(m,b)$.
    - This also needs to define a tolerance because there can be points that don't pass exactly through the line, but are close enough to be part of that line.
    - This process is repeated by sampling several times 2 points.

Both methods allow us to reduce the computational complexity, and still get good approximated results. However, they still are only finding lines and not proper segments.

### Progressive Probabilistic Hough Transform (PPHT)

PPHT allows us to find segments by including an additional process where lines can be extracted during the voting process by walking along connected components, instead of iterating to every possible edge pixel.

- In order to extend these lines, the algorithm adds adjacent edge pixels that align with the detected line's orientation (e.g. by using the direction of the gradient).
- It additionally considers some hyperparameters to control the merging process, such as a minimum line length and/or a line gap that influences the line merging.