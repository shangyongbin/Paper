# Optical flow

## 1. 什么是光流

- 给定两帧图像，每个像素点的运动矢量就是光流。（视频图像的一帧中的代表同一对象(物体)像素点移动到下一帧的移动量，使用二维向量表示）

  ![image-20210831162207301](D:\workspace\Paper\Image Matching\Prerequisites\optical-flow.assets\image-20210831162207301.png)

  <video src="D:\workspace\Paper\Image Matching\Prerequisites\optical-flow.assets\光流估计.mp4"></video>

- 根据是否选取图像稀疏点进行光流估计，可以将光流估计分为稀疏光流和稠密光流

  <video src="D:\workspace\Paper\Image Matching\Prerequisites\optical-flow.assets\分类.mp4"></video>

  稠密光流描述图像每个像素向下一帧运动的光流，为了方便表示，使用不同的颜色和亮度表示光流的大小和方向。

  ![img](https://pic1.zhimg.com/80/v2-41b28db5360814f6cd68be9827755e00_720w.jpg)

- 

