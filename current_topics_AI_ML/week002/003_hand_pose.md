# Hand Pose Estimation

## Types

- **Depth-based**: Utilizes as input depth maps for 3D information. Methods are either discriminative (localizing joints directly) or generative (creating models from depth maps). Techniques involve transforming depth images to point clouds or 3D voxelized maps, using 3D CNNs for joint localization.
- **RGB-based**: Utilizes as input standard RGB images. Challenges include dataset generation and dealing with various orientations and lighting. Some methods reconstruct depth maps from RGB images.
- **Hybrid**.
- Two types of networks to tackle these problems
    - Detection-based methods produce a probability density map for each joint.
    - Regression-based methods directly estimate the position of each joint. There are two ways to represent pose: root-relative or UV+depth
        - root-relative (more popular)
        - UV+depth: process of projecting a 2D (u and v represent the 2D axis) mapping to a 3D


## 2. Hand Shape
- Goes beyond pose estimation to include hand shape. Uses graph CNNs, MANO parameter estimation, and neural rendering. Challenges lie in mesh generation and dataset limitations.

### Hand Model - MANO
- MANO (Model for Articulated Neural Operations) is a key hand model. *It generates a mesh from pose and shape vectors*. Limitations include the need for ground truth meshes, limited expressiveness, and inability to account for soft tissue deformation.

## 3. Hand and Object
- Focuses on hand-object interactions. Methods like HOPE-Net understand these interactions. The field needs more specific datasets and exploration of the temporal aspects.

## 4. Datasets
- Includes various real and synthetic datasets like FreiHand, ICVL, NYU, and BigHand2.2M. Challenges involve dataset generalization and the costly nature of data collection for hand-object interactions.
- Doesn't generalize well to other datasets
- STB is not a reliable measure for how a method generalizes to unseen data.

## 5. Open problems/Future work
- Future research areas include improving 
    - graph-based methods
    - personalized hand models
    - dense hand shape estimation
    - handling interacting hands
    - handling temporal reasoning.

## Key Points Table

| Topic                | Key Points                                                                                   |
|----------------------|-----------------------------------------------------------------------------------------------|
| Depth-based          | Uses 3D information, discriminative and generative methods, 3D CNNs, point clouds.             |
| RGB-based            | Relies on RGB images, challenges in dataset generation and handling various conditions.       |
| Hand Shape           | Includes both pose and shape, use of graph CNNs, MANO parameters, challenges in mesh quality. |
| Hand Model - MANO    | Inputs pose and shape vectors, outputs mesh, trained on hand meshes, has expressiveness limits.|
| Hand and Object      | Interaction studies, HOPE-Net, need for specific datasets, temporal aspect exploration.        |
| Datasets             | Variety of real and synthetic datasets, generalization and data collection challenges.         |
| Open problems/Future | Graph methods, personalization, dense shapes, interacting hands, temporal reasoning.           |
