# [3D Reconstruction](https://www.bilibili.com/video/BV16z411B71m)

> 目标：从单张或多张图像中重构出三维场景的结构信息。

[TOC]

## 摄像机几何

> 用数学描述摄像机如何把三维场景映射为二维图像。

### 针孔摄像机 & 透镜

- **针孔摄像机模型**

  ![image-20210813134638735](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813134638735.png)

  - 后面分析中，分析的是虚拟像平面。

- 相机坐标与像平面坐标的关系

  ![image-20210813135159329](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813135159329.png)

  ![image-20210813135941056](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813135941056.png)

  - 光圈尺寸

    随着光圈减小，成像越来越清晰、越来越暗。— 解决：凸透镜

- **透镜**

  ![image-20210813140402299](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813140402299.png)

  ![image-20210813140435370](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813140435370.png)

- **透镜问题**

  ![image-20210813145504358](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813145504358.png)

  ![image-20210813145546454](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813145546454.png)

  

- 

### 摄像机几何

#### 相机坐标到像素坐标

![image-20210813145839979](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813145839979.png)

![image-20210813145917671](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813145917671.png)

- 问题

  - 三维点到二维像素坐标的变换是线性的吗？

  ![image-20210813150105272](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150105272.png)

  ![image-20210813150201510](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150201510.png)

  ![image-20210813150253561](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150253561.png)

  ![image-20210813150412569](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150412569.png)

- 摄像机偏斜

  ![image-20210813150550393](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150550393.png)

- 总结

  ![image-20210813150644886](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150644886.png)

  ![image-20210813150756729](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813150756729.png)

#### 世界坐标系

![image-20210813151211486](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813151211486-1628838732312.png)

![image-20210813151403166](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813151403166.png)

![image-20210813151605651](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813151605651.png)

![image-20210813151720849](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813151720849.png)

![image-20210813151959116](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813151959116.png)

### 其他摄像机模型

![image-20210813152136183](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813152136183.png)

![image-20210813152217948](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813152217948.png)

![image-20210813152235952](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813152235952.png)

![image-20210813152328052](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813152328052.png)

![image-20210813152337887](D:\workspace\Paper\Image Matching\Baisc Knowledge\3D-Reconstruction.assets\image-20210813152337887.png)



## 摄像机标定

> 如何从图像中估计出摄像机的相关参数。有了这些参数，就能准确计算出三维场景到二维图像的映射。









## 单视图几何

> 空间中的几何元素与相机得到的图像的几何元素的关联关系。
>
> 在有些场合中，仅利用这些关联关系就能重构出场景的三维结构。
>
> 在更多情况下，需要利用双视图或多视图三维重构方法。



### 1. 2D变换



### 2. 影消点、影消线



### 3. 单视图重构







## 三维重建基础与极几何

> 讨论同一个景物的两视图之间的几何关系。

 



## 双目立体视觉系统

> 介绍机器人视觉中常用的双目立体视觉系统的构建与理论。





## 多视图几何

> 介绍如何从多幅图像中恢复出三维场景的结构。



