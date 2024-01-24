# Gaze Estimation

- Three ways (or problems) related to gaze estimation
    - Gaze Following
    - Point of Regard (POG) Estimation
    - 3D Gaze Estimation
- Focusing in the third problem, we have two types of methods
    - Model-based methods try to model the whole eye mechanism to estimate the eye gaze. Requirement for high image quality
    - Appearance-based methods just model an approximation using any image quality input image. In this context, we find deep learning methods

- Deep Learning methods include
    - eye based 
    - semantic information based
    - face based

- Eye based
    - you can use only one eye to model the gaze
    - input one eye, then output a gaze vector
    - usually is also included the head pose information (as a vector) because in different head poses, our eyes will have different shapes

- Semantic information based
    - sometimes not every information is useful for estimating the gaze. And some information could be harming our model. e.g: white points in the eyes
    - semantic information is enough is these cases, and we can predict information with a simplified version of our eye.

- Face based
    - input: whole face -> output: gaze vector
    - similarly to eye based, the head pose information can help to estimate the gaze.
    - however, we should be aware that if we introduce more information on the input more risk of overfitting.

- Why is hard
    - Data collection is infeasible, additional equipment is needed
    - There are different ways to collect the data, but everyone has it's own challenges
        - cameras + screen: limited head pose
        - eyes tracker: need to remove the tracker iamges
        - eye synthesis: not real, lack of real details of eyes.
    - Another project is cross subject, which is a mechanism that everyone has in the eyes and help us to define our gaze. Nonetheless the nodal point N and fovea position are different regarding different people and invisible in images
    - There are three different approaches to deal with these problems, and are:
        - Differentail approach
        - Mixed approach
        - Finetune approch

    - Another problem is the domain problem that is present in every image accoding to natural or physical conditions of the image or person in the image

- Where thrend is it?
    - Unsupervised learning
    - Leverage other information in images
    - Add time dimension to predict gaze
    - Combine model-based methods with deep learning