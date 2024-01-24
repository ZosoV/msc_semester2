# Week 02: Quick Notes

## Intro

- The main objective of the research is learning by imitation.
- Research direction: comprehensive understanding of human through vision
    - Eye Gaze
    - Human Body Pose
    - Hand Pose
    - Object Pose
- Estimating the human body pose can be considered as estimating articulating structure.
- **Body Pose**: Recombining **motion** and **skeleton** information together to estimate the body pose.
    - Transfer Knowledge: Match similar kinematic joins by considering the motion characteristic.
    - It can help to learn movement by only recognizing the matching kinematic joins and imitating the movement.
    - Implemented into real robots. The robot learns to move its hand by looking at a person's hand.
    - Motion Retargeting: transfer the movement between avatars of different sizes.
    - Body Pose Sonification: helps people who can not see to climb a wall. They built an assistance in order to provide blind people with the freedom to climb. Includes some skeleton tracking step.
    - Musculosketal Activation Regression: to estimate the neck posture for rehabilitation goals.
- **Hand Pose**: Recognize the motion of the hand is challenging by multiple factors: moves quickly and too much joins
    - Solution: reduce the number of joins to 16 landmarks, which will be our output (16*3 = 48 dimensional vector by three due to the axis x, y, z of each landmark).
    - SeqHAND: how to learn the dynamic movement of a hand? How to use temporal information? They approach the problem by creating a database that is based on synthetic data, and combined with realistic backgrounds. The network is based on ConV-LSTM.
    - Fingerwriting: Recognize the hand-finger writing. You need to track the finger and recognize which character is the finger writing.
    - 3D Fringer CAPE: That tracks the hand, estimates the hand posture, and also detects the click behavior.

- **Eye Gaze**: Detect the point where a person is seeing.
    - nowadays, very expensive tracker glasses are used for accurate eye-tracking.
    - These devices are used to create dataset.
    - Dataset Generation: The proposed another method to create datasets by using motion capture cameras and GANs.
    - Student Attention: estimating the student's attention via Gaze Tracking and the time that the student spends looking to the whiteboard area.
    - CVPR Workshops
- **Interacting Object Pose**: recognize the pose of objects that humans interact with their hands.
    - The task is to estimate the 6D Pose of the object and the body?
    - 6D Pose: 3D rotation + 3D translation (relative to camera coordinate system).
    - PointPoseNet: it only learns with one 3D vector-field representation that accounts for both geometry and localization information. They include a geometry constraint that I don't understand.
    - G2L-Net: with embedding vector features.
    - PRI-AE: strong against oclusions. Instance label object tracking.
    - FS-Net: category level of object tracking
