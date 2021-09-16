# Realtime CNN-based Keypoint Detector with Sobel Filter and CNN-based Descriptor Trained with Keypoint Candidates

[TOC]





## Motivation

- **Handcraft filters** and **image pyramid** are usually used in  traditional keypoint detection methods.

  Inspired by **Key.Net**,

  -  use the output feature maps of  handcraft filters as the inputs of CNN.(only one)
  - use multi-scale images as the inputs of SobelNet.

- keypoint detection and descriptor computation are different tasks and should focus on separate issues.

  - 近年来，联合训练detector和descriptor成为潮流，假设`keypoints’ locations have a close relationship  with their corresponding descriptors`。这类方法通常有`a shared backbone, two separate heads`【SuperPoint、R2D2】。像【R2D2、D2D】，还考虑了`points with similar  descriptors should not be treated as keypoints`（R2D2增加了reliability map，D2D设计了relative saliancy）
  
  - 本文认为，检测和描述是不同的任务，关注不同的问题，应分别训练。**？？？？**
  
    检测器是检测不同视角下相同关键点，`corner points`可以在视角变化下保持不变。
  
    描述符是用来使 对应点的描述符尽可能相似，非对应点的描述符尽可能discriminative。
  
    :question:*所以为什么要分别训练？ 检测和描述虽然是不同的任务，但是检测器和描述符网络虽然是不同任务，但是它们都是针对某一个点（某一个点检测是否为特征点，对这个点描述），是相互耦合的，共用信息的显而易见的。*detect-and-describe这类方法公用一个backbone是因为无论检测或描述，都是从原图中提取信息，而一个backboe的作用就是`extract feature`。
  
    



## Method

### 1. Architecture

#### (1) SobelNet

![image-20210913105459915](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\Realtime CNN-based Keypoint Detector with Sobel Filter and CNN-based Descriptor Trained with Keypoint Candidates.assets\image-20210913105459915.png)

输入：Original image, two downscaled images (scale factors are $\sqrt{2}, 2$)

1. Sobel filter

   ![image-20210913110603353](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\Realtime CNN-based Keypoint Detector with Sobel Filter and CNN-based Descriptor Trained with Keypoint Candidates.assets\image-20210913110603353.png)

2. Gaussian filter

3. three convolutional layers with eight channels remaining its  dimension

4.  the downscaled feature maps are upscaled to the original image  size

5. feature maps will be summed up

6. the final convolutional layer to produce  an output score map

7. set the value of points (less than a certain ratio of the maximum  value) in the score map to zero

8. NMS

#### (2) DesNet

- a descriptor should have a large receptive  field to contain as much information around the keypoints as  possible

![image-20210913110757573](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\Realtime CNN-based Keypoint Detector with Sobel Filter and CNN-based Descriptor Trained with Keypoint Candidates.assets\image-20210913110757573.png)



### 2. Loss

#### (1) Gaussian loss





#### (2) Circle loss





## Results