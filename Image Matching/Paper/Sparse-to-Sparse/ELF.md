# ELF: Embedded Localisation of Features in pre-trained CNN

[ELF: Embedded Localisation of Features in pre-trained CNN (ICCV2019) - YouTube](https://www.youtube.com/watch?v=oxbG5162yDs)

![image-20210913093711847](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210913093711847.png)

## Motivation

- 先前的工作（描述符网络）已经从CNN的feature map得到descriptor，但是没有使用feature map直接得到feature detection.

  no existing approach uses a pre-trained CNN for feature detection.

- inspired by 【*Deep inside convolutional networks: Visualising image classification models and saliency maps*】,  the gradient of classification scores w.r.t the image is similar to the image saliency map.

  - ELF computes **the gradient of a trained CNN feature map with respect to w.r.t the image**: this outputs a saliency map with local maxima on keypoint positions
  - The extracted saliency map is then thresholded to keep only the most relevant locations.
  - Standard Non-Maxima Suppression (NMS) extracts the fnal keypoints.

  ![image-20210909100954650](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909100954650.png)

## Method

1. compute a saliency map

   the feature gradient w.r.t the image

2.  automatically threshold the saliency map

   use the data adaptive Kapur method

3.  run NMS for local maxima detection

### 1. Feature Specific Saliency

$\bold{I}$: a vector image of dimension $D_I = H_I · W_I · C_I$.

$F^l$: a vectorized feature map of dimension $D_F = H_l · W_l · C_l$.

$S^l$: the saliency map of dimension $D_I$
$$
S^l = \lvert ^t F^l(\bold{I}) · \nabla_I F^l \rvert
$$

- saliency激活在 对特征表达$F^l(\bold{I})$贡献最大的区域

- $\nabla_I F^l$ 是一个$D_F \times D_I$的矩阵

  - 表达了特征空间$F^l$和图像空间的correlation。

  - 从几何角度看，$\nabla_I F^l$ 可看作特征空间到图像空间的投影。
  - 从信号处理角度看，$F^l(\bold{I})$是信号输入，被$\nabla_I F^l$滤波到图像空间。

#### Feature Map Selection



### 2. Automatic Data-Adaptive Thresholding

- 使用$(\mu_{thr},\sigma_{thr})$高斯滤波器进行滤波

- 使用**Kapur’s method**计算阈值，进行阈值处理

- 使用$(\mu_{noise},\sigma_{noise})$高斯滤波器进行去噪

- run standard NMS

  we iteratively select decreasing global maxima while ensurwe iteratively select decreasing global maxima while ensurwindow $w_{NMS} ∈ N$



## Experiments

- handcrafted: SIFT, SURF, ORB, KAZE
- learning-based: SIFT, SuperPoint, LF-Net
- learning-based: TILDE, MSER

### 1. evaluation metrics

**A good keypoint is one that can be discriminatively described and matched.**

- repeatability (rep)
- matching score (ms)

### 2. datasets

All images are resized to the 480×640 pixels, and the image pair transformations are rectified accordingly.

-  **General performances**

  `HPatches dataset`

  it provides a total of 696 images (**6 images for 116 scenes**),  **the corresponding homographies** between the images of a same scene.

  -  For 57 of these scenes, the main changes are **photogrammetric** (lighting).

  - the remaining 59 show significant geometric deformations due to **viewpoint changes** on planar scenes.

    > The viewpoint changes proposed by HPatches are limited to **planar scenes** which does not reflect the complexity of 3D structures

  

- **Illumination Robustness**

  `Webcam dataset`

  static outdoor scenes with drastic natural light changes contrary to HPatches which mostly holds artifcial light changes in indoor scenes.

  

- **Rotation and Scale Robustness**

  derived from HPatches, with ground truth homographies for future comparisons.

  - For each of the 116 scenes, we keep the first image and rotate it with angles from 0 ◦ to 210◦ with an interval of 40◦ .
  - Four zoomed-in version of the image are generated with scales [1.25, 1.5, 1.75, 2].

- **3D Viewpoint Robustness**

  **three Strecha scenes** with increasing viewpoint changes: *Fountain, Castle entry, Herzjesu-P8*.

  Since the ground-truth depths are not available anymore, we use COLMAP3D reconstruction to obtain groundtruth scaleless depth. -> **depth maps, camera poses**

### 3. results

-  **General performances**: HPatches

  - learning-based methods all outperform handcrafted ones

  - LF-Net和LIFT在HPatches上性能弱的原因

    -  the data they are trained on differs too much from this one

      LIFT训练在outdoor images上，LF-Net训练在indoor和outdoor datasets上。HPatches由两者混合而成。

![image-20210909115941645](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909115941645.png)



- **Light Robustness**: Webcam

  - Overall, there is a performance degradation (∼20%) from HPatches to Webcam.

    - HPatches holds images with standard features such as corners
    - There are less such features in the Webcam dataset because of the natural lighting that blurs them

  - One reason may be that the learning-based methods never saw such lighting variations in their training set. 

    But this assumption is rejected as we observe that even SuperPoint, which is trained on Coco images, outperforms LIFT and LF-Net, which are trained on outdoor images.

  - Another justification can be that what matters the most is the pixel distribution.

  **![image-20210909120701768](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909120701768.png)**

- **Scale Robustness**

  - Repeatability is mostly stable for all methods

  - ms better assesses the detectors performance

    - SuperPoint is the most robust to scale changes.

    - followed by LIFT and SIFT. ELF and LF-Net lose 50% of their matching score with the increasing scale.

    - LIFT is more scale-robust than LF-Net when the latter’s global performance is higher. 

      LIFT detects keypoints at 21 scales of the same image whereas LF-Net only runs its detector CNN on 5 scales.

  ![image-20210909121657715](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909121657715.png)

- **Rotation Robustness**

  - all learned methods’ ms crash while **only SIFT survives** the rotation changes
    - **orientation estimation**

  ![image-20210909121836117](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909121836117.png)

- **3D Viewpoint Robustness**

  ![image-20210909122514412](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ELF.assets\image-20210909122514412.png)
  - all methods degrade uniformly.
    - While SIFT shows a clear advantage of pure-rotation robustness, it displays similar degradation as other methods on realistic rotation-and-translation on 3D structures.

#### CVPR19 Image Matching Challenge

This challenge evaluates detection/description methods on two standard tasks:

1. wide stereo matching
   - dataset:  `the photo-tourism image collections of popular landmarks`
   - metric: `matching score`, `camera pose estimation`
2. structure from motion from small image sets
   - dataset:  `the photo-tourism image collections of popular landmarks`
   - metric:  `camera pose estimation`

- **wide stereo matching**: matches image pairs across wide baselines

  

- **Structure-from-Motion from small subsets**