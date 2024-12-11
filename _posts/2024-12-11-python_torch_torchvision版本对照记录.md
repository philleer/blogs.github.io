# Python-Torch-Torchvision版本对照记录

### 本文目录

1. TOC
{:toc}

### 一、torchvision与torch版本对应以及对python版本的要求

| torch | torchvision | python |
| ------------ | ------------ | ------------ |
| main/nightly | main/nightly | >=3.9,<=3.12 |
|   2.5   |   0.20   |    >=3.9,<=3.12   |
|   2.4   |   0.19   |    >=3.8,<=3.12   |
|   2.3   |   0.18   |    >=3.8,<=3.12   |
|   2.2   |   0.17   |    >=3.8,<=3.11   |
|   2.1   |   0.16   |    >=3.8,<=3.11   |
|   2.0   |   0.15   |    >=3.8,<=3.11   |
|   1.13  |   0.14   |   >=3.7.2,<=3.10  |
|   1.12  |   0.13   |    >=3.7,<=3.10   |
|   1.11  |   0.12   |    >=3.7,<=3.10   |
|   1.10  |   0.11   |    >=3.6,<=3.9    |
|   1.9   |   0.10   |    >=3.6,<=3.9    |
|   1.8   |   0.9    |    >=3.6,<=3.9    |
|   1.7   |   0.8    |    >=3.6,<=3.9    |
|   1.6   |   0.7    |    >=3.6,<=3.8    |
|   1.5   |   0.6    |    >=3.5,<=3.8    |
|   1.4   |   0.5    | ==2.7,>=3.5,<=3.8 |
|   1.3   | 0.4.2 / 0.4.3 | ==2.7,>=3.5,<=3.7 |
|   1.2   |   0.4.1  | ==2.7,>=3.5,<=3.7 |
|   1.1   |   0.3    | ==2.7,>=3.5,<=3.7 |
|  <=1.0  |   0.2    | ==2.7,>=3.5,<=3.7 |


### 二、torchaudio与torch版本对应以及对python版本的要求

![image](https://raw.githubusercontent.com/philleer/blogs.github.io/refs/heads/master/images/20241211-torchversion-3.png#pic_center =640x932)


### 三、torch与torchvision和torchaudio以及cuda版本的对应

| torch | torchvision | torchaudio | cuda |
| ------------ | ------------ | ------------ | ------------ |
| 2.5.0  | 0.20.0  | 2.5.0  | 11.8/12.1/12.4 |
| 2.4.1  | 0.19.1  | 2.4.1  | 11.8/12.1/12.4 |
| 2.4.0  | 0.19.0  | 2.4.0  | 11.8/12.1/12.4 |
| 2.3.1  | 0.18.1  | 2.3.1  | 11.8/12.1 |
| 2.3.0  | 0.18.0  | 2.3.0  | 11.8/12.1 |
| 2.2.2  | 0.17.2  | 2.2.2  | 11.8/12.1 |
| 2.2.1  | 0.17.1  | 2.2.1  | 11.8/12.1 |
| 2.2.0  | 0.17.0  | 2.2.0  | 11.8/12.1 |
| 2.1.2  | 0.16.2  | 2.1.2  | 11.8/12.1 |
| 2.1.1  | 0.16.1  | 2.1.1  | 11.8/12.1 |
| 2.1.0  | 0.16.0  | 2.1.0  | 11.8/12.1 |
| 2.0.1  | 0.15.2  | 2.0.2  | 11.7/11.8 |
| 2.0.0  | 0.15.0  | 2.0.0  | 11.7/11.8 |
| 1.13.1 | 0.14.1  | 0.13.1 | 11.6/11.7 |

### 四、参考资料

[1] [vision官方网站https://github.com/pytorch/vision#installation](https://github.com/pytorch/vision#installation)

[2] [audio兼容版本https://pytorch.org/audio/main/installation.html#compatibility-matrix](https://pytorch.org/audio/main/installation.html#compatibility-matrix)

[3] [conda安装时不同版本的指令指南https://pytorch.org/get-started/previous-versions/](https://pytorch.org/get-started/previous-versions/)