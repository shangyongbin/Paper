# CNN基础



更新中...

[TOC]



## 基础知识

`ConvNet`常用范式：`conv-bn-relu [-pooling]`



- VGG

  采用3个$3 \times 3$卷积核代替1个$7 \times 7$卷积核，2个$3 \times 3$卷积核代替1个$5 \times 5$卷积核

  1. 增加了非线性

     如果2次$3 \times 3$卷积间没有非线性激活，那么与1个$5 \times 5$卷积一模一样。而事实上2次$3 \times 3$卷积间有非线性激活，这样比1个$5 \times 5$卷积增加一次非线性激活。

  2. 减少了参数量

     2个$3 \times 3$卷积核参数量为$3 \times 3 + 3 \times 3 =18$，1个$5 \times 5$卷积核参数量$5 \times 5 = 25$。

  为什么参数量少了，性能反而会好了呢？

  > 乍一看，会比较反直观，因为参数多，假设空间就会更大，表达能力有潜力会更大。
  >
  > 仔细一想，和MLP的问题一样：同样参数下，fat、shallow好还是thin、deep好？

  首先，按上述所说，虽然参数更少，但是感受野是一样的，非线性能力更强了

  其次，2次$3 \times 3$卷积是分而治之的思想（reuse of features）：可以理解为先$3 \times 3$卷积提取小特征，然后再$3 \times 3$卷积对小特征进行整合。而1次$5 \times 5$ 卷积是想用更多参数直接1次学到相同的东西。

## 疑问总结

### 关于采样

- 为什么要(下)采样，一直保持原分辨率不好吗？

  > 下采样方式：以前用maxpooling，现在用strided-convolution

  - 根据学姐说法：从语义方面，提取特征是凝练的过程；从内存消耗方面，（无论训练还是测试）前向传播要保留中间结果，一直保持原分辨率会占用很大内存。
  - 感受野的增速是直接和**卷积步长累乘**相关的。

- 池化

  ![image-20210812155212218](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210812155212218.png)

  ![image-20210812155157722](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210812155157722.png)

- 步长卷积



### 关于感受野

[CNN感受野](https://zhuanlan.zhihu.com/p/35708466)

[A guide to receptive field arithmetic for Convolutional Neural Networks](https://blog.mlreview.com/a-guide-to-receptive-field-arithmetic-for-convolutional-neural-networks-e0f514068807)

Understanding the Effective Receptive Field

- 计算

  ![image-20210811165818974](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210811165818974.png)

  - 感受野的增速是直接和**卷积步长累乘**相关的。
    - 想要网络更快速地达到某个感受野尺度，可以让步长大于1的卷积核更靠前
    - 大大增快的网络的推理速度

- 感受野有什么用？

- 感受野与total sampling ratio有什么关系？

  好像没什么关系。

  - total sampling ratio 与最终的feature map大小有关？只在Overfeat中见到过
  - 感受野

- 可视化

  https://github.com/CheungXu/reception_field_visualization

  

### $1 \times 1$卷积作用

- 全连接层的卷积实现

  - 在Overfeat中，使用$1 \times 1$卷积实现MLP，从而不限制输入大小。

  - 在Faster RCNN的官方实现RPN模块中，对proposals的分类和回归源码使用$1 \times 1$卷积实现。

- 降低参数量，且能获得期望维数的输出。

  - GoogLeNet中
    - 使用$1 \times 1, 3 \times 3, 5 \times 5$卷积获得不同大小感受野，拼接起来获得不同尺度特征的融合。
    - 在$3 \times 3, 5 \times 5$卷积中，先使用$1 \times 1$卷积对通道数降维，然后正常卷积对通道数生维，能大幅减少参数量。

  ![image-20210811121451141](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210811121451141.png)

  - 在ResNet中

    先用$1 \times 1$卷积对通道数降维，再普通卷积（使用降维后的通道数），再$1 \times 1$卷积对通道数升维。

    第二种比第一种感受野小。

    ![image-20210811122137953](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210811122137953.png)

- 不同特征层通道数的对齐

  FPN中

  - 上采样，统一大小
  - $1 \times 1$卷积，统一通道数

  ![image-20210811142342040](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210811142342040.png)

- 提取通道关联信息

  

  ![image-20210811141912729](D:\workspace\Paper\Backbone\CNN基础.assets\image-20210811141912729.png)