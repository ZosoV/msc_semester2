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

- PHT is 

- By using probabilistic techniques, they reduce the computation complexity while speeding the process without losing much accuracy.
- If multiple points in the image are collinear then their sinusoids in parameter space 
will cross.




- It tries to extend these lines by adding adjacent edge pixels that align with the detected line's orientatioN