# Cross-domain Image Analysis

- There are several image analysis tasks: classification, segmentation, object detection, 3d reconstruction, image generation, etc.
- **Domain shift**: the different distribution in train (**source**) and test (**target**) data.
    - Normally neural networks work under the assumption that the training and test data are drawn from the same distribution (e.g. camera images, or animate images, which are different domains).
    - But in practice, sometimes to get that data is difficult and we somehow should use data from one different domain to test in data of a different domain. This is a domain shift.
    - **Challenge**: The domain shift issue results in a low generalizability in NN.

- **Forms of Domaint Shift**
    - **Covariance shift:** the changes in the distribution of the input variables
        - e.g. image in sunny vs snowy days
    - **Prior probability shift:** the changes in the distribution of the class variables.
        - e.g. imbalaced data in test
    - **Concept shift:** the changes of the relationship between the input variables and
the class variables.
        - e.g before and after the shopping pattern is different. The relationship changes.

- **How to address domain shift?**
    - Aiming at learning domain-invariant features during training:
        - Domain adaptation or transfer learning in a broader concept
        - Domain invariant features are those features that doesn't change from domain to domain.
    - Aiming at increasing data diversity during training:
        - Data augmentation
    - Aiming at adapting target domain data during test:
        - Test-time adaptation

- Domain Adaption
    - Types: Supervised, semi-supervised, unsupervised
    - Homogenoeous or heterogenous
    - Scenarios: one-to-one, multi-source, multi-target

- Data Augmentation:
    - Basic Augmentation
    - Deformable Augmentation
    - Advanced augmentation (GANs)

- Domain shift is really often in medical image analysis
    1. Different types of images: MRI, Ultrasound, X-Ray, CT and PET.
    2. Images taken from different medical centers can have statistically more difference
    3. Even in the same medical center, the presence of tumors or the methods used could lead to domain shift problems.

# Cross-Domain Ultrasound Classification

- Ultrasounds have some pros and cons.
    - Pros: portable and economical. They use pulse to come up with an image.
    - Cons: not high-quality images
    - Used to diagnose different things: fetal, liver, heart, neck.
- Ultrasound images suffer from Domain shift for multiple reasons like artifacts or different device measures.
- They proposed a cross-device fetal ultrasound classification. 
    - The aim is to learn the domain invariant feature of each category (6 categories).
    - Unsupervised domain adaptation scenario -> makes sense but still the question where we are testing?
    - The architecture consists in a sequence of modules
        1. **Encoder** outputs the latent code representations ($F_s$,$F_t$) of the source and target image
        2. **Gaussian Embedding** by using the source and target latent codes, it returns another latent space. This is a step to make sure that the features of both domains share the same prior distribution.
            - L_rec and L_prior are used to ensure this (similar to what VAE does I think)
        3. **Classifier** intermediate latent codes are fed into a classifier in order to return logits and predict a class for the source and a class for target.
            - L_KL encourages a similar ratio of categories in both domains
            - L_M  and L_H encourage to cluster together images of the same class and move far away images from different classes.
            - L_ce is a normal cross entropy used only for the source image that has labels.
    - This method outperforms others in precision, recall, and F1 but I'm not still sure what they use to test. Because it seems like they are using the same image for testing and training.

- But the things can became more complicated hahaha
    - What would happen if we have a source dataset with some classes and unlabeled data that we know belongs to some of those classes, but we are not sure which class.
    - Or even worse if some of the unlabeled target data actually overlaps some of the labeled data. In other words some class in the labeled data actually should correspond to two different class in the unlabeled data.

- The second model aim is to disentangle the context features from the domain features. Or in other words, to separate the domain features from the context invariant features.
    - the context features are the domain invariant features (or anatomical features as she said)
    - domain features those features which come from the specific distribution

## Cross-domain Medical Image Segmentation#

- Segmenting medical images is time-consuming and complex due to the heterogeneous forms.

- Method 1:
    - It contains two branches.
        - 1. Inputs a source image (and/or target image?) and returns a segmented image
        - 2. Discriminator that tells us if an image belongs to the source or target domain
    - L_adv is the discriminator loss
    - L_seg_Adv is the lost of the first branch, which will try to fool the discriminator
        - it minimizes the segmentation loss L_seg
        - and maximize the L_adv (in order to fool the discriminator)
    - By fooling to the discriminator the first branch is encouraging to learn domain invariant features


- Method 2: Cross-modality image segmentation
    - source MRI and target CT
    - MRI is too much time consuming and expensive
    - CT scans are relatively faster, exposure to radiation.
    

### Questions:

**Cross-domain classification**
- Is this method one-to-one right?

- It is an unsupervised method because they don't have labeled data in the target domain. However, it made me wonder if they are using the labels in the source set, is this method still unsupervised?
- Something, I don't have clearly here. If we use the source and target data during training, do we still need another test set (with similar data from the target domain), right? In order, to have those results we cannot use the same target data used during training, right?

- In the second model, which tries to separate context and domain features. The way how the architecture is built suggests that we can predict the class of an image only by using context features, right?
    - Is that something that always happens?
    - Or is it most like a process to transfer enough invariant domain information to in some way bootstrap the classification training of the other target domain?

**Cross-domain segmentation**

- Why the fooling action lead us to learn domain invariant features? Because we will induce images from the target domain to be represented as image from source domain????