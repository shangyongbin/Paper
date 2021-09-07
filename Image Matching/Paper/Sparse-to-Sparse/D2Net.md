https://paperswithcode.com/paper/190503561

https://blog.csdn.net/u010260681/article/details/108370305

https://www.pianshen.com/article/20981511076/

- **解决问题、Motivation**

  - 极度变化下（白天和黑夜、低纹理区域），性能差。原因：缺少repeatability：detector仅仅考虑了small image regions，检测使用的low-level information更容易受到外界的影响

    直接dense matching能表现得更好，但是higher matching time和memory consumption。

  - 一个网络同时描述和检测。

    - 先检测，然后patch描述
    - 主干网络，分支进行检测和描述

- **方法**

  ![image-20210726135108726](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726135108726.png)

  ![img](https://pics5.baidu.com/feed/c2fdfc039245d6888f2a8c35134ecc18d31b248d.jpeg?token=9f27ce488fd6f3fdb238c6f94fe1dc14)

  输入I，通过特征提取网络VGG16，得到feature map F。输出descriptor和score map

  - 将F看作提取的dense descriptor，再使用L2 正则归一化。

  - 将F看作类似SIFT中的DOG响应图或Harris中的corner响应图，每个通道都看作一个响应图。如果一个点是特征点，首先要在通道方向最大，其次要在空间上为局部最值点。

    ![image-20210726172520962](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726172520962.png)

    但是在训练时不同使用非0即1的方式，本文采用打分机制。

    - 在通道方向，使用ratio-to-max，即相对于最大值的比例。（每个通道上的每个位置都能得到一个0-1的值）

    ![image-20210726172017322](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726172017322.png)

    - 在空间上，使用soft-local-max（即在邻域内使用softmax）。（每个通道上的每个位置都能得到一个0-1的值）

    ![image-20210726172149784](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726172149784.png)

    因此，每个位置的分数为两者的乘积，再取每个通道的最大值。（得到一个2D分数图）

    ![image-20210726172254487](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726172254487.png)

    最后对分数图进行归一化。

    ![image-20210726172506444](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726172506444.png)

    

- **损失**

  ![image-20210726173842885](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726173842885.png)

  ![image-20210726173849487](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726173849487.png)

  ![image-20210726173903400](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726173903400.png)

  ![image-20210726173909078](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726173909078.png)

  ![image-20210726173930825](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726173930825.png)

  

- **测试**

  首先对输入图像构建图像金字塔（0.5，1，2），然后在每个scale上进行forward，得到D2特征图，再把多尺度特征图逐scale上采样并与同分辨率融合（见下式），得到融合后的特征图。预测阶段根据融合特征图进行上述后处理，即可提取出特征点。

  ![image-20210726174751300](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726174751300.png)

- **结果**

  1. standard image matching task

     数据集：**HPatches**，116个序列中使用108个序列，每个序列有6个图片。每个序列使用第一个匹配其他剩下5个，得到108*5=540个图像对。

     - 光照改变的序列（56个没有）

     - 视角改变的序列（52个没有）

       每个图像对，使用nearest neighbor search匹配，当 mutual nearest neighbors时接受匹配。

       一个匹配被认为是正确的，如果它的 reprojection error（由数据集提供的homography估计）低于给定的匹配阈值。

       变化阈值，记录所有图像对的mean matching accuracy (MMA，每个图像对正确匹配的百分比/图像对数目)

       ![image-20210726180356514](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726180356514.png)

  2. two more complex computer vision pipelines

     - 3D reconstruction

       数据集：Madrid Metropolis、Gendarmenmarkt、Tower of London。

       首先run SfM，然后Multi-View Stereo（MVS）。

       - SfM

         the number of images and 3D points（大）、the mean track lengths of the 3D points（大）、 the mean reprojection error（小）

         ![image-20210726181018769](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\D2Net.assets\image-20210726181018769.png)

       - MVS

     - visual localization

       - Day-Night Visual Localization.

         数据集：Aachen Day-Night dataset。98个夜晚图像，每个夜晚图像对应多大20个白天图像，知道相对位姿。

         

       - Indoor Visual Localization.

         数据集：InLoc dataset。

- 问题

  - 作者这里提到sparse方法的缺陷是keypoint不够可重复，因为这些sparse feature提取时只考虑图像低层特征。但是这段又没给参考文献，所以本文究竟是针对哪些论文做的改进呢？近几年的local feature并不会像作者说的那样“only consider small low-level information like image regions”啊？难道是针对SIFT为代表的的传统方法的缺陷吗？看到下面评估部分也有和SuperPoint对比，那SuperPoint也有这个缺陷吗？
  - 