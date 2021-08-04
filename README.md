# Paper

---

[TOC]

## 一. Image Matching

### 0. Survey, Benchmark and Dataset

#### Survey

- Local Invariant Feature Detectors: A Survey 【2007】

#### Benchmark

- Benchmarking 6DOF Outdoor Visual Localization in Changing Conditions. 【2018】
- Inloc: Indoor Visual Localization with Dense Matching and View Synthesis. 【2018】

#### Dataset

##### Image Matching

- HPatch dataset

  116个序列中使用108个序列，每个序列有6个图片。每个序列使用第一个匹配其他剩下5个，得到108*5=540个图像对。

  - Evaluation protocol
    - MMA (Mean Matching Accuracy)

##### Long-Term Visual Localization

- Aachen Day-Night dataset
- RobotCar Seasons dataset
- InLoc dataset [challenging]





### 1. Dense-to-Dense

carry high computational cost and memory consumption which make them hardly scalable for computer vision applications.

- Neighbourhood Consensus Networks. 【2018】

  trains a CNN to search in the 4D space of all possible correspondences, with the use of 4D convolutions.





### 2. Sparse-to-Dense

perform the detection stage asymmetrically. under strong visual changes, the need for repeatability in keypoint detection is alleviated, allowing each pixel to be a detection.

-  Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization. 【2019】
- S2DNet: Learning Accurate Correspondences for Sparse-to-Dense Feature Matching. 【2020】

### 3. Sparse-to-Sparse

#### (1) Local Feature Detection: not descriptor-specific

##### a. handcraft

- Brisk: Binary robust invariant scalable keypoints. 【2011】
- Kaze features【2012，ECCV】
- In the saddle: chasing fast and repeatable features. 【2016】

##### b. learned

- Tilde: a temporally invariant learned detector. 【2015】

  trains a piece-wise linear regression model as the detector, that is robust to weather and illumination changes.

- Learning covariant feature detectors. 【2016】

  CNN models are trained with feature covariant constraints

- Learning discriminative and transformation covariant local feature detectors.【2017】

  CNN models are trained with feature covariant constraints

- Quad-networks: unsupervised learning to rank for interest point detection 【2017】

  assumes that the ranking of the keypoint scores should be invariant to image transformations.

- Learning to detect features in texture images. 【2018】

- Repeatability is not enough: Learning affine regions via discriminability. 【2018】

  learns to predict the affine parameters of a local feature via the hard negative constant loss based on the descriptors.

- Key.net: Keypoint detection by handcrafted and learned cnn filters. 【2019】

  combines hand-crafted filters with learned ones to extract keypoints at different scale levels.

- ELF: Embedded Localisation of Features in pre-trained CNN 【2019】

  pre-trained CNNs on standard tasks such as classifcation can be adapted to keypoint detection

#### (2) Local Feature Description: independent of the detectors

###### local patch datasets

- Discriminative learning of local image descriptors. 【2011】	
- Hpatches: A benchmark and evaluation of handcrafted and learned local descriptors. 【2017】
- A large dataset for improving patch matching. 【2018】

##### a. handcraft: histograms of local gradients

- Distinctive Image Features from Scale-Invariant Keypoints. 【2004】
- SURF: Speeded Up Robust Features. 【2006】
- BRIEF: Binary Robust Independent Elementary Features. 【2010】
- ORB: An Efficient Alternative to SIFT or SURF. 【2011】

##### b. learned: deep local descriptors

- Discriminative learning of deep convolutional feature point descriptors. 【2015】	

- PN-Net: Conjoined Triple Deep Network for Learning Local Image Descriptors. 【2016】

- Learning local feature descriptors with triplets and shallow convolutional neural networks 【2016】

- L2-net: Deep learning of disriminative patch descriptor in euclidean space. 【2017】

- Working hard to know your neighbor’s margins: Local descriptor learning loss. 【2017】

  combines triplet loss with a within-batch hard negative mining that has proven to be remarkably effective

- Learning deep descriptors with scale-aware triplet networks. 【2018】

- Local descriptors optimized for average precision. 【2018】

- Sosnet: Second order similarity regularization for local descriptor learning. 【2019】

  extends HardNet with and second-order loss.

#### (3) Joint Detection and Description

##### a. handcraft

- Distinctive image features from scale-invariant keypoints. 【2004】
- SURF: Speeded Up Robust Features. 【2006】

##### b. learned

- Lift: Learned in variant feature transform. 【2016】

- Superpoint: Self-supervised interest point detection and description. 【2018】【self-supervised】

  leverages two separate decoders for detection and description on a shared encoder.

  Synthetic shapes and image pairs generated from random homographies are used to train the two parts.

  patch cropping is replaced by fully convolutional dense descriptors

- Lf-net: learning local features from images. 【2018】【self-supervised】

- Rf-net: An end-to-end image matching network based on receptive field. 【2019】

- Contextdesc: Local descriptor augmentation with cross-modality context 【2019】

- R2d2: Repeatable and reliable detector and descriptor. 【2019】【self-supervised】

  learning keypoints that are not only repeatable but also reliable together with robust descriptors.

- D2-net: A trainable cnn for joint detection and description of local features. 【2019】

  learning keypoints that are not only repeatable but also reliable together with robust descriptors.

- Aslfeat: Learning local features of accurate shape and localization 【2020】

- Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization. 【2019】

- Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization. 【2019】

- D2D: Keypoint Extraction with Describe to Detect Approach 【2020】

  description-guided detection
