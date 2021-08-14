# SuperPoint: Self-Supervised Interest Point Detection and Description

[TOC]



## Conclude

- **detect-and-describe**

  - 采用FCN网络，输入整个图像，一次前向传播联合计算了像素级的（dense）关键点位置和相应的描述符。

- **self-supervised approach**

  - pseudo-ground truth interest point locations

    supervised by the detector itself, rather than a large-scale human annotation effort.

    由MagicPoint（在Synthetic Shapes上训练得到的base detector）+ Homographic Adaptation 得到。

    - 首先，在Synthetic Shapes（millions of synthetic images）上训练一个base detector（称为MagicPoint）
      - MagicPoint在合成数据集上表现很好，超出传统的检测器
      - MagicPoint在真实图像上表现也不错，尽管有domain adaptation difficulties。但相比传统检测器，MagicPoint还是会漏检很多关键点。
    - 然后，Homographic Adaptation + MagicPoint产生pseudo ground truth
      - 训练数据集：MS-COCO generic image dataset
      - 使用Homographic Adaptation，warp输入图像多次。将这些图像通过MagicPoint，产生伪真值。

- **Homographic Adaptation**

  - a multi-scale, multi homography approach.
  - bridge the gap between synthetic and real images，to boost detectors' repeatability.



## Motivation

- the notion of interest point detection is semantically ill-defined
  - Thus training convolution neural networks with strong supervision of interest points is non-trivial.
  - we create a large dataset of pseudo-ground truth interest point locations in real images, supervised by the interest point detector itself.





## Method

### 1. SuperPoint Architecture

![image-20210809171335945](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809171335945.png)

- **输入**

  $I \in \mathbb{R}^{H \times W}$

- **Encoder**

  ![image-20210809183728225](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809183728225.png)

  ![image-20210809172838762](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809172838762.png)

  ![image-20210809183227775](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809183227775.png)

  |  name   | ksize | stride | padding |       size       |  rf  |      |
  | :-----: | :---: | :----: | :-----: | :--------------: | :--: | :--: |
  |         |       |        |         |   $H \times W$   |  1   |      |
  | conv1a  |   3   |   1    |    1    |                  |  3   |  +2  |
  | conv1b  |   3   |   1    |    1    |                  |  5   |  +2  |
  | maxpool |   2   |   2    |         | $H/2 \times W/2$ |  6   |      |
  | conv2a  |   3   |   1    |    1    |                  |  10  |  +4  |
  | conv2b  |   3   |   1    |    1    |                  |  14  |  +4  |
  | maxpool |   2   |   2    |         | $H/4 \times W/4$ |  16  |      |
  | conv3a  |   3   |   1    |    1    |                  |  24  |  +8  |
  | conv3b  |   3   |   1    |    1    |                  |  32  |  +8  |
  | maxpool |   2   |   2    |         | $H/8 \times W/8$ |  36  |      |
  | conv4a  |   3   |   1    |    1    |                  |  52  | +16  |
  | conv4b  |   3   |   1    |    1    |                  |  68  | +16  |

  

  - VGG-style

    - eight 3x3 convolution layers sized 64-64-64-64-128-128- 128-128.

    - Every two layers there is a 2x2 max pool layer.

      the spatial resolution is decreased via **pooling** or **strided convolution**.

  - 输出

    $\mathcal{B} \in \mathbb{R}^{H_c \times W_c \times F}$

    $H_c = H/8, W_c = W/8, channels = 128$

  - 感受野

    

- **Decoder**

  - **Interest Point Decoder**

    - 上采样层（upsampling layers，如SegNet）的缺点

      a high amount of computation、 **checkerboard artifacts**

    ![image-20210809184718706](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809184718706.png)

    ![image-20210809184701064](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809184701064.png)

    ![image-20210809184738505](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809184738505.png)

    |  name  | ksize | stride | padding |       size       |  rf  |      |
    | :----: | :---: | :----: | :-----: | :--------------: | :--: | :--: |
    | conPa  |   3   |   1    |    1    | $H/8 \times W/8$ |  84  | +16  |
    | convPb |   1   |   1    |         |                  |  84  |      |

    

    a single 3x3 convolutional layer of 256 units, followed by a 1x1 convolution layer with 65 units.

    - 输入

      $\mathcal{B} \in \mathbb{R}^{H_c \times W_c \times F}$, $H_c = H/8, W_c = W/8, channels = 128$

    - 中间结果$\mathcal{X} \in \mathbb{R}^{H_c \times W_c \times 65}$

      - 先通过$3 \times 3$的卷积、BN、激活，得到$H/8 \times W/8 \times 256$；再通过$1 \times 1$的卷积、BN，得到$H/8 \times W/8 \times 65$。

      -  The 65 channels correspond to local, non-overlapping 8 × 8 grid regions of pixels plus an extra “no interest point” dustbin.

    - 输出 $\mathbb{R}^{H \times W}$

      - 先通过a channel-wise softmax，the dustbin dimension is removed；然后reshape$\mathbb{R}^{H_c \times W_c \times 64} \Rightarrow \mathbb{R}^{H \times W}$
      - each pixel of the output corresponds to a probability of “**pointness**” for that pixel in the input.

  - **Interest Point Decoder**

    ![image-20210809191119547](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809191119547.png)

    ![image-20210809191409273](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809191409273.png)

    ![image-20210809191431282](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809191431282.png)

    

    |  name  | ksize | stride | padding |       size       |  rf  |      |
    | :----: | :---: | :----: | :-----: | :--------------: | :--: | :--: |
    | conDa  |   3   |   1    |    1    | $H/8 \times W/8$ |  84  | +16  |
    | convDb |   1   |   1    |         |                  |  84  |      |

    

    a single 3x3 convolutional layer of 256 units, followed by a 1x1 convolution layer with 256 units.

    - 输入

      $\mathcal{B} \in \mathbb{R}^{H_c \times W_c \times F}$, $H_c = H/8, W_c = W/8, channels = 128$

    - 中间结果$\mathcal{D} \in \mathbb{R}^{H_c \times W_c \times D}$

      - 先通过$3 \times 3$的卷积、BN、激活，得到$H/8 \times W/8 \times 256$；再通过$1 \times 1$的卷积、BN，得到$H/8 \times W/8 \times 256$。

    - 输出$\mathbb{R}^{H \times W \times D}$（类似UCN）

      - 先通过Bi-Cubic Interpolate，得到 a semi-dense grid（one every 8 pixels） of descriptors $\mathbb{R}^{H \times W \times D}$；再通过L2-normalization变为单位长度。

### 2. Training

####  (1) MagicPoint: Synthetic Pre-Training

##### Synthetic Dataset: Synthetic Shapes

Synthetic Shapes consists of simplified 2D geometry via synthetic data rendering of *quadrilaterals*, *triangles*, *lines* and *ellipses*.

![image-20210809192854956](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809192854956.png)

In this dataset, we are able to remove label ambiguity by modeling interest points with simple *Y-junctions*, *L-junctions*, *T-junctions* as well as *centers of tiny ellipses* and *end points of line segments*.

Once the synthetic images are rendered, we apply homographic warps to each image to augment the number of training examples.

##### MagicPoint

- 数据：Synthetic Shapes
- 网络：Encoder+Interest Point Decoder
- 损失：log损失？
- 训练：200,000 iterations

- 结果

  - the mean Average Precision (mAP) on 1000 held-out images of the Synthetic Shapes dataset

  ![image-20210809194148896](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210809194148896.png)

  - We were surprised to find that MagicPoint performs reasonably well on real world images, especially on scenes which have strong corner-like structure such as tables, chairs and windows.

    Unfortunately in the space of all natural images, it underperforms when compared to the same classical detectors on repeatability under viewpoint changes.

#### (2) Pseudo ground truth:Homographic Adaptation

##### Homographic Adaptation

At the core of our method is a process that **applies random homographies to warped copies of the input image and combines the results**.

- Homographic Adaptation Overview

  **homographies** are at the core of our self-supervised approach.

  ![image-20210810153718368](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810153718368.png)

  - $f_{\theta}(·)$：特征点函数，$I$：输入图像，$x$：特征点，$\mathcal{H}$：单应性

  $$
  x = f_{\theta}(I)
  $$

  - $f_{\theta}(·)$ should be convariant with respect to homographies $\mathcal{H}$.
    $$
    \mathcal{H}x = f_{\theta}(\mathcal{H}(I))
    x = \mathcal{H}^{-1} f_{\theta}(\mathcal{H}(I))
    $$
    In practice, a detector will not be perfectly covariant.

  - The basic idea behind Homographic Adaptation is to **perform an empirical sum over a sufficiently large sample of random $\mathcal{H}$’s**
    $$
    \hat{F}(I;f_{\theta}) = \frac{1}{N_h} \sum_{i=1}^{N_h}\mathcal{H}^{-1} f_{\theta}(\mathcal{H}_i (I))
    $$

- Choosing Homographies

  ![image-20210810155305338](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810155305338.png)

  - we decompose a potential homography into more simple, less expressive transformation classes.

    - translation
    - scale
    - in-plane rotation
    - sysmetric perspective distortion using a truncated normal distribution

    These transformations are composed together with **an initial root center crop** to help avoid **bordering artifacts**.

  - we use **the average response** across a large number of homographic warps of the input image.

    $N_h = 100$

    - 

- Iterative Homographic Adaptation

  The process can be repeated iteratively to continually self-supervise and improve the interest point detector.

  ![image-20210810155243341](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810155243341.png)



##### Pseudo labels

- 数据集：[MS-COCO 2014](https://cocodataset.org/#home)  training dataset split which has 80,000 images

  The images are sized to a resolution of 240 × 320 and converted to grayscale.

- 网络：MagicPoint base detector

- 方法：Homographic Adaptation with $N_h = 100$

  ![image-20210810153718368](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810153718368.png)

  We repeat the Homographic Adaptation a second time, using the resulting model trained from the first round of Homographic Adaptation.

#### (3) Train

- 数据集：[MS-COCO 2014](https://cocodataset.org/#home)  training dataset split which has 80,000 images

  The images are sized to a resolution of 240 × 320 and converted to grayscale.

  - 输入：pairs of synthetically warped images $I, I'$
    - pseudo-ground truth interest point locations
    - the ground truth correspondence from a randomly generated homography $\mathcal{H}$ which relates the two images.
  - pseudo ground truth：interest point locations

- 网络：SuperPoint

- 输出

  - detected locations: $\mathcal{X}=\{ \mathbb{x}_{hw} \in \mathbb{R}^{65} \}, \mathcal{X'}$；ground truth: $\mathcal{Y}=\{ \mathbb{x}_{hw} \in \mathbb{R} \}, \mathcal{Y'}$

  - descriptors: $\mathcal{D}=\{ \mathbb{d}_{hw} \in \mathbb{R}^{256} \}, \mathcal{D'}=\{ \mathbb{d'}_{h'w'} \in \mathbb{R}^{256} \}$

    

    

- 损失：

##### Loss

$$
\mathcal{L}(\mathcal{X}, \mathcal{X'}, \mathcal{D}, \mathcal{D'}; \mathcal{Y}, \mathcal{Y'}, S) = 
\mathcal{L}_p(\mathcal{X}, \mathcal{Y}) + 
\mathcal{L}_p(\mathcal{X'}, \mathcal{Y'}) +
\mathcal{L}_d(\mathcal{D}, \mathcal{D'}, S)
$$

- $\mathcal{L}_p(\mathcal{X}, \mathcal{Y})$

  对于每8个位置，有1个ground truth。对应ground truth处的logp最大。
  $$
  \mathcal{L}_p(\mathcal{X}, \mathcal{Y}) = 
  \frac{1}{H_c W_c}
  \sum_{h=1 \\ w=1}^{H_c, W_c}
  l_p(\mathbb{x}_{hw}; y_{hw}) 
  
  \\
  
  l_p(\mathbb{x}_{hw}; y_{hw}) = 
  -log(
  \frac
  { exp(\mathbb{x}_{hwy}) }
  { \sum_{k=1}^{65} exp(\mathbb{x}_{hwk}) }
  )
  $$

- $\mathcal{L}_d(\mathcal{D}, \mathcal{D'}, S)$

  - $S$

  ![image-20210810192543494](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810192543494.png)

  ![image-20210810192618711](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810192618711.png)

  - $\mathcal{L}_d(\mathcal{D}, \mathcal{D'}, S)$

  ![image-20210810192641972](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810192641972.png)

## Results

### System Runtime

- Titan X GPU: 13 ms or 70 FPS

  - A single forward pass of the model runs in approximately 11.15 ms with inputs sized 480 × 640, which produces the point detection locations and a semi-dense descriptor map.

  - we can just sample from the 1000 detected locations, which takes about 1.5 ms on a CPU implementation of bi-cubic interpolation followed by L2 normalization.

### HPatches dataset

#### Repeatability

- Repeatability is computed at 240 × 320 resolution with 300 points detected in each image.
- We also vary the Non-Maximum Suppression (NMS) applied to the detections. 
- We use a correct distance of $\epsilon =3$ pixels.

![image-20210810162642120](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810162642120.png)

#### Homography Estimation

- We evaluate SuperPoint against LIFT, SIFT, ORB

  - For LIFT we use the pre-trained model (Picadilly) provided by the authors.
  - For SIFT and ORB we use the default OpenCV implementations.

- We use a correct distance of $\epsilon= 3$ pixels for Rep, MLE, NN mAP and MScore.

- We compute **a maximum of 1000 points** for all systems at **a 480 × 640 resolution** and compute a number of metrics for each image pair.

- To estimate the homography, we perform **nearest neighbor matching** from all interest points+descriptors detected in the first image to all the interest points+descriptors in the second.

  We use an OpenCV implementation (findHomography() with RANSAC) with all the matches to compute the final homography estimate.

![image-20210810163032509](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810163032509.png)

![image-20210810163136683](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\SuperPoint.assets\image-20210810163136683.png)

