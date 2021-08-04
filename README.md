# Image Matching Paper

<a name="Contents"></a>

### :hammer: **目录|Table of Content**

- [Survey, Benchmark and Dataset](#Survey, Benchmark and Dataset)
  - [Survey](#Survey)
  - [Benchmark](#Benchmark)
  - [Dataset](#Dataset)
- [Dense-to-Dense](#Dense-to-Dense)
- [Sparse-to-Dense](#Sparse-to-Dense)
- [Sparse-to-Sparse](#Sparse-to-Sparse)
  - [Local Feature Detection](#Local Feature Detection)
    - [handcraft](#handcraft-detection)
    - [learned](#learned-detection)
  - [Local Feature Description](#Local Feature Description)
    - [handcraft](#handcraft-description)
    - [learned](#learned-description)
  - [Joint Detection and Description](#Joint Detection and Description)
    - [handcraft](#handcraft-d2)
    - [handcraft](#handcraft-d2)





### :key: **关键词** | Keywords

【TODO】



<a name="Survey, Benchmark and Dataset"></a>

## Survey, Benchmark and Dataset

<a name="Survey"></a>

### Survey

:heavy_check_mark: **Local Invariant Feature Detectors: A Survey** 【2007】

<a name="Benchmark"></a>

### Benchmark

:heavy_check_mark: **Benchmarking 6DOF Outdoor Visual Localization in Changing Conditions** 【2018】

:heavy_check_mark: **Inloc: Indoor Visual Localization with Dense Matching and View Synthesis** 【2018】

<a name="Dataset"></a>

### Dataset

- **Image Matching**

:heavy_check_mark: **HPatch dataset**

说明：116个序列中使用108个序列，每个序列有6个图片。每个序列使用第一个匹配其他剩下5个，得到108*5=540个图像对。

Evaluation protocol：
- MMA (Mean Matching Accuracy)

- **Long-Term Visual Localization**

:heavy_check_mark: **Aachen Day-Night dataset**

:heavy_check_mark: **RobotCar Seasons dataset**

:heavy_check_mark: **InLoc dataset** (challenging)

<a name="Dense-to-Dense"></a>

[返回目录](#Contents)



## Dense-to-Dense

carry high computational cost and memory consumption which make them hardly scalable for computer vision applications.

**:heavy_check_mark:Neighbourhood Consensus Networks**【2018】

trains a CNN to search in the 4D space of all possible correspondences, with the use of 4D convolutions.



[返回目录](#Contents)



<a name="Sparse-to-Dense"></a>

## Sparse-to-Dense

perform the detection stage asymmetrically. under strong visual changes, the need for repeatability in keypoint detection is alleviated, allowing each pixel to be a detection.

:heavy_check_mark:**Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization** 【2019】

**:heavy_check_mark:S2DNet: Learning Accurate Correspondences for Sparse-to-Dense Feature Matching** 【2020】



[返回目录](#Contents)



<a name="Sparse-to-Sparse"></a>

## Sparse-to-Sparse

<a name="Local Feature Detection"></a>

### 1. Local Feature Detection: not descriptor-specific

<a name="handcraft-detection"></a>

#### (1) handcraft

**:heavy_check_mark:Brisk: Binary robust invariant scalable keypoints.** 【2011】

:heavy_check_mark:**Kaze features**【2012，ECCV】

:heavy_check_mark:**In the saddle: chasing fast and repeatable features.** 【2016】

<a name="learned-detection"></a>

#### (2) learned

:heavy_check_mark:**Tilde: a temporally invariant learned detector.** 【2015】

trains a piece-wise linear regression model as the detector, that is robust to weather and illumination changes.

:heavy_check_mark:**Learning covariant feature detectors.** 【2016】

CNN models are trained with feature covariant constraints

:heavy_check_mark:**Learning discriminative and transformation covariant local feature detectors.**【2017】

CNN models are trained with feature covariant constraints

:heavy_check_mark:**Quad-networks: unsupervised learning to rank for interest point detection** 【2017】

assumes that the ranking of the keypoint scores should be invariant to image transformations.

:heavy_check_mark:**Learning to detect features in texture images.** 【2018】

:heavy_check_mark:**Repeatability is not enough: Learning affine regions via discriminability.** 【2018】

learns to predict the affine parameters of a local feature via the hard negative constant loss based on the descriptors.

**:heavy_check_mark:Key.net: Keypoint detection by handcrafted and learned cnn filters.** 【2019】

combines hand-crafted filters with learned ones to extract keypoints at different scale levels.

:heavy_check_mark:**ELF: Embedded Localisation of Features in pre-trained CNN** 【2019】

pre-trained CNNs on standard tasks such as classifcation can be adapted to keypoint detection

<a name="Local Feature Description"></a>

[返回目录](#Contents)

### 2. Local Feature Description: independent of the detectors

<a name="local patch datasets"></a>

#### (0) local patch datasets

:heavy_check_mark:**Discriminative learning of local image descriptors.** 【2011】	

:heavy_check_mark:**Hpatches: A benchmark and evaluation of handcrafted and learned local descriptors.** 【2017】

:heavy_check_mark:**A large dataset for improving patch matching.** 【2018】

<a name="handcraft-description"></a>

#### (1) handcraft: histograms of local gradients

:heavy_check_mark:Distinctive Image Features from Scale-Invariant Keypoints. 【2004】

:heavy_check_mark:SURF: Speeded Up Robust Features. 【2006】

:heavy_check_mark:BRIEF: Binary Robust Independent Elementary Features. 【2010】

:heavy_check_mark:ORB: An Efficient Alternative to SIFT or SURF. 【2011】

<a name="learned"></a>

#### (2) learned: deep local descriptors

:heavy_check_mark:Discriminative learning of deep convolutional feature point descriptors. 【2015】	

:heavy_check_mark:PN-Net: Conjoined Triple Deep Network for Learning Local Image Descriptors. 【2016】

:heavy_check_mark:Learning local feature descriptors with triplets and shallow convolutional neural networks 【2016】

:heavy_check_mark:L2-net: Deep learning of disriminative patch descriptor in euclidean space. 【2017】

:heavy_check_mark:Working hard to know your neighbor’s margins: Local descriptor learning loss. 【2017】

combines triplet loss with a within-batch hard negative mining that has proven to be remarkably effective

:heavy_check_mark:Learning deep descriptors with scale-aware triplet networks. 【2018】

:heavy_check_mark:Local descriptors optimized for average precision. 【2018】

:heavy_check_mark:Sosnet: Second order similarity regularization for local descriptor learning. 【2019】

extends HardNet with and second-order loss.

<a name="Joint Detection and Description"></a>

[返回目录](#Contents)

### 3. Joint Detection and Description

<a name="handcraft-d2"></a>

#### (1) handcraft

:heavy_check_mark:Distinctive image features from scale-invariant keypoints. 【2004】

:heavy_check_mark:SURF: Speeded Up Robust Features. 【2006】

<a name="learned-d2"></a>

#### (2) learned

:heavy_check_mark:Lift: Learned in variant feature transform. 【2016】

:heavy_check_mark:Superpoint: Self-supervised interest point detection and description. 【2018】【self-supervised】

leverages two separate decoders for detection and description on a shared encoder.

Synthetic shapes and image pairs generated from random homographies are used to train the two parts.

patch cropping is replaced by fully convolutional dense descriptors

:heavy_check_mark:Lf-net: learning local features from images. 【2018】【self-supervised】

:heavy_check_mark:Rf-net: An end-to-end image matching network based on receptive field. 【2019】

:heavy_check_mark:Contextdesc: Local descriptor augmentation with cross-modality context 【2019】

:heavy_check_mark:R2d2: Repeatable and reliable detector and descriptor. 【2019】【self-supervised】

learning keypoints that are not only repeatable but also reliable together with robust descriptors.

:heavy_check_mark:D2-net: A trainable cnn for joint detection and description of local features. 【2019】

learning keypoints that are not only repeatable but also reliable together with robust descriptors.

:heavy_check_mark:Aslfeat: Learning local features of accurate shape and localization 【2020】

:heavy_check_mark:Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization. 【2019】

:heavy_check_mark:Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization. 【2019】

:heavy_check_mark:D2D: Keypoint Extraction with Describe to Detect Approach 【2020】

description-guided detection



[返回目录](#Contents)
