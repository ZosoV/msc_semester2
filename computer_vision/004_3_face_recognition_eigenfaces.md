# Face Recognition

In this session, we study face recognition, not face detection.

The problem in question is how to match a given face with another group of faces.

The **Eigenface** approach is used in this section. This approach aims to represent the image face of a person in low-dimensional representation given by the projected image face (input $x$) into an eigenspace.
    - The eigenvectors that constitute the eigenspace correspond to specific characteristics of human faces.
    - Then, the recognition of a new face just consists of comparing the low-dimensional representations between the reference image and a pool of images (where you want to search for a match).

Process:
1. Unrolled the images in our dataset in flattened representations. 
    - So that our dataset becomes D with size $(n \times d)$
        - $n$: number of samples
        - $d$: number of features (pixels)
2. Center the data by the mean vector of all the samples.
    - Such that our normalized dataset is X.
3. Calculate the eigenvalues and eigenvector by Singular Value Decomposition of X
    - V $(d\times d)$ contains our eigenvectors
    - D $(n\times d)$ our singular values $sigma_i$. If you want to get the eigenvalues, then you can use $\lambda_i = \frac{\sigma_i^2}{n-1}$
4. Project our original images into the new coordinate system by multiplying $XV$ to get the weights of each images.
    - Notice it's possible to take only the k-top eigenvectors in $V$ for reducing the dimensionality
    - By projecting X (an face image) into the eigenspace, you get a point into this new space that represent the **weight** of the face.
    - By unrolling the principal components (or eigenvectors in V), you can get the representation of the **eigenfaces** that correspond to the features with more variability, useful to distinguish a face from another.


    