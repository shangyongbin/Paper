





## Model

![image-20210911122900808](D:\workspace\Paper\Backbone\backbone.assets\image-20210911122900808.png)

以`VGG16`为例。

|   name    | ksize | stride | padding | **channel** |       size       | params | memory(B) |
| :-------: | :---: | :----: | :-----: | :---------: | :--------------: | :----: | :-------: |
|  `input`  |       |        |         |      3      | $224 \times 224$ |        |   150K    |
| `conv1_1` |   3   |   1    |    1    |     64      |                  |  1.7K  |   3.2M    |
| `conv1_2` |   3   |   1    |    1    |     64      |                  |  36K   |   3.2M    |
| `maxpool` |   2   |   2    |         |             | $112 \times 112$ |        |   0.8M    |
| `conv2_1` |   3   |   1    |    1    |     128     |                  |  73K   |   1.6M    |
| `conv2_2` |   3   |   1    |    1    |     128     |                  |  147K  |   1.6M    |
| `maxpool` |   2   |   2    |         |             |  $56 \times 56$  |        |   0.4M    |
| `conv3_1` |   3   |   1    |    1    |     256     |                  |  294K  |   0.8M    |
| `conv3_2` |   3   |   1    |    1    |     256     |                  |  589K  |   0.8M    |
| `conv3_3` |   3   |   1    |    1    |     256     |                  |  589K  |   0.8M    |
| `maxpool` |   2   |   2    |         |             |  $28 \times 28$  |        |   0.2M    |
| `conv4_1` |   3   |   1    |    1    |     512     |                  |  1.1M  |   0.4M    |
| `conv4_2` |   3   |   1    |    1    |     512     |                  |  2,3M  |   0.4M    |
| `conv4_3` |   3   |   1    |    1    |     512     |                  |  2,3M  |   0.4M    |
| `maxpool` |   2   |   2    |         |             |  $14 \times 14$  |        |   0.1M    |
| `conv5_1` |   3   |   1    |    1    |     512     |                  |  2,3M  |   0.1M    |
| `conv5_2` |   3   |   1    |    1    |     512     |                  |  2,3M  |   0.1M    |
| `conv5_3` |   3   |   1    |    1    |     512     |                  |  2,3M  |   0.1M    |
| `maxpool` |   2   |   2    |         |             |   $7 \times 7$   |        |    25K    |
|   `fc1`   |       |        |         |    4096     |   $1 \times 1$   | 102.7M |   4096    |
|   `fc2`   |       |        |         |    4096     |                  | 16.7M  |   4096    |
|   `fc3`   |       |        |         |    1000     |                  |   4M   |   1000    |
|           |       |        |         |             |                  |        |           |
|  `total`  |       |        |         |             |                  | ~138M  |   ~15M    |

```txt
INPUT: [224x224x3]        memory:  224*224*3=150K   weights: 0
CONV3-64: [224x224x64]  memory:  224*224*64=3.2M   weights: (3*3*3)*64 = 1,728
CONV3-64: [224x224x64]  memory:  224*224*64=3.2M   weights: (3*3*64)*64 = 36,864
POOL2: [112x112x64]  memory:  112*112*64=800K   weights: 0
CONV3-128: [112x112x128]  memory:  112*112*128=1.6M   weights: (3*3*64)*128 = 73,728
CONV3-128: [112x112x128]  memory:  112*112*128=1.6M   weights: (3*3*128)*128 = 147,456
POOL2: [56x56x128]  memory:  56*56*128=400K   weights: 0
CONV3-256: [56x56x256]  memory:  56*56*256=800K   weights: (3*3*128)*256 = 294,912
CONV3-256: [56x56x256]  memory:  56*56*256=800K   weights: (3*3*256)*256 = 589,824
CONV3-256: [56x56x256]  memory:  56*56*256=800K   weights: (3*3*256)*256 = 589,824
POOL2: [28x28x256]  memory:  28*28*256=200K   weights: 0
CONV3-512: [28x28x512]  memory:  28*28*512=400K   weights: (3*3*256)*512 = 1,179,648
CONV3-512: [28x28x512]  memory:  28*28*512=400K   weights: (3*3*512)*512 = 2,359,296
CONV3-512: [28x28x512]  memory:  28*28*512=400K   weights: (3*3*512)*512 = 2,359,296
POOL2: [14x14x512]  memory:  14*14*512=100K   weights: 0
CONV3-512: [14x14x512]  memory:  14*14*512=100K   weights: (3*3*512)*512 = 2,359,296
CONV3-512: [14x14x512]  memory:  14*14*512=100K   weights: (3*3*512)*512 = 2,359,296
CONV3-512: [14x14x512]  memory:  14*14*512=100K   weights: (3*3*512)*512 = 2,359,296
POOL2: [7x7x512]  memory:  7*7*512=25K  weights: 0
FC: [1x1x4096]  memory:  4096  weights: 7*7*512*4096 = 102,760,448
FC: [1x1x4096]  memory:  4096  weights: 4096*4096 = 16,777,216
FC: [1x1x1000]  memory:  1000 weights: 4096*1000 = 4,096,000
 
TOTAL memory: 15M * 4 bytes ~= 60MB / image (only forward! ~*2 for bwd)
TOTAL params: 138M parameters
```

- Most **memory** is in early CONV: conv1
- Most **params** are in late FC



