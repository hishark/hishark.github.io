---
title: Introduction to Deep Learning
date: 2018-07-20 15:42:35
tags: 
- Deep Learning
categories: 学习笔记
authors:
- hishark777
---
暑假好忙啊又要复习又要自学新东西OTZ
btw Ng讲话真的好温柔啊哈哈哈
<!--more-->
我也不知道读研学啥啊，全民AI搞得我很懵噢反正先自学一下吧。
吴恩达的课都说看看入门蛮好，网易云课堂只有视频没法做测试题，然后就去coursera上申请了一下助学金> <
* [Deep Learning课程地址](https://www.coursera.org/specializations/deep-learning)

边看视频边做了点笔记，省得学完又忘了个一干二净(oﾟvﾟ)ノ
<p align="right">*笔记内容全部来自吴恩达课程视频 本人仅做整理*</p>
#### What is a neural network?

coursera还提供了pdf和ppt啊贼贴心(～￣▽￣)～
* [What is a neural network.ppt](http://p3as6e9rs.bkt.clouddn.com/What%20is%20Neural%20Network.pptx)
* [What is a neural network.pdf](http://p3as6e9rs.bkt.clouddn.com/What%20is%20Neural%20Network.pdf)

##### Example 1 – single neural network 

深度学习一般指的是训练神经网络，那么什么是神经网络？这一节将给你一些它的基本知识。
一个简单的例子——房价预测
![winn-image1](https://user-images.githubusercontent.com/29684201/48275046-98c7a380-e47f-11e8-93c0-550dd7a07ca6.png)

用房子的大小x作为对神经网络的输入，经过小圈输出房价y。
这个小圈也就是一个神经网络中的一个神经元（neuron），就会执行下图画出的函数：
![winn-image2](https://user-images.githubusercontent.com/29684201/48275047-99603a00-e47f-11e8-8e49-1df1f1defb2a.png)

这样一个函数我们叫做ReLu函数，意思是线性整流函数（Rectified Linerar Unite）。之后课程会学到。
如果这是一个单一神经元的话，这就是一个非常非常小的神经网络，而一个很大的神经网络是由许多这样的单一神经元叠加在一起组成。

##### Example 2 – Multiple neural network 

假设我们不仅仅根据房屋大小来预测房屋价格，现在有别的特征量用来预测，比如卧室数量，邮政编码，家庭大小，街区富裕程度，学校质量好坏……
![winn-image3](https://user-images.githubusercontent.com/29684201/48275049-99603a00-e47f-11e8-99dd-44e43f866179.png)

Ng画的每一个小圈都可以是这些ReLU函数或者别的非线性函数中的一个，所以房子要花多少钱取决于购买者看重什么东西，所有的这些都能帮助你预测房价。

在这个例子中，x是所有输入，y是试图预测的价格，所以通过堆叠一些单一神经元，我们可以得到一个稍大的神经网络。
![winn-image4](https://user-images.githubusercontent.com/29684201/48275051-99f8d080-e47f-11e8-9bc0-03d41f4fc810.png)

那么如何管理神经网络呢？就是说当你实现（搭建）它的时候，你只需要给它你训练集中的大量的例子的输入x以及对应的输入y，而所有这些在中间的东西他们（神经网络）将会自己搞清楚。
![winn-image5](https://user-images.githubusercontent.com/29684201/48275052-99f8d080-e47f-11e8-93cd-9ca92046ce37.png)

所以实际要做的是这个：
![winn-image6](https://user-images.githubusercontent.com/29684201/48275054-9a916700-e47f-11e8-85e5-6db0c03aec4d.png)

给定四个输入，神经网络的工作就是预测价格y，这里的每个小圆圈都叫做神经网络中的隐藏神经元，其中的每一个神经元都将所有的四个特征当作输入。

左边这一层称为输入层，中间层是全连接的，因为每一个输入特征(参数)都会连接中间层的每一个节点。

神经网络最重要的一点就是只要给定足够多的训练示例x和y，神经网络就能很好地拟合出一个函数来建立x和y之间的映射关系。

这就是最基本的神经网络。实际上当你建造了你自己的神经网络之后，你将发现他们在监督学习中是最有用、最强大的，所谓监督学习就是需要把一个输入x和一个输出y相对应起来，就像上面的房屋价格预测示例。

#### Supervised Learning with Neural Networks

* [Supervised Learning with Neural Networks.ppt](http://p3as6e9rs.bkt.clouddn.com/Supervised%20Learning%20with%20Neural%20Networks.pptx)
* [Supervised Learning with Neural Networks.pdf](http://p3as6e9rs.bkt.clouddn.com/Supervised%20Learning%20with%20Neural%20Networks.pdf)

到目前为止，几乎所有通过神经网络创造的经济价值都是利用了其中一种机器学习方式——监督学习。在监督学习中，你有一些输入x，并且你想通过x学习到一个函数，这个函数能够将x映射到输出y。

#####  Some examples of supervised learning

比如说现在我们有一个预测房价的应用软件，它可以根据你输入的房屋特征去估计房屋的售价。
![slwnn-img1](https://user-images.githubusercontent.com/29684201/48275056-9a916700-e47f-11e8-98bb-057bbfb96957.jpg)

目前最有利可图的深度学习应用就是在线广告。在在线广告应用当中，根据用户在网站上的输入信息及用户的一些其他信息向你展示与用户信息相关的广告，神经网络已经能够很好地预测用户是否会点击某一个广告。
![slwnn-img2](https://user-images.githubusercontent.com/29684201/48275058-9b29fd80-e47f-11e8-9da6-963dcec64c9b.jpg)

机器视觉在过去的几年里飞速发展，这几乎都归功于深度学习技术。你也许会输入一张图片，并且想得到一个索引，例如说索引范围为1到1000，每个索引都代表了一种图片，共有1000种不同的图片，你也许会用它来标记照片类别以便分类管理。
![slwnn-img3](https://user-images.githubusercontent.com/29684201/48275059-9b29fd80-e47f-11e8-8237-6eb3cad33bff.jpg)

语音识别目前的进展情况也是非常令人兴奋的，当你输入一段语音给神经网络时，它能够自动将语音转化为文本。
![slwnn-img4](https://user-images.githubusercontent.com/29684201/48275061-9bc29400-e47f-11e8-902b-475d81ad0b4b.jpg)

归功于深度学习技术，机器翻译也向前迈出了一大步。你可以给神经网络输入一个英文句子，并且直接输出英文段落的翻译结果，例如输出对应的中文段落。
![slwnn-img5](https://user-images.githubusercontent.com/29684201/48275062-9bc29400-e47f-11e8-9c8c-626540d71de8.jpg)

在自动驾驶技术中，你可能可以输入一幅包含了车辆前方的信息的图像，又或再加上一些雷达扫描信息，神经网络基于这些信息经过训练后就能够告诉你路面上其他汽车的位置信息。所以神经网络成为了自动驾驶技术的关键组成部分。
![slwnn-img6](https://user-images.githubusercontent.com/29684201/48275063-9bc29400-e47f-11e8-9c8a-cd92bc128c29.jpg)

很多有价值的发明都是通过神经网络在特定问题下来巧妙地建立x对应y的函数映射关系，并且通过监督学习拟合数据，成为某个复杂系统的一部分，例如自动行驶的交通工具。事实证明结构稍有不同的神经网络在不同的应用领域都非常的有用。

在预测房价和在线广告里用的都是相对标准的神经网络结构，就像上一节看到过的那样；在图像应用中我们常常将卷积结构放在神经网络结构当中，简称为CNN；而在序列化数据中比如说音频，是时序组成的数据。音频需要完整的播放才能表达其意，所以 一维时间序列或一维时序序列最能代表音频的数据结构。在这种序列化数据中常常用到RNN（循环神经网络）。语言比如英语和中文（字母或汉字）都在序列化数据中有自己出现的时序，所以语言也能够被表现为序列化数据。并且更复杂版本的RNNs 经常用到上述的应用当中；而更复杂的应用像自动驾驶技术，当你去识别图像内容时，需要对卷积神经网络CNN的结构和雷达信息有更多的改进，直至定义出更加复杂、混合着其他结构的神经网络结构。
![slwnn-img7](https://user-images.githubusercontent.com/29684201/48275065-9c5b2a80-e47f-11e8-8f43-84db1c563f80.jpg)

##### Different types of neural network

所以这些应用只是将标准的CNN和RNN结构更加的具体化。你可能会看到这样的图像。如最左边的图片所示，这是标准的神经网络结构。如中间的图片所示，这是一个卷积神经网络的例子，卷积神经网络经常用于图像数据的处理。如最右边的图片所示，这是一个循环神经网络，循环神经网络可以很好的表现一维序列化数据。
![slwnn-img8](https://user-images.githubusercontent.com/29684201/48275066-9c5b2a80-e47f-11e8-8942-19cffdaa0c85.jpg)

##### Structured vs unstructured data

机器学习能够应用在结构化和非结构化数据中。

结构化数据是基于数据库的数据。举个例子，在房价预测中，你也许会有一个数据库或列表，它将告诉你房屋面积和卧室数量等信息，这就是结构化数据。又或在预测用户是否会点击某一个广告时，你会有关于这个用户的信息、关于这则广告的信息和一些标签来帮助你进行预测，这也是结构化数据。意思是每一个特征，例如房屋面积、卧室数量、用户年龄等它们都有清晰的定义。
![slwnn-img9](https://user-images.githubusercontent.com/29684201/48275067-9cf3c100-e47f-11e8-8de1-fe1f64d987a7.jpg)

相对来说，非结构化数据则是类似于音频、图片或文本这种数据，这里的特征也许是图片中的像素值或一段文本中的独立单词。历史上对于非结构化数据的学习常常比对结构化数据的学习要困难得多。在神经网络崛起后 最令人兴奋的事情之一就是它以及它所带来的深度学习使得计算机能够比以前更好地解释非结构化数据。
![slwnn-img10](https://user-images.githubusercontent.com/29684201/48275068-9cf3c100-e47f-11e8-8e04-7f02746a82ad.jpg)

#### Why is Deep Learning taking off?

* [Why is Deep Learning taking off.ppt](http://p3as6e9rs.bkt.clouddn.com/Why%20is%20Deep%20Learning%20taking%20off.pptx)
* [Why is Deep Learning taking off.pdf](http://p3as6e9rs.bkt.clouddn.com/Why%20is%20Deep%20Learning%20taking%20off.pdf)

##### Answer

让我们先来画个坐标图，横坐标表示在某个任务上我们拥有的数据量，纵坐标表示学习算法的性能，比如垃圾邮件分类器的准确率、广告点击预测的准确率 或者对于自动驾驶来说探测其他车子位置的准确率。
![widlto-img1](https://user-images.githubusercontent.com/29684201/48275070-9d8c5780-e47f-11e8-881f-5ab65f7586e4.png)

如果将传统的学习算法，比如支持向量机或者逻辑回归这些算法的性能来作为数据量的函数来作图，或许会得到红色的曲线。这个曲线刚开始性能逐渐上升，当加入越多的数据后性能逐渐地趋于平坦，他们不知道该拿大规模的数据怎么办。而使用神经网络，如果训练一个小型的神经网络，那么它的性能也许看起来像黄色的曲线。如果训练一个中型的神经网络，它的性能会稍微好些，像蓝色的曲线。如果训练一个非常大的神经网络，它的性能会越来越好，像绿色的曲线。
![widlto-img2](https://user-images.githubusercontent.com/29684201/48275071-9d8c5780-e47f-11e8-89de-d935d09c4863.png)

如果想要达到如此高的性能，需要考虑两件事。首先需要训练足够大的网络。其次需要非常多的数据。所以我们通常说规模驱动深度学习进展。规模不仅仅是神经网络的规模还有数据的规模。

想要达到高性能最可靠的方法是要么训练一个大网络，要么放入更多的数据。这个在一定程度后也会达到瓶颈，因为最终会用光所有数据，或者网络实在太大了以致于训练得花很长时间。

为了让这个示意图更加的准确，在X轴上写上数据量。更准确地来说，这是被标记过的数据量。被标记过的意思是对于训练集，我们同时有输入X和标记Y。
![widlto-img3](https://user-images.githubusercontent.com/29684201/48275072-9e24ee00-e47f-11e8-8765-066034c3e1ff.png)

m用来表示训练集的大小，也就是训练样本的数量。在训练集的左边部分区间里（small training sets），不同算法的排名是不规则的。如果没有很大的数据集，那么自己提取出来的的特征很大程度上决定了算法的性能。所以，很有可能发生这样的事，有人用手工设计好的特征去训练SVM（支持向量机），或在这个很小的训练集上训练一个很大的网络，那么SVM 可能会得到更好的结果。所以，在这个图像左边的这个区域里，不同算法的性能的排名 是不固定的，这个性能更多的是由提取特征的能力和算法的细节而决定。

只有在这个m很大的数据集的区域里，我们会经常看到很大的神经网络的算法性能超过了其他方法。

在最近这次深度学习崛起的早期，主要是靠大量的数据和高效的计算能力，也就是我们训练网络的能力，无论是在CPU还是在GPU上。这个能力的提升让我们前进了很多。有趣的是，很多在算法层面上的创新，使得神经网络能运行得更快。

##### Example - Signmoid->ReLU

举一个例子，神经网络里一个重大的突破就是从sigmoid函数到ReLU函数的迁移。左边的是 signmoid，右边是ReLU。sigmoid函数在机器学习里有一个问题，那就是在箭头所指的这些梯度几乎为0的区域里，学习的进度会变得非常慢。例如当你用梯度下降法的时候，梯度几乎为0，参数会变得非常慢。而当我们换成ReLU函数，全名是修正线性单元（rectified linear unit），对于负输入，梯度为0，而对于所有的正输入，梯度都是1，那么梯度就不会慢慢变成0。结果证明，简单地把sigmoid函数换成ReLU函数使得梯度下降算法的速度提高很多，从而我们可以训练更大的神经网络。
![widlto-img4](https://user-images.githubusercontent.com/29684201/48275073-9e24ee00-e47f-11e8-8e8c-7c5d4b496a0d.png)

##### Iterative

当我们有一个很大的网络和很多的数据的时候，我们需要在合理的时间里去训练。快速计算很重要的另一个原因是训练一个神经网络的过程是一个循环。比如你有一个网络架构的想法，你用代码实现你的想法，之后实验结果将告诉你网络的表现怎么样，这样就可以回过头去修改网络里面的细节，然后重复这个循环。
![widlto-img5](https://user-images.githubusercontent.com/29684201/48275045-98c7a380-e47f-11e8-8ea8-cbc77706e289.png)

当神经网络需要花费很长时间训练的时候，它就会花费很长时间在这个循环里。在这中间，效率会受到很大的影响。比如你可以用10分钟或者最多一天尝试你的一个想法，看看它是否可行，也许，你需要1个月去训练你的网络。当你可以在10分钟或者1天之内得到结果的时候，你可以尝试很多想法。 这会让你更有可能去发现你的网络是否针对你的应用是可行的。快速计算确实会提高你拿到实践结果的速度。

#### QUIZ

做测验的时候有一个选项不理解
- It is faster to train on a big dataset than a small dataset.

去论坛搜了一下，有人问过这个问题，看完助教的回答就懂啦。
> I think your intuition might be that "training" takes longer when there is a lot of data, because the algorithms work faster when there is less data. And this is true. With fewer examples, (a smaller training set), the algorithms are faster.
But, small data sets often do not do a very good job of training a neural network so that it performs well after training when it sees a new sample that is different from the few examples in the training set.
A small data set may train very quickly, but it doesn't learn very much. It will need to be taught over and over again. I mean the training process executes faster with a small data set, but overall training to get good general results will probably be faster with a large data set, even though the actual training passes will execute slower. In other words, the total time spent creating a "good" neural network is reduced when we have a lot of data to train it with. The more data we have, the better the algorithms work!

还有个题目记一下
* Why is an RNN (Recurrent Neural Network) used for machine translation, say translating English to French? 
1. It can be trained as a supervised learning problem.
2. It is strictly more powerful than a Convolutional Neural Network (CNN).
3. It is applicable when the input/output is a sequence (e.g., a sequence of words).
4. RNNs represent the recurrent process of Idea->Code->Experiment->Idea->....

WEEK1结束啦明天开始WEEK2！(●'◡'●)