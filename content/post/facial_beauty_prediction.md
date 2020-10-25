---
title: Facial Beauty Prediction
date: 2019-11-18 20:46:21
tags: 
- ML
- 论文复现
categories: 学习笔记
---
人工智能课程概论作业——论文复现
期末汇报存档
<!--more-->
## 1 简介

### 1-1 论文简介

&nbsp;&nbsp;&nbsp;&nbsp;[SCUT-FBP5500: A Diverse Benchmark Dataset for Multi-Paradigm Facial Beauty Prediction](https://arxiv.org/abs/1801.06345)是华南理工大学的[人机智能交互实验室](http://www.hcii-lab.net/)在2018年1月发表的论文，以下将Facial Beauty Prediction简称为FBP。FBP是一个值得关注的视觉识别问题，其目的是对人脸的吸引力作出与人类感知一致的预测。在以往的研究中，大多数FBP基准数据集都是在特定的约束下建立的，这会限制模型的性能以及灵活性。该论文提出了一个不同的数据集SCUT-FBP5500，来实现多范式的FBP——基于人脸特征向量的FBP、基于端到端特征学习模型的FBP等。

### 1-2 项目简介

&nbsp;&nbsp;&nbsp;&nbsp;该项目是对论文中本人感兴趣的部分内容进行复现，实现目标为可以对任意输入的人脸照片进行颜值评估并输出分数。本项目存放至[Github-FacialBeautyPrediction](https://github.com/hishark/FacialBeautyPrediction)，对整个学习摸索过程以及复现过程进行了存档。

## 2 数据集

&nbsp;&nbsp;&nbsp;&nbsp;SCUT-5500由5500张正脸人像照片组成，其中包括2000个亚洲女性、2000个亚洲男性、750个白种女性以及750个白种男性。照片的来源主要是互联网，亚洲人的照片大部分来源于[数据堂](datatang.com)，白种人的照片大部分来源于[10k US Adult Faces Database ](https://wilmabainbridge.com/facememorability2.html)。对照片的评分共由60个人完成，每个人都对5500张照片进行了颜值打分，最后得到了330000个分数，分数区间处于[1,5]。

&nbsp;&nbsp;&nbsp;&nbsp;有意思的是这60个人很有可能都是华南理工大学的学生和教职工，从另一个层面来看，根据这个数据集训练出来的模型很大程度上反应了华南理工大学师生对人脸的喜好。

<img src="https://i.loli.net/2020/03/06/t8GedRIl5nYWVP4.jpg" style="zoom: 35%;" />

## 3 数据分析

### 3-1 平均得分

&nbsp;&nbsp;&nbsp;&nbsp;经过60个人的评分最终得到了330000个分数，对每张照片的所有得分取平均求出每张照片的平均得分作为最终得分。

<img src="https://i.loli.net/2020/03/06/DWQ417PfTuM32Hn.png" style="zoom:33%;" />

### 3-2 异常值

&nbsp;&nbsp;&nbsp;&nbsp;遍历所有人脸得分，若发现有评分与平均分相差2分以上，就将该评分视为异常值，并进行剔除。整个数据集中的异常值占比如以下表格所示。

&nbsp;&nbsp;&nbsp;&nbsp;从表格中可以看出，异常值相较于总数目来说非常少，所以剔除异常值后造成的影响可忽略不计。

|    子集    | 白种女性 | 白种男性 | 亚洲女性 | 亚洲男性 |
| :--------: | :------: | :------: | :------: | :------: |
| 打分总数目 |  45000   |  45000   |  120000  |  120000  |
| 异常值数目 |   143    |   181    |   356    |   497    |
| 异常值占比 |   0.3%   |   0.4%   |   0.3%   |   0.4%   |

### 3-3 分数分布

&nbsp;&nbsp;&nbsp;&nbsp;由于数据集中的异常值占比较小，原始数据和预处理数据的分布基本相似，因此分别使用剔除了异常值的四个子集数据来可视化SCUT-FBP5500数据集的分数分布，如下图所示。

&nbsp;&nbsp;&nbsp;&nbsp;可以看到有超过一半的照片评分都在2～3分这个路人阶段，1～2分和4～5分的极端情况占比较小。
<center><img src="https://i.loli.net/2020/03/06/bFD5uPBQdZrgJOK.png"  style="zoom: 40%;" /><img src="https://i.loli.net/2020/03/06/6CpdnPIEFb2w8MS.png"  style="zoom: 40%;" /><img src="https://i.loli.net/2020/03/06/k3gX9PoZ4VDAIuC.png" style="zoom: 40%;" /><img src="https://i.loli.net/2020/03/06/pDFdHn5PIj8OhEV.png"  style="zoom: 40%;" /></center>



### 3-4 人脸特征向量提取

&nbsp;&nbsp;&nbsp;&nbsp;使用人脸识别库[Face Recognition](https://github.com/ageitgey/face_recognition/)从人脸照片中提取到128维的人脸特征向量如下：

```python
feature_vector =
  [-5.35460114e-02,  1.04834020e-01,  5.82005121e-02, -6.23208508e-02,
   -1.20127812e-01,  1.96827948e-03, -5.26909046e-02, -1.48328632e-01,
   1.40360817e-01, -1.83582366e-01,  2.92252243e-01, -4.40107957e-02,
   ......           ......           ......          ......
   6.61701858e-02,  8.83736014e-02,  1.50460765e-01,  4.80800048e-02,
   2.50568688e-02, -4.27672938e-02, -2.44506165e-01, -5.89822307e-02,
   6.45350441e-02, -4.25964147e-02,  5.43840826e-02, -5.32909557e-02]
```

## 4 模型

&nbsp;&nbsp;&nbsp;&nbsp;本论文共训练了两类模型来进行颜值预测，其中包括浅层预测与深层预测。浅层预测使用了三种浅层机器学习模型——线性回归模型、高斯回归模型、支持向量回归模型。深层预测使用了三种卷积神经网络——AlexNet、ResNet18、ResNext50。

### 4-1 浅层预测

#### 4-1-1 模型训练 

&nbsp;&nbsp;&nbsp;&nbsp;浅层预测部分主要使用了[scikit-learn](https://scikit-learn.org/)库中的[LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html?highlight=linearregression#sklearn.linear_model.LinearRegression)、[GaussianProcessRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.GaussianProcessRegressor.html)和[SVR](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVR.html)来训练三个回归模型，使用10折交叉验证来训练、验证模型，将所有的数据集等分成10份，不重复地每次取其中1份做测试集，其他9份做训练集来训练模型。

#### 4-1-2 模型性能分析

&nbsp;&nbsp;&nbsp;&nbsp;在每次交叉验证时都计算出皮尔逊相关系数（PC）、平均绝对误差（MAE）、均方根误差（RMSE）来衡量模型的性能，经过10次交叉验证后，将10次计算的PC、MAR、RMSE取平均数得到最后的值。

&nbsp;&nbsp;&nbsp;&nbsp;对数据集的四个子集——亚洲女性（AF）、亚洲男性（AM）、白种女性（CF）、白种男性（CM）通过10折交叉验证后计算了PC、MAE、RMSE的平均值如下表所示。

<img src="https://i.loli.net/2020/03/06/fknPwC3WNSzQOlR.png" style="zoom:50%;" />

&nbsp;&nbsp;&nbsp;&nbsp;对整个数据集通过10折交叉验证后计算了PC、MAE、RMSE的平均值如下表所示。可以看到支持向量回归模型是三种回归模型中表现最好的模型，相关系数最高，误差最小。

<img src="https://i.loli.net/2020/03/06/hVBxHwfLjIEoNZd.png" style="zoom: 37%;" />

#### 4-1-3 实际得分VS预测得分

&nbsp;&nbsp;&nbsp;&nbsp;对测试集进行测试时，将预测得分记录下来与实际得分进行对比，得到三个回归模型的得分折线对比图如下。橙线为预测得分的折线，蓝线为实际得分的折线，可以看到预测效果还是不错的。

<center><img src="https://i.loli.net/2020/03/06/QIN8XjvT5Votxq9.png" style="zoom: 25%;" /><img src="https://i.loli.net/2020/03/06/I8iD3jGRl5XgZWB.png" style="zoom: 25%;" /><img src="https://i.loli.net/2020/03/06/N6jTh4sF8xHcLSD.png" style="zoom: 25%;" /></center>

### 4-2 深层预测

&nbsp;&nbsp;&nbsp;&nbsp;本项目使用到的caffe深度学习框架需要使用CUDA进行GPU加速，同时CUDA只支持Nvidia图形卡，由于我电脑的图形卡不是N卡，只能使用CPU，所以无法使用GPU进行模型训练，耗费时间过长，故直接使用作者已训练好的模型进行5折交叉验证。

<img src="https://i.loli.net/2020/03/06/jgwDlrIGQK5AOJN.png" style="zoom: 30%;" />

#### 4-2-1 模型性能分析

&nbsp;&nbsp;&nbsp;&nbsp;与浅层预测略有不同，在深度预测中，使用5折交叉验证对测试集进行验证。图片减去均值后，再进行训练和测试，会提高速度和精度。这里通过caffe自带的用于计算平均值的c++接口对每次交叉验证的测试集计算平均值，并保存为一个均值文件，在之后的测试中可以直接使用这个均值来相减，而不需要对测试图片重新计算。

&nbsp;&nbsp;&nbsp;&nbsp;将5次交叉验证得到的PC、MAE、RMSE取平均值得到最终的结果，可以看到三个不同结构的卷积神经网络中表现最好的为**ResNeXt-50**——皮尔逊相关系数最高，误差最小。

|       PC       |    1     |    2     |    3     |    4     |    5     |  平均值  |
| :------------: | :------: | :------: | :------: | :------: | :------: | :------: |
|    AlexNet     |   0.87   |   0.86   |   0.87   |   0.87   |   0.85   |   0.86   |
|   ResNet-18    |   0.88   |   0.88   |   0.89   |   0.88   |   0.90   |   0.89   |
| **ResNeXt-50** | **0.90** | **0.91** | **0.89** | **0.90** | **0.91** | **0.90** |

|      MAE       |    1     |    2     |    3     |    4     |    5     |  平均值  |
| :------------: | :------: | :------: | :------: | :------: | :------: | :------: |
|    AlexNet     |   0.27   |   0.25   |   0.27   |   0.26   |   0.27   |   0.27   |
|   ResNet-18    |   0.24   |   0.26   |   0.24   |   0.25   |   0.24   |   0.25   |
| **ResNeXt-50** | **0.23** | **0.22** | **0.23** | **0.21** | **0.23** | **0.22** |

|      RMSE      |    1     |    2     |    3     |    4     |    5     |  平均值  |
| :------------: | :------: | :------: | :------: | :------: | :------: | :------: |
|    AlexNet     |   0.35   |   0.33   |   0.36   |   0.34   |   0.37   |   0.35   |
|   ResNet-18    |   0.32   |   0.33   |   0.33   |   0.31   |   0.31   |   0.32   |
| **ResNeXt-50** | **0.30** | **0.31** | **0.30** | **0.28** | **0.29** | **0.30** |

## 5 颜值打分

&nbsp;&nbsp;&nbsp;&nbsp;至此已经得到了6个训练好的模型，其中包括3个浅层预测模型和3个卷积神经网络模型，从中挑出表现最好的两个模型——支持向量回归模型、ResNeXt-50模型来进行颜值打分。由于数据集仅由亚洲人与白种人组成，故挑选了两个亚洲明星和美国明星的正脸清晰照来作为模型的输入图片。（Typora里数字都能垂直居中，怎么这里就不行了！）

|                           输入图片                           | SVR  | ResNeXt-50 | 最终得分 |
| :----------------------------------------------------------: | :--: | :--------: | :------: |
| <img src="https://i.loli.net/2020/03/06/qRJkUa4mGo57vbt.jpg" width="100" /> | 3.86 |    3.92    | **3.89** |
| <img src="https://i.loli.net/2020/03/06/fpRkXYAuzGJ8jTE.png" width="100" /> | 4.04 |    4.13    | **4.09** |
| <img src="https://i.loli.net/2020/03/06/GV4KEHd3nU1hOty.png" width="100" /> | 3.45 |    3.84    | **3.65** |
| <img src="https://i.loli.net/2020/03/06/ghvxmb8aUuek4t6.png" width="100" /> | 4.11 |    4.27    | **4.19** |
寡姐胜！

## 6 参考

- [SCUT-FBP5500-Database-Release](https://github.com/HCIILAB/SCUT-FBP5500-Database-Release)
- [How Attractive Are You in the Eyes of Deep Neural Network?](https://towardsdatascience.com/how-attractive-are-you-in-the-eyes-of-deep-neural-network-3d71c0755ccc)
- [facial_beauty_prediction](https://github.com/jackhuntcn/facial_beauty_prediction)
