# Human Body Pose Estimation
It is the estimation of body joins of a person from an image.
- The body joins can be 2D or 3D and corresponds to different parts of the body.
- It can be performed in a single person or multiple persons.
- Challenges include
    - various appearances and low-resolutions
    - diverse human poses and viewa
    - occluded or invisible key points
    - crowded background
- There are two approaches: Top-down vs Bottom-up.

## Top-down methods
- These methods involve human detection followed by single person key points detection.  
- A rough bounding box is given, providing scale and location for each joint.
- Pros: State-of-the-art accuracy
- Cons: Lower speed, dependent on human detection accuracy.
- 6 papers were shown. Relevant notes:
    - Deep High-Resolution: they proposed a network, which remains with higher resolution through the whole process. They do that by connecting multiple subnetworks in parallel (the subnetworks are high to low), but they share information over and over leading to high resolution representations.

## Botton-down methods

- These methods focus on detecting key points and synthesizing human bodies without prior detections. 
- Challenges include scale and number estimation, but keypoint estimates can be used to improve detections.
- Pros: Higher speed, does not rely on human detection.
- Cons: Lower accuracy.
- 6 papers were shown. Relevant: 
    - OpenPose: it consists of different steps:
        1. estimates part confidence maps, that show where a possible body join is
        2. estimates part affinity field, which roughly speaking estimates the connections (extremities of the body).
        3. match the possible join and connections with a process known as bipartie matching.


| Aspect                 | Top-down Methods                                                                           | Bottom-up Methods                                                                           |
|------------------------|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| Approach               | Human detection + Single person key points detection                                       | Detecting key points + Synthesizing human bodies                                            |
| Key Features           | Scale, One location per joint                                                              | No initial idea of scale or number, Key point estimates to improve detections               |
| Research Highlights    | 6 papers including "Stacked hourglass networks" and "HRNet"                                | 6 papers including "Realtime Multi-person 2D Pose Estimation" and "PifPaf"                  |
| Advantages & Disadvantages | Pros: High accuracy. Cons: Slower, depends on human detection accuracy | Pros: Faster, independent of human detection. Cons: Lower accuracy                          |