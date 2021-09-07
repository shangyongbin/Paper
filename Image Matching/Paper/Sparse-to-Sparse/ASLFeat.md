# ASLFeat: Learning Local Features of Accurate Shape and Localization



## Motivation

- `detect-and-describe` 的不足

  - 没有关键点的**属性**（scale、orientation）

     the lack of shape-awareness of feature points for acquiring stronger geometric invariance.

    - handcrafted 【有】

      1. scale/rotation estimation【SIFT、ORB】

      2. affine shape adaptation【 An affine invariant interest point detector】

    - detect-then-describe 【有】

      > build a separate network to regress the shape parameters, then transform the patch inputs before feature descriptions.

      

    - detect-and-describe 【无】

      > no pre-defined keypoint is given and thus previous patch-wise shape estimation becomes inapplicable.

      

    

  - 关键点检测**定位**不准

    the lack of keypoint localization accuracy for solving camera geometry robustly.

    ![image-20210814112703766](D:\workspace\Paper\Image Matching\Paper\Sparse-to-Sparse\ASLFeat.assets\image-20210814112703766.png)



## Related Work



