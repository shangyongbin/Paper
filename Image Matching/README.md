# Image Matching Paper

**更新中.../Updating...**



<a name="Contents"></a>

### :hammer: **目录|Table of Content**

- [Survey,Benchmark and Dataset](#Survey-Benchmark-Dataset)
  - [Survey](#Survey)
  - [Benchmark](#Benchmark)
  - [Dataset](#Dataset)
- [Dense-to-Dense](#Dense-to-Dense)
- [Sparse-to-Dense](#Sparse-to-Dense)
- [Sparse-to-Sparse](#Sparse-to-Sparse)
  - [Local Feature Detection](#Local-Feature-Detection)
    - [handcraft](#handcraft-detection)
    - [learned](#learned-detection)
  - [Local Feature Description](#Local-Feature-Description)
    - [handcraft](#handcraft-description)
    - [learned](#learned-description)
  - [Joint Detection and Description](#Joint-Detection-and-Description)
    - [handcraft](#handcraft-d2)
    - [learned](#learned-d2)




### :key: **关键词** | Keywords

【TODO】



<a name="Survey-Benchmark-Dataset"></a>

## Survey,Benchmark and Dataset

<a name="Survey"></a>

### Survey

:heavy_check_mark: **Local Invariant Feature Detectors: A Survey** 【2007】

:heavy_check_mark: **Image Matching from Handcrafted to Deep Features: A Survey** 【2020】

论文/Paper：https://link.springer.com/article/10.1007/s11263-020-01359-2

:heavy_check_mark:  On the Comparison of Classic and Deep Keypoint Detector and Descriptor Methods【2020】

论文/Paper: https://arxiv.org/abs/2007.10000

:heavy_check_mark:Features for Ground Texture Based Localization -- A Survey 【2020】

论文/Paper: https://arxiv.org/abs/2002.11948





<a name="Benchmark"></a>

### Benchmark

:heavy_check_mark: **Benchmarking 6DOF Outdoor Visual Localization in Changing Conditions** 【2018】

:heavy_check_mark: **Inloc: Indoor Visual Localization with Dense Matching and View Synthesis** 【2018】

:heavy_check_mark:**The Visual Localization Benchmark**

:heavy_check_mark:**Image Matching Benchmark**

相关：[image-matching-benchmark-baseline](https://github.com/shangyongbin/image-matching-benchmark-baselines)



:heavy_check_mark: An evaluation of feature matchers for  fundamental matrix estimation. 【2019】

:heavy_check_mark: Comparative evaluation of hand-crafted and learned local  features. 【2017】



:heavy_check_mark: Tanks and Temples: Benchmarking large-scale scene reconstruction.  【2017】





<a name="Dataset"></a>

### Dataset

- **Image Matching**

  :heavy_check_mark: **HPatch dataset**

  总结：

  链接/Link：https://hpatches.github.io/

- **Long-Term Visual Localization**

  :heavy_check_mark: **Aachen Day-Night dataset**

  使用：https://github.com/Midhun07/Night-to-day-Aachen-dataset

  链接/Link：

  :heavy_check_mark: **RobotCar Seasons dataset**

  总结：

  链接/Link：

  :heavy_check_mark: **InLoc dataset** (challenging)

  使用总结：

  链接/Link：

<a name="Dense-to-Dense"></a>

[返回目录/back](#Contents)



## Dense-to-Dense

> This approach carries high computational cost and memory consumption, which make them hardly scalable for computer vision applications.

**:heavy_check_mark:Neighbourhood Consensus Networks**【2018】



[返回目录/back](#Contents)



<a name="Sparse-to-Dense"></a>

## Sparse-to-Dense

> This paradigm performs the detection stage asymmetrically. 
>
> Under strong visual changes, the need for repeatability in keypoint detection is alleviated, allowing each pixel to be a detection.

:heavy_check_mark:**Sparse-To-Dense Hypercolumn Matching for Long-Term Visual Localization** 【2019】

**:heavy_check_mark:S2DNet: Learning Accurate Correspondences for Sparse-to-Dense Feature Matching** 【2020】



[返回目录/back](#Contents)



<a name="Sparse-to-Sparse"></a>

## Sparse-to-Sparse

<a name="Local-Feature-Detection"></a>

### 1. Local Feature Detection: not descriptor-specific

<a name="handcraft-detection"></a>

#### (1) handcraft

:heavy_check_mark:Brisk: Binary robust invariant scalable keypoints. 【2011】

:heavy_check_mark:Kaze features【2012，ECCV】

:heavy_check_mark:In the saddle: chasing fast and repeatable features. 【2016】

<a name="learned-detection"></a>

#### (2) learned

:heavy_check_mark:Tilde: a temporally invariant learned detector. 【2015】

use a principle similar to Homographic Adaptation.

:heavy_check_mark:Learning covariant feature detectors. 【2016】

:heavy_check_mark:Learning discriminative and transformation covariant local feature detectors.【2017】

:heavy_check_mark:Quad-networks: unsupervised learning to rank for interest point detection 【2017】【无监督】

patch-baed,relatively shallow 2-layer network.

:heavy_check_mark:Learning to detect features in texture images. 【2018】

:heavy_check_mark:Repeatability is not enough: Learning affine regions via discriminability. 【2018】

:heavy_check_mark:Key.net: Keypoint detection by handcrafted and learned cnn filters. 【2019】

:heavy_check_mark:**ELF: Embedded Localisation of Features in pre-trained CNN** 【2019】

总结：通过feature map的梯度图取阈值得到关键点。

论文/Paper：https://arxiv.org/abs/1907.03261

代码/Code：https://github.com/abenbihi/elf



<a name="Local Feature Description"></a>

[返回目录/back](#Contents)

### 2. Local Feature Description: independent of the detectors

<a name="Local-Feature-Description"></a>

#### (0) local patch datasets

:heavy_check_mark:**Discriminative learning of local image descriptors.** 【2011】	

:heavy_check_mark:Hpatches: A benchmark and evaluation of handcrafted and learned local descriptors. 【2017】

:heavy_check_mark:A large dataset for improving patch matching. 【2018】

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

:heavy_check_mark:**L2-net: Deep learning of disriminative patch descriptor in euclidean space.** 【2017】

总结：https://www.cnblogs.com/eilearn/p/9998369.html

论文/Paper：https://ieeexplore.ieee.org/document/8100132

代码/Code：

:heavy_check_mark:Working hard to know your neighbor’s margins: Local descriptor learning loss. 【2017】

:heavy_check_mark:Learning deep descriptors with scale-aware triplet networks. 【2018】

:heavy_check_mark:**Local descriptors optimized for average precision.** 【2018】

总结：直接优化AP

论文/Paper：https://arxiv.org/abs/1804.05312

代码/Code：

:heavy_check_mark:Sosnet: Second order similarity regularization for local descriptor learning. 【2019】

:heavy_check_mark:**Contextdesc: Local descriptor augmentation with cross-modality context** 【2019】

总结：https://github.com/shangyongbin/Paper/blob/master/Image%20Matching/Paper/Sparse-to-Sparse/ContextDesc.md

论文/Paper：https://arxiv.org/abs/1904.04084

代码/Code：https://github.com/lzx551402/contextdesc

<a name="Joint-Detection-and-Description"></a>

[返回目录/back](#Contents)

### 3. Joint Detection and Description

<a name="handcraft-d2"></a>

#### (1) handcraft

:heavy_check_mark:**Distinctive image features from scale-invariant keypoints.** 【2004】

总结：

论文/Paper：http://www.cs.ubc.ca/~lowe/papers/ijcv04.pdf

代码/Code：

:heavy_check_mark:SURF: Speeded Up Robust Features. 【2006】

总结：

论文/Paper：

代码/Code：

<a name="learned-d2"></a>

#### (2) learned

- **detect-then-describe**

  **:heavy_check_mark:Lift: Learned in variant feature transform.** 【2016】

  总结：

  论文/Paper：

  代码/Code：

  :heavy_check_mark:**Lf-net: learning local features from images.** 【2018】【self-supervised】

  总结：

  论文/Paper：

  代码/Code：

  :heavy_check_mark:**Rf-net: An end-to-end image matching network based on receptive field.** 【2019】

  总结：

  论文/Paper：

  代码/Code：

  

- **detect-and-describe**

  :heavy_check_mark:**Superpoint: Self-supervised interest point detection and description.** 【2018】【self-supervised】

  总结：

  论文/Paper：https://arxiv.org/abs/1712.07629

  代码/Code：[magicleap/SuperPointPretrainedNetwork](https://github.com/magicleap/SuperPointPretrainedNetwork) | [rpautrat/SuperPoint](https://github.com/rpautrat/SuperPoint) |[eric-yyjau/pytorch-superpoint](https://github.com/eric-yyjau/pytorch-superpoint)

  :heavy_check_mark:**R2d2: Repeatable and reliable detector and descriptor.** 【2019】【self-supervised】

  总结：

  论文/Paper：https://arxiv.org/abs/1906.06195

  代码/Code：https://github.com/naver/r2d2 | [视频](https://www.bilibili.com/video/av84172526/)

  :heavy_check_mark: Unsuperpoint: End-to-end  unsupervised interest point detector and descriptor 【2019】

  :heavy_check_mark:Aslfeat: Learning local features of accurate shape and localization 【2020】

  总结：

  论文/Paper：https://arxiv.org/abs/2003.10071v2

  代码/Code：

  :heavy_check_mark:**DenserNet: Weakly Supervised Visual Localization Using Multi-scale Feature Aggregation**【2021】

  总结：

  论文/Paper：https://arxiv.org/abs/2012.02366

  代码/Code：

  :heavy_check_mark:Realtime CNN-based Keypoint Detector with Sobel Filter and CNN-based Descriptor Trained with Keypoint Candidates【2020】

  总结：

  论文/Paper：http://arxiv.org/abs/2011.02119

  代码/Code：
  
  









- **describe-and-detect** : description-guided detection

  :heavy_check_mark:**D2-net: A trainable cnn for joint detection and description of local features.** 【2019】

  总结：

  论文/Paper：https://arxiv.org/abs/1905.03561

  代码/Code：https://github.com/mihaidusmanu/d2-net

  :heavy_check_mark:**D2D: Keypoint Extraction with Describe to Detect Approach** 【2020】

  总结：

  论文/Paper：https://arxiv.org/abs/2005.13605

  代码/Code：None





[返回目录/back](#Contents)

#### 4. Other

:heavy_check_mark:Learning to assign orientations to feature points 【2016】



:heavy_check_mark: Local keypoint-based Faster R-CNN【2020】



:heavy_check_mark: Circle loss: A unified perspective of pair similarity  optimization 【2020】

总结：

论文/Paper：https://arxiv.org/abs/2002.10857v2

代码/Code：

