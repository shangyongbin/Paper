[TOC]



#### Motivation

- **detectors based on various saliency measures** where the saliency was defined in terms of local signal complexity or unpredictability; 

  more specifically the Shannon entropy of local descriptor was suggested.

  -  Saliency, scale and image description. 【2001，IJCV】

     Recognition without correspondence using multidimensional receptive field histograms. 【2000，IJCV】

  - 由于dense local measurements的复杂性，这种思路没有被广泛采用。

  - 现在的CNN dense descriptors允许重新使用这种思路： using saliency measured by descriptors to define keypoint locations

#### Contribution

- 新范式：describe-then-detect

  -  detect-then-describe、detect-and-describe是两种策略

  - 对比local descriptors的进步，keypoint detector没有多少进步。

    新范式describe-then-detect可直接利用现有的描述符网络，不需额外训练。

- 给出了关键点的一种基于描述符的定义

  - Local invariant feature detectors: a survey认为good features的性质应包括**repeatability**、**informativeness**、**locality**、**quantity**、**accuracy**、**efficiency**
  - 本文提出了 a relative and an absolute saliency measure of local deep feature maps along the spatial and depth dimensions 来定义keypoints.

#### 介绍

- In the era of deep learning, there are t**hree main research directions** towards improving image matching
  - non-detector-specific **description**
    -  Local descriptors optimized for average precision【2018，CVPR】
    -  Working hard to know your neighbor’s margins: Local descriptor learning loss. 【2017，NIPS】
    -  L2-net: Deep learning of discriminative patch descriptor in euclidean space. 【2017，CVPR】
    -  Sosnet: Second order similarity regularization for local descriptor learning. 【2019，CVPR】
    -  Contextdesc: Local descriptor augmentation with cross-modality context. 【2019，CVPR】
    -  Geodesc: Learning local descriptors by integrating geometry constraints. 【2018，CVPR】
  - non-descriptor-specific **detection**
    - Tilde: a temporally invariant learned detector. 【2015，CVPR】
    - Key.net: Keypoint detection by handcrafted and learned cnn filters. 【2019】
  - jointly learnt **detection-description**
    - Lift: Learned invariant feature transform. 【2016，ECCV】
    - Lf-net: learning local features from images. 【2018，NIPS】
    - Rf-net: An end-to-end image matching network based on receptive field. 【2019，CVPR】
    - D2-net: A trainable cnn for joint detection and description of local features. 【2019】
    - R2d2: Repeatable and reliable detector and descriptor.  【2019，CVPR】

- detection-description的缺点
  - In contrast to the CNN based **descriptors**, the performance of jointly learnt **detection-description**  does not seem to generalise well across datasets and tasks.
  - CNN descriptors perform significantly better if trained and applied in the same data domain.
- 单独的detector的缺点
  - Different keypoint **detectors** are suitable for different tasks. fine-tuning a descriptor for a specific keypoint detector further improves the performance.
  - With all available options finding optimal pair of detector-descriptor for a dataset or a task requires extensive experiments.

#### Method

- What is a keypoint？

  - keypoints should be image points that have the potential of being repeatably detected under different imaging conditions.

    - 根据【Local invariant feature detectors: a survey】，这样的关键点应该满足**repeatability**、**informativeness**、**locality**、**quantity**、**accuracy**、**efficiency**
    - 本文称**informativeness**为**saliency**，认为这个性质能lead to satisfying most of the other requirements.

  - define the saliency in relative terms （the other descriptors in the neighbourhood）and in absolute terms （the information content of the descriptor）.

    - **Assumption 1**

      A point in an image has **a high absolute saliency** if its corresponding descriptor is highly **informative**.

      - 图像检索中，saliency/attention is defined on image regions with rich semantic information
      - 特征匹配中，local image structures that exhibit significant variations in shape and texture can be considered salient

    - **Assumption 2**

      A point in an image has **a high relative saliency** if its corresponding descriptor is highly **discriminative** in its spatial neighbourhood.

      - 单有the relative saliency是不够的。比如，均匀区域的角点有high relative saliency，但是描述符信息含量不高。

    - **Definition**

      A point in an image is a keypoint, if its corresponding descriptor’s absolute and relative saliencies are both high.

- How to detect a keypoint?

  - Measuring the **absolute saliency** of a point ：  computing the entropy of a descriptor

    - Orb: An efficient alternative to sift or surf. 【2011】

      Bold - binary online learned descriptor for efficient image matching. 【2015】

    - computing an accurate differential entropy requires probability density estimation, which is computationally expensive.

      ![image-20210803152302488](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803152302488.png)

  - Measuring the **relative saliency** of a point

    - A function that measures the relationship between a variable’s current value and its neighboring values is the **autocorrelation**. 【Moravec、Harris】

    ![image-20210803152449358](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803152449358.png)

  ![image-20210803152605604](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803152605604.png)

- Dense Descriptors

  -  patch-based methods : infeasible

     generate dense descriptors by extracting patches with a sliding window

  - FCN

    - HardNet

      SOSNet

    - SuperPoint

      D2-Net

- Details

  - 

#### Results

- Image Matching

  - 数据集：Hpatches dataset

    Hpatches contains 116 image sequences with ground truth homographies under different viewpoint or illumination changes.

  - 结果：

    - MMA for thresholds 1 to 10 pixels averaged over all image pairs.

    - mean number of keypoints

    - mean number of mutual nearest neighbour matches per image pair

    - the ratio between the two numbers

      ![image-20210803155733402](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803155733402.png)

- Day-Night Visual Localisation ：the task of long-term visual localization using the Aachen Day-Night dataset

  ​	This task evaluates the performance of local features under **challenging conditions** including day-night and viewpoint changes.

  - 数据集：Aachen Day-Night dataset

    Our evaluation is performed via a [localisation pipeline](https://github.com/tsattler/visuallocalizationbenchmark/tree/master/local_feature_evaluation) based on COLMAP [43] and The [Visual Localization Benchmark]([Benchmarking Long-term Visual Localization](https://www.visuallocalization.net/))

  - 结果

    ![image-20210803161457456](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803161457456.png)

- 3D Reconstruction 

  We test our method on the ETH SfM benchmark【Comparative evaluation of hand-crafted and learned local features,2017】 in the task of 3D reconstruction.

  no nearest neighbour ratio test is conducted to better expose the matching performance of the descriptors.

  - 数据集

  - 结果

    We compare the reconstruction quality by comparing 

    - the number of registered images-
    - reconstructed sparse and dense points
    - mean track length
    - the reprojection error

    ![image-20210803162038206](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803162038206.png)

- Efficiency : compare the feature extraction speed of several methods

  we record the extraction time over 108 image sequences in Hpatches, where there are 648 images with various resolutions (the average resolution is 775 × 978).

  

  ![image-20210803162329805](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2D.assets\image-20210803162329805.png)

