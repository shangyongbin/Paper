# Backbone

**更新中.../Updating...**

![image-20210907153614078](D:\workspace\Paper\Backbone\README.assets\image-20210907153614078.png)

:star2: 一个学习者的个人理解

:fireworks: 欢迎不同见解与批评

:telephone_receiver: QQ: 3569556717；E-mail: ybshang@foxmail.com



<a name="Contents"></a>

### :hammer: **目录|Table of Content**

- [Videos, Blogs](#Videos-Blogs)

- [Survey,Benchmark and Dataset](#Survey-Benchmark-Dataset)
  - [Survey](#Survey)
  - [Benchmark](#Benchmark)
  - [Dataset](#Dataset)

- [Backbone](#Backbone)
- [Other](#Other)



<a name="Videos-Blogs"></a>

## Videos, Blogs

**B站**

- [吴恩达深度学习](#https://www.bilibili.com/video/BV1FT4y1E74V)

  深度学习基础。

- [李宏毅深度学习](#https://www.bilibili.com/video/BV1Wv411h7kN):star:

  宽度+一定深度。

- [李飞飞cs231n](#https://www.bilibili.com/video/BV1nJ411z7fe)

  经典课程（没看...），这位[UP](https://space.bilibili.com/354943571/?spm_id_from=333.999.0.0)带学。

  独有：网络的参数计算与占用内存分析。

- [跟李沐学AI](https://space.bilibili.com/1567748478/?spm_id_from=333.999.0.0) :star:

  大佬中的大佬。

  分类+检测+分割+NLP。

  讲解比较粗糙，但是大佬的看法才是可遇不可求~

- [霹雳吧啦Wz](https://space.bilibili.com/18161609):star:

  分类+检测，代码讲解非常细致，赞。

- [秋刀鱼的炼丹工坊](https://space.bilibili.com/823532) :star:

  几分钟论文简述，拓宽视野。

  对某篇感兴趣可自行深读。

- [不想读paper](https://space.bilibili.com/24460257)

  几分钟论文简述。

  诶，小姐姐声音真好听~

**油管**

- [First Principles of Computer Vision](https://www.youtube.com/channel/UCf0WB91t8Ky6AuYcQV0CcLw)

  各个领域的传统方法。推荐Introduction。

  [Introduction](https://www.youtube.com/playlist?list=PL2zRqk16wsdoz4eycyq7EmeV2KpE6JN76) **|** [Image Formation | Image Sensing | Binary Images](https://www.youtube.com/playlist?list=PL2zRqk16wsdr9X5rgF-d0pkzPdkHZ4KiT) **|** [Image Processing](https://www.youtube.com/playlist?list=PL2zRqk16wsdorCSZ5GWZQr1EMWXs2TDeu) **|** [Edge Detection | Boundary Detection | SIFT Detector](https://www.youtube.com/playlist?list=PL2zRqk16wsdqXEMpHrc4Qnb5rA1Cylrhx) **|** [Image Stitching | Face Detection](https://www.youtube.com/playlist?list=PL2zRqk16wsdp8KbDfHKvPYNGF2L-zQASc) **|** ....

<a name="Survey-Benchmark-Dataset"></a>

## Survey,Benchmark and Dataset

<a name="Survey"></a>

### Survey



<a name="Benchmark"></a>

### Benchmark





<a name="Dataset"></a>

### Dataset





[返回目录/back](#Contents)



<a name="Backbone"></a>

## Backbone

:heavy_check_mark: **AlexNet** 【2012】

总结：

论文/Paper：http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf

:heavy_check_mark: **VGGNet** 【2014】:star:

总结：VGG block：`3x3 卷积`



论文/Paper：https://arxiv.org/abs/1409.1556

:heavy_check_mark: **GoogLeNet**【2014】:star:

总结：Inception block: `split-transform-merge`

论文/Paper：https://arxiv.org/abs/1409.4842

```txt
Inception_v1（GoogLeNet） https://arxiv.org/abs/1409.4842
Inception_v2（Batch Normalization） https://arxiv.org/abs/1502.03167
Inception_v3 https://arxiv.org/abs/1512.00567
Inception_v4（Inception-ResNet） https://arxiv.org/abs/1602.07261
```

:heavy_check_mark: **ResNet**【2015】:star:

总结：residual block: `skip connection`

论文/Paper：https://arxiv.org/abs/1512.03385

:heavy_check_mark: **ResNeXt** 【2016】

总结：

论文/Paper：https://arxiv.org/abs/1611.05431

:heavy_check_mark: **DenseNet** 【2017】

总结：

论文/Paper：https://arxiv.org/abs/1608.06993

:heavy_check_mark: **SENet**【2018】

总结：引入通道注意力

论文/Paper：https://arxiv.org/abs/1709.01507

:heavy_check_mark: **MobileNet: Efficient Convolutional Neural Networks for Mobile Vision Application** 【2017】

总结：`depthwise seperable convolution`

论文/Paper：https://arxiv.org/abs/1704.04861

```txt
MobileNet_v1 https://arxiv.org/abs/1704.04861
MobileNet_v2 https://arxiv.org/abs/1801.04381
MobileNet_v3 https://arxiv.org/abs/1905.02244
```

[返回目录/back](#Contents)



<a name="Other"></a>

## Other

:heavy_check_mark: **ResNetv2: Identity Mappings in Deep Residual Networks** 【2016】

总结：ResNet为什么有效？—梯度可以直接通过shortcut反传到任意shallow层。

论文/Paper：https://arxiv.org/abs/1603.05027

:heavy_check_mark: **The Shattered Gradients Problem: If resnets are the answer, then what is the question?**【2017】

总结：ResNet为什么有效？—增强了梯度相关。

论文/Paper：

:heavy_check_mark:**Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift** 【2015】

总结：`conv-bn-relu`

论文/Paper：https://arxiv.org/abs/1502.03167



[返回目录/back](#Contents)

