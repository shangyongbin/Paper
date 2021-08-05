# HPatch

**更新中.../Updating...**

[TOC]



<a name="Contents"></a>

### :hammer: **目录|Table of Content**

- [Repositories related to HPatches](#Repositories)
- [HPatches: Homography-patches dataset](#Dataset)
  - [Patch-based dataset](#Patch)
  - [Full image sequences](#Full)
  - [Pre-computed descriptor](#descriptor)
- [Hpatches-benchmark](#benchmark)
  - [Tasks](#Tasks)
  - [Matching](#Matching)
  - [Verification](#Verification)
  - [Retrieval](#Retrieval)



论文/Paper：[HPatches: A benchmark and evaluation of handcrafted and learned local descriptors](https://arxiv.org/abs/1704.05939)

链接/Link：https://hpatches.github.io/

<img src="D:\workspace\Paper\Dataset\Image Matching\HPatch\README.assets\montage.png" alt="montage" style="zoom: 25%;" />



<a name="Repositories"></a>

### Repositories related to HPatches

[`hpatches-dataset`](https://github.com/hpatches/hpatches-dataset) details about the dataset

[`hpatches-benchmark`](https://github.com/hpatches/hpatches-benchmark) evaluation code

[`hpatches-decriptors`](https://github.com/hpatches/hpatches-descriptors) pre-computed descriptor templates



[返回目录/back](#Contents)



<a name="Dataset"></a>

### HPatches: Homography-patches dataset

<a name="Patch"></a>

#### Patch-based dataset

- 下载链接：[链接下载](http://icvl.ee.ic.ac.uk/vbalnt/hpatches/hpatches-release.tar.gz) | [命令下载](https://github.com/shangyongbin/hpatches-benchmark)

- `data`

  - `hpatches-release`

    - `i_X` (#57): patches extracted from image sequences with viewpoint changes.

      > Each patch has a size of `65x65` pixels.
      >
      > A single `*.png` file contains all the patches extracted from an image stacked along a single column.

      ![patches](D:\workspace\Paper\Dataset\Image Matching\HPatch\README.assets\patches.png)

      - `ref.png` (#1) : reference

        `shape=(Nx65, 65, 3)`

      - `eX.png` (#5, X=1~5) : easy, have little geometric noise

        ![patches_easy](D:\workspace\Paper\Dataset\Image Matching\HPatch\README.assets\patches_easy-1628136975466.png)

      - `hX.png` (#5, X=1~5) : hard, have more geometric noise

        ![patches_hard](D:\workspace\Paper\Dataset\Image Matching\HPatch\README.assets\patches_hard.png)

      - `tX.png` (#5, X=1~5) : `e<h<t`

    - `v_X` (#59): patches extracted from image sequences with viewpoint changes.

<a name="Full"></a>

#### Full image sequences

> we provide the full image sequences that were used, together with the corresponding homographies.
>
> Each image sequence contains a reference image and 5 target images taken under a different illumination and/or, for a planar scenes, a different viewpoint. 
>
> For all images we have the estimated ground truth homography $H$ with respect to the reference (stored in CSV files `H_ref_X` where $X=1,...,5$).

![images](D:\workspace\Paper\Dataset\Image Matching\HPatch\README.assets\images.png)

- 下载链接：http://icvl.ee.ic.ac.uk/vbalnt/hpatches/hpatches-sequences-release.tar.gz
- `data`
  - `hpatches-sequences-release`
    - `i_X`
      - `k.ppm` (#6, k=1~6)
      - `H_ref_k` (#5, k=2~6)
    - `v_X`

<a name="descriptor"></a>

#### Pre-computed descriptor

```
sh download.sh descr       # prints all the currently available baseline pre-computed descriptors
sh download.sh descr sift  # downloads the pre-computed descriptors for sift
```

the pre-computed descriptor files are saved on `./data/descriptors`.



[返回目录/back](#Contents)



<a name="benchmark"></a>

### Hpatches-benchmark

<a name="Tasks"></a>

#### Tasks

| task name      | description                                                  |
| -------------- | ------------------------------------------------------------ |
| `verification` | measures how well a descriptor separates positive from negative pairs of patches |
| `matching`     | measures how well a descriptor matches two images            |
| `retrieval`    | measures how well a descriptor retrieves similar patches from a large collection |

<a name="Matching"></a>

#### Matching

The matching task, does not make use of definition files, since due to its nature there is no need for repeatability enforcement.

<a name="Verification"></a>

#### Verification

For the `verification` task, for each split `X`, we provide 3 files in `./tasks	`:

| file name                     | description                                            |
| ----------------------------- | ------------------------------------------------------ |
| `verif_pos_split-X.csv`       | contains the positive pairs                            |
| `verif_neg_inter_split-X.csv` | contains negative pairs sampled from between sequences |
| `verif_neg_intra_split-X.csv` | contains negative pairs sampled from withing sequences |

Positive pairs:

```txt
s1,t1,idx1,s2,t2,idx2
v_birdwoman,4,251,v_birdwoman,3,251
v_strand,1,1625,v_strand,3,1625
i_salon,0,1100,i_salon,3,1100
i_zion,3,1766,i_zion,0,1766
...
```

Negative pairs:

```txt
s1,t1,idx1,s2,t2,idx2
v_birdwoman,4,251,i_resort,3,204
v_strand,1,1625,i_santuario,3,482
i_salon,0,1100,i_ajuntament,3,544
...
```

- Each pair is defined by the items of the header `s1,t1,idx1,s2,t2,idx2`.

  - `s` represents the sequence
  - `t` the image id from which the patch is extracted (0-5 since in HPatch there are 6 images per sequence)
  - `idx` the index of the patch inside the sequence

  `v_birdwoman,4,251` is 252th patch from the `v_birdwoman` sequence, extracted from the `5th` image.

  `v_birdwoman,0,251` is the same, patch, but extracted from the `ref` image.

<a name="Retrieval"></a>

#### Retrieval

For the retrieval task, we provide two files per split `X` in `./tasks`:

| file name                        | description                            |
| -------------------------------- | -------------------------------------- |
| `retr_queries_split-X.csv`       | contains the queries                   |
| `retr_distractors_split-X-X.csv` | contains the pool with the distractors |

Note that the file contents are slightly different than the ones in the `verification` task:

```txt
s,idx
v_man,841
v_birdwoman,1758
v_coffeehouse,219
i_salon,986
v_yuri,9
i_ajuntament,799
```

since in the retrieval task, only the patches from the `ref` image are used, and thus, there is no need for the `t` index.



[返回目录/back](#Contents)