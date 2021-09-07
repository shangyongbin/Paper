# DenserNet: Weakly Supervised Visual Localization Using Multi-Scale Feature Aggregation

## 总结

- weakly supervised



## Motivation

- 像SuperPoint、D2Net等网络的backbone只使用一个特征层，fail to exploit **multi-scale features** from different semantic levels. (DenseNet)
  - This limitation motivates our approach to exploit features from multi-level semantics to improve localization behavior.
- Training a CNN-based method with strong supervision is not efficient and effective enough for generalization.
  - the ground truth correspondences between image pairs are expensive to obtain at the scale required to train a CNN-based method.
  - such supervised priors based on human annotations may not fully capture all relevant features for image representation to train a network.





## Method

### 框架

![image-20210901172210609](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\DenserNet.assets\image-20210901172210609.png)



