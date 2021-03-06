---
title: Neural Networks Basics
date: 2018-07-30 20:39:20
tags: 
- Deep Learning
categories: 
- 学习笔记
authors:
- hishark777
---
deadline是第一生产力\*(੭\*ˊᵕˋ)੭\*ଘ
<!--more-->
一直拖到最后两天才开始看视频
一次性看把我给累的OTZ
好费时间啊看视频整理视频文本内容再排个版什么的
没时间搞了还有好多其他事
之后的先搁置着哈哈哈哈等忙完了再学
另外coursera的作业系统真的太棒了(´▽\`ʃ♡ƪ)
<p align="right">*笔记内容全部来自吴恩达课程视频 本人仅做整理*</p>

#### Logistic Regression as a Neural Network

##### Binary Classification

当你实现一个神经网络的时候，一些技巧是非常重要的。

比如，如果你有一个含有m个训练样本的训练集，你可能习惯于用一个for循环来处理这m个训练样本，但当你实现一个神经网络时，你一般想训练整个训练集，但不显式使用for循环来遍历整个训练集。那么，你将在本周看到如何实现这一点。

另外，当你在你的网络中组织计算的时候，经常使用所谓的前向传播以及所谓的反向传播，所以在本周你还将了解到为什么在训练神经网络时，计算可以被组织为一次前向传播过程以及一次反向传播过程。

本周将使用逻辑回归算法作为例子，以使其更容易理解。

逻辑回归是一个二元分类算法，所以让我们从这样一个问题开始。

这里有一个二元分类问题的例子，你也许有一张输入图片，像这样。你希望算法输出一个0或1标签指明图上是不是猫。输出1说明是猫，输出0说明不是猫。
![](https://user-images.githubusercontent.com/29684201/48273322-96634a80-e47b-11e8-96b0-eb5526e64f6a.png)

在这里，我们用符号y来表示输出标签。

让我们先来看一看图像在计算机里是怎么表示的，为了在计算机里保存一幅彩色图像，计算机要存储3个独立的矩阵，分别对应着图像的红、绿、蓝3个颜色通道。
![](https://user-images.githubusercontent.com/29684201/48273400-c6125280-e47b-11e8-8fd9-0d9837a41e44.png)

所以，如果图像大小是64x64，那么你会有3个64x64大小的实数矩阵，分别代表图像的红、绿、蓝3个颜色通道。

为了用向量表示这些像素矩阵，我们将把这些矩阵中的像素值展开为一个向量x作为算法的输入，我们所做的就是按下面方法定义一个与该图像相对应的向量。向量中列出了图像中红、绿、蓝三个通道的像素值。
![](https://user-images.githubusercontent.com/29684201/48273474-feb22c00-e47b-11e8-8fe8-a70a6bc7a70d.png)

如果图像的大小是64x64，那么该向量的维度将会是64x64x3，这就是图像的矩阵包含的元素总数。

在这个例子中，向量的总长度为12288，也就是64x64x3的乘积。我们将用n(x) = 12288来表示输入特征向量x的维度 。并且，有时候为了简化，也会直接用n来表示输入特征向量的维度。

所以，在二元分类问题中，我们的目标是学习到这样的一个分类器： 输入一幅以特征向量x表示的图像，然后预测对应的输出y是1还是0。即这幅图上是猫还是不是猫。

先让我们来罗列出一些符号，这些符号将会在余下课程中陆续用到。单个样本由一对（x,y）表示。其中x是一个n(x)维的特征向量，y是标签，取值为0或1。
![](https://user-images.githubusercontent.com/29684201/48273475-feb22c00-e47b-11e8-994b-507bb696fe93.png)

训练集包含m个训练样本，所以训练集将被写成(x(1),y(1)) 表示第一个样本的输入和输出 (x(2),y(2))代表第二个样本的输入和输出 直到(x(m),y(m))，表示最后一个样本输入和输出。
![bcimg-5](https://user-images.githubusercontent.com/29684201/48273476-feb22c00-e47b-11e8-894c-2d12382977dc.png)

因此将使用小写m代表训练集的样本总数。并且，有时为了强调是表示训练集的样本总数，会写成M=M(train)。

当是测试集时，有时会用m(test)来表示测试集的样本总数。 因此，m(test)等于测试集的样本总数。

最后，为了将所有的训练样本写成更加紧凑的形式，我们将定义一个矩阵，用大写X表示。X定义如下：将训练集中的输入x(1)、x(2)....x(m)取出，按列排列到矩阵X中。

因此，我们将x(1)放在矩阵的第一列中，x(2)放在矩阵的第二列中，直到x(m)。这样，便得到了矩阵X。矩阵M将有m列，m即训练样本的总数，同时矩阵X有n(x)行。
![bcimg-6](https://user-images.githubusercontent.com/29684201/48273477-ff4ac280-e47b-11e8-881b-9b16acfd6eff.png)

概括一下，X是一个n(x)乘m维的矩阵。在Python中，你会看到X.shape命令，这是Python里得到矩阵形状的命令。
![bcimg-7](https://user-images.githubusercontent.com/29684201/48273478-ff4ac280-e47b-11e8-9611-5e5cb3112ee2.png)

输出是（n(x)，m），这表示X是一个n(x)乘m维的矩阵。

以上就是你如何组织训练样本的输入x到矩阵X。那么如何组织输出标签Y呢，事实证明要使应用神经网络时更简单，同样应该将y按列排列。因此，Y等于[ y(1) y(2) ... y(m) ] 直到y(m)。
![bcimg-8](https://user-images.githubusercontent.com/29684201/48273479-ffe35900-e47b-11e8-90eb-4e75e050a133.png)

Y是一个1xm大小的矩阵，同样的，使用Python命令Y.shape，将会输出(1，m)，表示Y是一个1xm大小的矩阵。

在本课程之后，当你实现你自己的神经网络时 你会发现一个非常有用的惯例：混合不同的训练样本数据（单个x或y），并将它们按列排列，像我们之前对x和y做的那样。

符号指南.pdf

##### Logistic Regression

使用逻辑回归学习算法会得到的输出标签y，y在监督学习问题中全是0或者1，因此这是一种针对二分类问题的算法。给定的输入特征向量 x 和一幅图片对应，我们希望识别这是否是一张猫的图片，因此我们想要一种算法能够输出一个预测值，我们称之为 yhat， 这代表对真实标签 Y 的估计。
![lrimg-1](https://user-images.githubusercontent.com/29684201/48273480-ffe35900-e47b-11e8-8e07-9ab1fdc76a53.png)

形式上讲，yhat是当给定输入特征x时，预测标签 y 为1的概率。换种说法就是当x是一张图片，你想要yhat告诉你这是一张猫图的概率。

x是一个n_x维的向量，约定逻辑回归的参数是w，w也是一个n_x维的向量。另外参数b是一个实数。因此给定了一个输入x以及参数w和b要如何产生输出 yhat 呢？
![lrimg-2](https://user-images.githubusercontent.com/29684201/48273481-007bef80-e47c-11e8-8031-77bfa1a04583.png)

有一种方法可以试试，尽管它不怎么奏效。就是让 yhat 等于 w.T\*x+b ，这是一个线性函数输出。事实上如果使用线性回归，就是这样操作的。但是这对于二分类并不是一个好的算法，因为你希望 yhat 能够输出 y 为1的概率，因此 yhat 的值应该在0和1之间，而这种算法很难实现这个要求，因为w.T\*x+b可能会比1大很多或者是一个负数 这对于概率就失去了意义。
![lrimg-3](https://user-images.githubusercontent.com/29684201/48273482-007bef80-e47c-11e8-8a95-d98362896fbb.png)

所以 让逻辑回归中的输出 yhat  等于对这个值应用sigmoid函数的结果。
![lrimg-4](https://user-images.githubusercontent.com/29684201/48273483-007bef80-e47c-11e8-9e7b-152fad7f0fa8.png)

sigmoid函数如下图，如果水平轴的标签为z，那么函数sigmoid(z)从0平滑地升高到1，然后它会在0.5处和竖直轴交叉。
![lrimg-5](https://user-images.githubusercontent.com/29684201/48273485-01148600-e47c-11e8-8520-35ff60a70623.png)

这里用z表示 (w.T\*x+b) 因此这就是sigmoid(z)函数。 当z是一个实数 sigmoid(z)就等于 1 / ( 1+e^(-z) ) 。
![lrimg-6](https://user-images.githubusercontent.com/29684201/48273472-fe199580-e47b-11e8-905b-92fef1ef8437.png)

如果z非常大，这项会接近1。事实上，如果你看左边的图，如果z非常大，那么sigmoid(z)非常接近1。相反地，如果z非常小 或者他是一个非常大的负值，sigmoid(z) 就会接近0 。
![lrimg-7](https://user-images.githubusercontent.com/29684201/48273473-fe199580-e47b-11e8-96a7-7f6dbb27f022.png)

因此当你实现逻辑回归时，你的目标是尽力学习到参数w和b。因此yhat就能很好地估计y等于1的概率。

你现在已经知道逻辑回归是什么样子了，接下来为了改变参数w和b，需要定义一个代价（成本）函数（cost function），我们将在下一节来讲解。

##### Logistic Regression Cost Function

在之前的视频中，我们学习了逻辑回归模型。为了优化逻辑回归模型的参数W和B，需要定义一个代价函数。现在就来了解一下可以优化逻辑回归的代价函数。

先来回顾一下，我们之前的讲义中用过的这个方程式。
![lrcfimg-1](https://user-images.githubusercontent.com/29684201/48273736-a2034100-e47c-11e8-91b5-31673b959310.png)

为了了解你的模型参数，这里有一组用于优化m参数的示例。
![lrcfimg-2](https://user-images.githubusercontent.com/29684201/48273737-a29bd780-e47c-11e8-9d46-f73e97990eb5.png)

对于优化集合的假定，我们只提出yhat(i)将接近从优化集合中获得的实标（true
label）y_i。

为了更详细地描述上诉方程式，我们已经提及yhat已经在之前为优化示例进行了设置。我们使用上标圆括号标注索引，区分示例。
![lrcfimg-3](https://user-images.githubusercontent.com/29684201/48273738-a3346e00-e47c-11e8-8b01-c7aec01c8f12.png)

所以本课中 我们就使用这个标记法则，上标括号指的是数据 X Y Z以及其他字母与i-th优化示例相关联，也与i-th示例相关，这是括弧里上标i的意义。
![lrcfimg-4](https://user-images.githubusercontent.com/29684201/48273739-a3346e00-e47c-11e8-8dad-0a962a77e3a5.png)

现在我们来学习损失函数（误差函数）-loss(error) function。误差函数可以用来检测算法运行情况，如在算法输出时定义损失 yhat 和实标y有可能是一个或半个平方误差 。
![lrcfimg-5](https://user-images.githubusercontent.com/29684201/48273740-a3cd0480-e47c-11e8-8eed-1c493e68e755.png)

你可以如此操作，但一般在逻辑回归里不进行此操作，因为当研究参数时，我们讨论的优化问题将会变成非凸问题，所以优化问题会产生多个局部最优解。梯度下降算法也就无法找到全局最优解。
![lrcfimg-6](https://user-images.githubusercontent.com/29684201/48273728-a0d21400-e47c-11e8-9374-e5a7dcf41d6d.png)

函数L被称为损失函数，需要进行设定才能在实标为y时对输出值yhat进行检测。在逻辑回归中，我们会设定一个不同的损失函数充当平方误差，这样能产生一个凸象最优问题。将使之后的优化变得更容易。

所以实际要使用的逻辑回归是下图中的损失函数。
![lrcfimg-7](https://user-images.githubusercontent.com/29684201/48273729-a16aaa80-e47c-11e8-9361-8ca8729f37d7.png)

这里说明下为什么这个损失函数有意义。在此逻辑回归损失函数里，我们要让这个数值尽可能小。

为了帮助理解，我们举两个例子。

第一个，我们假定y=1，这也就是要求yhat的数值必须大，却不能大过1，所以yhat值要无限接近1。
![lrcfimg-8](https://user-images.githubusercontent.com/29684201/48273730-a16aaa80-e47c-11e8-9623-fa0a682f09eb.png)

另一个例子是，如果y等于0，就是损失函数会使yhat尽可能变小。
![lrcfimg-9](https://user-images.githubusercontent.com/29684201/48273733-a2034100-e47c-11e8-9528-17a101e6112a.png)

目前有很多函数有拉斐拉效应，也就是，如果y等于1，yhat值要变大。如果y等于0，yhat值要变小，就像上面两个图。这个损失函数被单一的优化示例所定义，它将检测单一优化示例的运行情况。

最后要设定代价函数来检测优化组的整体运行情况。
![lrcfimg-10](https://user-images.githubusercontent.com/29684201/48273734-a2034100-e47c-11e8-8844-3afc90927059.png)

损失函数适用于单一的优化示例，损失函数反映的是你的参数成本。所以在优化逻辑回归模型时，我们要试着去找参数W和B以此来缩小代价函数J的整体成本。

##### Gradient Descent

我们已经讲了逻辑回归模型，讲了如何通过损失函数来界定你的模型对单一样本的训练效果，还讲了代价函数，代价函数可以用来衡量参数w与b在你设计的整个模型中的作用效果。

现在，我们继续来看看如何使用梯度下降模型去训练， 或者去学习，来调整训练集中的参数w和b。 

总的来说，这里有一个我们已经熟悉的逻辑回归算法。
![gdimg-1](https://user-images.githubusercontent.com/29684201/48273864-f1497180-e47c-11e8-9434-c79b835d32cc.png)![gdimg-2](https://user-images.githubusercontent.com/29684201/48273866-f1497180-e47c-11e8-904e-7850137f1af4.png)

在第二行我们看到了代价函数 J 。代价函数J有参数w和b， 并且定义为平均值，计算从1到m的损失函数之和。

损失函数可以衡量你的算法的效果，对每一个训练样例都输出y^(i)，并与每一个训练样例上的真实结果y(i)进行比较。

所以代价函数可以衡量你的参数w和 b在训练集上的效果，要使得参数w和b的设置变得合理，自然地想到要去找到使得代价函数 J(w, b)尽可能小所对应的w和b。

接下来给出梯度下降法(gradient descent)的说明。在这个图中横轴表示你的空间参数w和b，在实践中w可以是更高的维度，但是为了更好地绘图我们定义w和b都是单一实数。代价函数J(w,b)是在水平轴w和b上的曲面，因此曲面的高度就是 J(w,b)在某一点的值。
![gdimg-3](https://user-images.githubusercontent.com/29684201/48273867-f1e20800-e47c-11e8-96a3-db1d6b7b0aec.png)

我们所想要做的就是找到这样的w和b，使得对应的代价函数J值是最小值。我们可以看到代价函数J是一个凸函数(convex function)，像这样的一个大碗。

并且这与下图的函数相反，下图函数是非凸的，并且有很多不同的局部最优。
![gdimg-4](https://user-images.githubusercontent.com/29684201/48273868-f1e20800-e47c-11e8-96f1-9e3bde996023.png)

因此我们的成本函数J(w,b)之所以定义为凸函数，一个重要原因是我们使用这个特殊代价函数J造成的。

为了去找到最优的参数值，我们将会用一些初始值来初始化w和b，通常用0来进行初始化，随机初始化也有效 但是对于逻辑回归我们通常不这么做。因为函数是凸函数，所以无论在哪里初始化，你应该达到同一点或大致相同的点。

梯度下降法以初始点开始，然后朝最陡的下坡方向走一步，因此在梯度下降法一步后，你或许会停在那里，因为它正试图沿着最陡下降的方向走下坡路，这是梯度下降的一次迭代。两次或三次或更多次迭代将收敛到这个全局最优值或接近全局最优值。
![gdimg-5](https://user-images.githubusercontent.com/29684201/48273870-f1e20800-e47c-11e8-9d27-4c86ab7ffa4e.png)

所以这张图片说明了梯度下降模型。为了更好地说明，让我们来看一些函数。

你想要找到J(w)的最小值，可能函数会看起来像这样，为了画起来容易些，我现在忽略b，仅仅是用一维曲线代替多维曲线。
![gdimg-6](https://user-images.githubusercontent.com/29684201/48273852-eee71780-e47c-11e8-87e9-5126d949263d.png)

梯度下降是这样做的，我们将重复执行以下更新的操作，我们更新w的值，使用“:=”表示w进行迭代。
![gdimg-7](https://user-images.githubusercontent.com/29684201/48273855-ef7fae00-e47c-11e8-9440-1b4534bc12bc.png)

在算法收敛之前我会重复这样做。公式中有两点是我要提一下的，首先在这里的α表示学习率(learning rate)，学习率可以控制我们在每一次迭代或者梯度下降法中的步长大小。我们之后将讨论如何选择学习率α。

当我们开始编写代码来实现梯度下降，我们将使用代码中变量名的约定——dw表示导数。
![gdimg-8](https://user-images.githubusercontent.com/29684201/48273856-ef7fae00-e47c-11e8-9fa6-9382de9f9ab0.png)

因此你会像这样编写代码 w:=w-α\*dw(公式如图)。
![gdimg-9](https://user-images.githubusercontent.com/29684201/48273857-f0184480-e47c-11e8-8a1d-1c1fecbaae6a.png)

现在我们确保梯度下降法更新是有意义的。

当w取图中最右端的某个值时，w通过w自身减去学习率乘导数来更新，导数是正的所以每一次从w中减去这个乘积，每一次都向左边走一步 如果在一开始你参数w的值就非常的大的话，像这样梯度下降法会使你的算法渐渐地减小。
![gdimg-10](https://user-images.githubusercontent.com/29684201/48273858-f0184480-e47c-11e8-9a73-c2e502202913.png)

另一个例子，如果w的位置是在左边，导数将会是负的，并且梯度下降法在更新参数时，w将会减去α乘上一个负数，并慢慢地使得参数w增加，所以这样的迭代和梯度下降法会使得参数w逐步变大。
![gdimg-11](https://user-images.githubusercontent.com/29684201/48273860-f0184480-e47c-11e8-9744-54e895178324.png)

无论你初始化的位置是在左边还是右边，梯度下降法都会朝着全局最小值方向移动。

对于上述的梯度下降法，我们写出来的参数中假设只有w。而在逻辑回归中代价函数是一个含有w和b的函数，在这种情况下，梯度下降的内部循环就是这个公式。
![gdimg-12](https://user-images.githubusercontent.com/29684201/48273861-f0b0db00-e47c-11e8-871a-0aefd390ff48.png)

你需要不断重复迭代，这两个等式是你实际迭代更新参数时进行的操作。另外当函数J有两个以上的变量时，我们不使用小写字母d，而使用偏导数符号。
![gdimg-13](https://user-images.githubusercontent.com/29684201/48273863-f0b0db00-e47c-11e8-9b1f-953db501eaed.png)

##### Computation graph

神经网络的计算过程，由正向传播来进行前向计算，来计算神经网络的输出，以及反向传播计算来计算梯度或微分。计算图解释了为什么以这种方式来组织。

在这个视频中，我们来看一个例子。为了演示计算图，我们用一个简单的逻辑回归或单层神经网络。我们试图计算一个函数J 它有三个变量a，b和c ，函数为3(a+bc)。
![cgimg-1](https://user-images.githubusercontent.com/29684201/48273990-4a190a00-e47d-11e8-8d61-25b86e087183.png)

计算这个函数分为三个步骤，首先你需要计算bc，设bc=u。 然后你需要计算V=a+u，设V=a+u。最后输出则变为J=3V。
![cgimg-2](https://user-images.githubusercontent.com/29684201/48273991-4a190a00-e47d-11e8-99b3-6bf18ebc23bb.png)

接下来我们可以将这三个步骤画作计算图。
![cgimg-3](https://user-images.githubusercontent.com/29684201/48273992-4ab1a080-e47d-11e8-8a43-4afa5e00f66a.png)

当有一些特殊的输出变量时，计算图用起来很方便。我们在这个例子中看到的是从左到右传播，可以计算J的值。在下一节中，我们可以看到从右向左的这个过程，和这个蓝色箭头的过程相反，这会是用于计算导数最自然的方式。
![cgimg-4](https://user-images.githubusercontent.com/29684201/48273993-4ab1a080-e47d-11e8-81a2-f40a6cf6454e.png)

##### Derivatives with a Computation Graph

现在让我们用一个简明的例子说明如何用计算图来计算函数J 的导数，这是一个计算图。
![cgimg-5](https://user-images.githubusercontent.com/29684201/48274079-7fbdf300-e47d-11e8-9a23-aa7f741c7d13.png)

比方说你想计算J对于v的导数，它等于多少呢？也就是说如果我们把v的值改变一点点，J的值将会如何变化呢？

J被定义为3乘以v，现在v等于11，因此如果我们把v提高一点点到11.001，那么J就从目前的33提高到33.003。
![cgimg-6](https://user-images.githubusercontent.com/29684201/48274067-7d5b9900-e47d-11e8-86b7-5e11cd1f6d82.png)

这里我们把v提高0.001，结果J增加了3个0.001。因此J对v的导数等于3，因为J的增量是v增量的3倍。
![cgimg-7](https://user-images.githubusercontent.com/29684201/48274069-7d5b9900-e47d-11e8-8a0b-3e84fb6810eb.png)

用反向传播这个术语来解释的话，如果你想要计算最终输出变量对于v的导数（这也是你通常最关心的变量），我们把这个过程叫做图中的一步反向传播。

现在我们来看另一个例子，dJ/da是什么？换句话说，如果我们增大一点a的值，J的值会如何变化呢。让我们仔细看一下这个例子，现在a=5 我们把它增大到5.001，那么对于v的影响，注意到v=a+u，原来是11，现在增加到11.001。正如我们在之前的例子中看到的那样，J现在从33增加到33.003。我们看到如果a增加0.001，J会增加0.003，那么a的变化会在计算图中向右传播，结果J变成了33.003。因此J增量是a增量的3倍，这意味着J对a的导数为3。
![cgimg-8](https://user-images.githubusercontent.com/29684201/48274070-7df42f80-e47d-11e8-8787-636cb402595a.png)

我们来分解一下这个过程，如果你改变了a，v也会随之改变 ，v改变了，J也会改变。在微积分中这叫做链式法则，a影响v，v影响J，然后当你改变a的时候J的改变量等于改变a时v的改变量乘以改变v时J的改变量。
![cgimg-9](https://user-images.githubusercontent.com/29684201/48274072-7df42f80-e47d-11e8-8d4b-4d206f3a640b.png)

这个小例子展示了如何通过计算dJ/dv，即J关于v的导数，来帮助你计算dJ/da。这是反向传播的另一步。

接下来我要介绍另一种符号惯例，当你写反向传播代码的时候，你真正关心的是你想优化的最终输出变量（在这个例子里是J，也就是计算图中的最后一个节点）， 因此你会做许多关于最终输出变量的导数的计算，即下式。
![cgimg-10](https://user-images.githubusercontent.com/29684201/48274073-7e8cc600-e47d-11e8-9551-72179f168e1f.png)

我们就叫它dvar。你会需要计算做许多关于最终输出变量导数的计算，在这个例子中是J。这会牵涉到许多中间变量，例如a b c u v。

当你在程序中实现的时候，你给这些变量取什么名字呢？在Python中，你可以起一个很长的名字比如dFinalOutputVar/dvar。但这是一个很长的变量名，你可以把这叫做dJdvar。

因为导数都是关于最终输出变量J的， 我想引入一种新的记号，当你在代码中计算这个导数的时候，我们就用变量名dvar来代表这个值。所以dvar在你的代码里就代表最终输出变量对它的导数。
![cgimg-11](https://user-images.githubusercontent.com/29684201/48274075-7f255c80-e47d-11e8-9aeb-bd4d0e0605c1.png)

通过这个计算图，我们介绍了一部分反向传播的知识。我们将继续这个例子。让我们回顾一下，我们通过反向运算得到dv=3（dv只是一个变量名，它代表的其实是dJ/dv），我们已经计算出da=3（同样da也是dJ/da在代码中的变量名）。 我们已经推演了反向传播是如何在这两条边上实现的。
![cgimg-12](https://user-images.githubusercontent.com/29684201/48274076-7f255c80-e47d-11e8-8e2c-10c35fae7918.png)

之后的一张图说明。
![cgimg-13](https://user-images.githubusercontent.com/29684201/48274077-7fbdf300-e47d-11e8-9c4c-e373c116bca0.png)

这个例子里最重要的东西是，当你在计算导数的时候最有效率的方式，是按红色箭头方向从右往左进行计算，这里面将用到非常有用的一个法则——链式法则。

以上就是使用计算图正向从左到右计算代价函数（比如你想优化的J），以及如何反向或从右到左计算导数。

##### Logistic Regression Gradient Descent

在这一节中，我们将讨论在实现逻辑回归时如何计算导数来实现梯度下降。重点在于理解逻辑回归中梯度下降的关键方程。

在这个视频里，我将用计算图来进行计算，我必须承认使用计算图对于逻辑回归的梯度下降来说有些大材小用，但我想通过这种方式让你们熟悉这些想法，希望会对你学习神经网络有所帮助。

现在我们深入探讨逻辑回归的梯度下降， 之前我们建立了这样的逻辑回归方程。
![lrgdimg-1](https://user-images.githubusercontent.com/29684201/48274195-b8f66300-e47d-11e8-822a-e2e8086ed758.png)

预测值yhat的定义如图，z的定义如图， 损失函数L关于这个例子的定义如图。其中a是逻辑回归的输出，y是真实值。我们通过计算图表示它。例如有两个特征x1和x2，为了计算z 我们要输入w1,w2和b，还有特征x1和x2的值 用来计算z。z=w1x1+w2x2+b，接着计算yhat，yhat=a=sigma(z)，最后我们计算L(a,y)。
![lrgdimg-2](https://user-images.githubusercontent.com/29684201/48274196-b8f66300-e47d-11e8-8188-a5000a0047f5.png)

在逻辑回归中，我们要做的就是修改参数w和b来减少损失函数。之前讲正向传播的步骤中 讲了如何计算单个样本的损失函数，现在我们讲讲如何反向计算导数。这是一个整理后的框图。
![lrgdimg-3](https://user-images.githubusercontent.com/29684201/48274197-b98ef980-e47d-11e8-925c-fd6126d9c47b.png)

因为我们要计算关于损失函数的导数，反向传播时，首先要做的是计算损失函数对于a的导数。所以在代码中，你只要用da来表示dL/da，可以得到dL/da=-y/a+(1-y)/(1-a)。 现在已经算出了da的值（最终输出值对a的导数）。
![lrgdimg-4](https://user-images.githubusercontent.com/29684201/48274198-b98ef980-e47d-11e8-8279-0f58dd801cc5.png)


你可以继续往回算出dL/dz，把损失函数显式地写成a和y的函数L(a,y)，或者直接写L也行，用dz来表示dL/dz，可以得到dz=a-y。 这个dL/dz 可以被表示成dL/da乘以da/dz， da/dz可以算出是a(1-a)，所以dL/da的表达式和da/dz的结合起来相乘可以得到结果是a-y。这是链式法则的应用。 
![lrgdimg-5](https://user-images.githubusercontent.com/29684201/48274188-b72c9f80-e47d-11e8-92c0-8b545d3174d0.png)

反向传播的最后一步，是反向算出你需要改变w和b多少。你可以算出L对w1的导数，通常记作dw1，它等于x1乘以dz。同样dw2代表你要改变的w2的值，是x2乘以dz。db等于dz。
![lrgdimg-6](https://user-images.githubusercontent.com/29684201/48274190-b7c53600-e47d-11e8-8ab3-d8fcec55f9fd.png)

所以如果你要对于一个例子进行梯度下降，你需要做如下事情。用公式算出dz，然后算出dw1，dw2和db，然后进行更新。w1=w1-α\*dw1，α代表学习速率，w2也按一样的方式更新，b=b-αdb。
![lrgdimg-7](https://user-images.githubusercontent.com/29684201/48274193-b7c53600-e47d-11e8-94f2-7b8a1117196e.png)

这是一个一步梯度的简单例子，以上介绍了对于一个单一的训练样本如何计算导数和执行逻辑回归的梯度下降。但训练一个逻辑回归模型，你不止有一个样本，而是有m个。 在下一节中我们将谈谈如何应用这些想法到多个训练样本上，而不是单独的一个训练样本。

##### Gradient Descent on m Examples

在之前的课程中，我们学习了怎样计算导数以及怎样实现梯度下降（在只有一个训练样例的逻辑回归情况下）。现在我们来讨论m个训练样例的情况。

我们先回顾一下代价函数J(w,b)。我们关心的J(w,b)是个平均数，1/m乘上i取1到m时的损失函数L的和。
![gdomeimg-1](https://user-images.githubusercontent.com/29684201/48274301-fe1a9500-e47d-11e8-9988-308b90f1cc96.png)

当你的算法输出关于样本y的a^i，你知道a^i是训练样本的预测值，也就是𝜎(z^i)，等于𝜎函数作用于w的转置乘上x^i 加上b。
![gdomeimg-2](https://user-images.githubusercontent.com/29684201/48274304-feb32b80-e47d-11e8-96f4-65cc7e7f1cd5.png)

我们在之前展示的是对任意单个训练样本如何计算导数，当你只有一个训练样本时，dw1、dw2和 db 加上上标 i 表示你求得的相应值。
![gdomeimg-3](https://user-images.githubusercontent.com/29684201/48274305-feb32b80-e47d-11e8-8ca8-45ca1cb630a4.png)

如果你现在在做之前演示的情况，但只使用一个训练样本(x^i,y^i)，全局代价函数对w1的导数也同样是各项损失函数对w1导数的平均值。 
![gdomeimg-4](https://user-images.githubusercontent.com/29684201/48274306-ff4bc200-e47d-11e8-8b98-b5fdb8854007.png)

之前已经演示了如何计算单个训练样本
![gdomeimg-5](https://user-images.githubusercontent.com/29684201/48274307-ff4bc200-e47d-11e8-9eac-d9af6a494b0f.png)

所以你真正需要做的是计算这些导数（dwi）然后求平均，这会给你一个全局梯度值，你能够直接把它实现 到梯度下降法中。
![gdomeimg-6](https://user-images.githubusercontent.com/29684201/48274310-ff4bc200-e47d-11e8-8700-57bb2db0b6a4.png)

我们把这些装进一个具体的算法中，你需要实现的就是使逻辑回归和其中的梯度下降法生效。我们可以初始化J等于0，dw1等于0，dw2等于0，db等于0。
![gdomeimg-7](https://user-images.githubusercontent.com/29684201/48274312-ffe45880-e47d-11e8-9f40-3ce57afc4b7f.png)

我们将要做的是使用一个for循环遍历训练集，同时计算相应的每个训练样本的微分，并把它们加起来。如我们所做的让 i 取1到m，m是训练样本数。这个计算已经假设只有两个特征，所以n等于2。
![gdomeimg-8](https://user-images.githubusercontent.com/29684201/48274313-ffe45880-e47d-11e8-9482-1a3fd3f83248.png)

最终对所有的m个训练样本都进行这个计算后，你还需要除以m，因为我们是在计算平均值。
![gdomeimg-9](https://user-images.githubusercontent.com/29684201/48274314-007cef00-e47e-11e8-835a-2d3b4c54cb55.png)

做完所有这些计算后，你已经计算了代价函数 J 对各个参数w1，w2，和b的导数。

回顾我们正在做的细节，我们使用dw1，dw2和db作为累加器，所以算完这个以后，dw1等于全局代价函数对w1的导数。dw2和db也是一样。
![gdomeimg-10](https://user-images.githubusercontent.com/29684201/48274315-007cef00-e47e-11e8-9b82-4c5452922fce.png)

注意dw1和dw2没有上标 i ，这是因为我们在代码中把它们作为累加器去求取整个训练集上的和。而dzi是对应于单个训练样本的dz，这也就是为什么这里会有个上标 i ，指代对应的第i个训练样本。

完成所有这些计算后实现一步梯度下降来更新w1，即w1减去学习率乘上dw1，而w2更新为w2减去学习率乘上dw2，同时b更新为b减去学习率乘上db。
![gdomeimg-11](https://user-images.githubusercontent.com/29684201/48274316-01158580-e47e-11e8-9452-461acfc23f07.png)

这里dw1，dw2和db都是如之前所说那样计算的，最终这里的 J 也会是你代价函数的正确值。以上所有东西只实现了一步梯度下降，因此你需要重复以上内容很多次，以完成多次梯度下降。

但计算中有两个缺点，如果按照这里的方法实现逻辑回归， 你需要两个for循环，第一个for循环用于遍历m个训练样本，第二个for循环是一个遍历所有特征的for循环。

这个例子中我们只有2个特征所以n等于2并且nx等于2，但如果你有更多特征，你需要编写dw1，dw2以及类似地计算dw_3等等直到dwn。所以将需要一个for循环遍历所有n个特征。

当你实现深度学习算法时，你会发现在代码中显式地使用for循环会使你的算法不够高效。在深度学习时代会有越来越大的数据集，所以不使用显式的for循环来实现你的算法是非常重要的，而且会帮你适用于更大的数据集。

所以这里有一些技术，叫做矢量化技术。它可以帮助你的代码摆脱这些显式的for循环。
![gdomeimg-12](https://user-images.githubusercontent.com/29684201/48274318-01158580-e47e-11e8-8011-2f885306369a.png)

矢量化是有着两面性的，有时候能加速你的代码，有时候也未必。但在深度学习时代，矢量化已经变得相当重要，因为我们越来越多地训练非常大的数据集，因此你需要使代码变得非常高效。

#### Python and Vectorization

##### Vectorization

向量化就是一项让你的代码变得更高效的艺术。在深度学习的实际应用中，你可能会遇到大量的训练数据，因为深度学习算法在这个情况下表现更好。所以你的代码的运行速度非常重要， 如果它运行在一个大的数据集上面，你的代码可能花费很长时间去运行，你将要等待非常长的时间去得到结果。所以在深度学习领域 实现向量化的能力已经变成一个关键的技巧，让我们从一个例子开始。

什么是向量化？ 在逻辑回归中，你需要去计算下式。W是列向量，X也是列向量。
![vimg-1](https://user-images.githubusercontent.com/29684201/48274425-40dc6d00-e47e-11e8-9a7c-4632ab82dfd5.png)

如果你有很多的特征，那么就会有一个非常大的向量，所以W和X是R内的nx维向量。
![vimg-2](https://user-images.githubusercontent.com/29684201/48274426-40dc6d00-e47e-11e8-8910-b05c250e8674.png)

计算WT\*X，这是一个非向量化的实现 你会发现这是真的很慢。
![vimg-3](https://user-images.githubusercontent.com/29684201/48274428-41750380-e47e-11e8-97a2-5ba3b750176d.png)

作为对比，一个向量化的实现将会非常直接计算WT\*X，你将会发现这个非常快。
![vimg-4](https://user-images.githubusercontent.com/29684201/48274429-41750380-e47e-11e8-8084-970b352c55a9.png)

通过实际对比，非向量化版本多花费了300倍向量化版本的时间 。当你正在实现深度学习算法，如果你向量化你的代码，你能快速得到一个返回的结果。

##### More Vectorization Examples

通过内置函数和避免使用显式的for循环来实现向量化可以有效地提高代码的运行速度。让我们再看几个例子，需要记住的经验之谈是当你在编写神经网络或逻辑回归时，都要尽可能避免使用显式的for循环，虽然有时候无法完全避免使用for循环，但如果你能使用内置函数或者找到其他方式来计算你想要的答案，这通常会比直接使用for循环更快。

###### Example 1

左BEFORE,右AFTER
![mveimg-1](https://user-images.githubusercontent.com/29684201/48274537-86009f00-e47e-11e8-8948-5b3aa1af32e5.png)

###### Example 2

BEFORE:
![mveimg-2](https://user-images.githubusercontent.com/29684201/48274539-86009f00-e47e-11e8-9ed7-da23d5235c14.png)

AFTER:
![mveimg-3](https://user-images.githubusercontent.com/29684201/48274541-86993580-e47e-11e8-8a5a-e535de2c8125.png)

##### Vectorizing Logistic Regression

我们已经谈过向量化能够大大地加速你的代码，在本节课中我们会讲讲逻辑回归的向量化实现，使得它们可以被用于处理整个训练集。也就是说可以用梯度下降法的一次迭代来处理整个训练集， 甚至不需要使用任何一个for循环。

首先让我们看看逻辑回归的前向传播，假设我们有m个训练样本，为了预测第一个样本，你需要计算z。并使用z来计算激活函数a。
![vlrimg-1](https://user-images.githubusercontent.com/29684201/48274542-86993580-e47e-11e8-9ccf-04ef74472151.png)

然后预测第二个样本，你需要做同样的计算。然后预测第三个样本，你还需要做这个计算。以此类推，如果你有m个训练样本，你可能需要重复m次。
![vlrimg-2](https://user-images.githubusercontent.com/29684201/48274545-8731cc00-e47e-11e8-9dd0-b3f57970782b.png)

不过为了实现前向传播，即计算出m个训练样本的预测结果，有一种实现方法可以不需要for循环，让我们看看如何做到。

首先回忆一下，我们曾把矩阵X定义为训练的输入值，就像这样排列在不同的列中，这就是一个矩阵，一个nx乘m的矩阵。
![vlrimg-3](https://user-images.githubusercontent.com/29684201/48274546-8731cc00-e47e-11e8-9371-0eac305887ae.png)

构造一个1\*m维的行向量，方便计算z(1)，z(2)...z(m)都是在同一时间内(完成计算) 实际上它可以表达成 W的转置矩阵(W^T)与矩阵X相乘。再加上这个向量 b b b ... 其中这个[b b ... b b]的东西是个1\*m维的向量，或者称为一个1\*m维的矩阵或一个m维的行向量。
![vlrimg-4](https://user-images.githubusercontent.com/29684201/48274549-87ca6280-e47e-11e8-8533-1f7139f78298.png)

所以你得到了另一个1\*m的向量，如果你参照上面的定义，第1个元素就是z(1)的定义，第2个元素就是z(2)的定义等等。
![vlrimg-5](https://user-images.githubusercontent.com/29684201/48274531-84cf7200-e47e-11e8-87fd-bf5ab8184ef3.png)

就如同我们构造X那样，把你的训练样本水平排列在一起，我将把Z定义为把z(1) z(2) ... z(m)们水平排列在一起。
![vlrimg-6](https://user-images.githubusercontent.com/29684201/48274532-84cf7200-e47e-11e8-9ffe-697e62a504e5.png)

所以当你把代表着不同训练样本的x们水平排列在一起，你得到了X。当你用同样的方法把这些z们水平排列在一起，你会得到Z。为了实现这些计算numpy命令为Z=np.dot(W.T,X)+b，其中W.T为W的转置。这里有一个python的精妙的地方，这里b是一个实数，或者说一个1\*1的矩阵，即一个普通的实数。但是当你把这个实数b加到这个向量上的时候，python自动把这个实数b
扩展为一个1\*m的行向量，为了防止你觉得这个运算难以理解，这个在python中叫做广播(broadcasting)。
![vlrimg-7](https://user-images.githubusercontent.com/29684201/48274534-85680880-e47e-11e8-8a5a-623c5527d345.png)

那我们怎么求这些a们的值呢，我们下一步要做的就是找到一个同时求 a(1), a(2), ..., a(m) 的方法，就像把所有x排列在一起可以得到X，把所有z排列在一起可以得到Z，把所有a排列在一起可以得到一个新的变量，我们将它定义为A。将Z作为sigmoid函数的输入值 会非常高效地得到A。
![vlrimg-8](https://user-images.githubusercontent.com/29684201/48274535-85680880-e47e-11e8-966b-2669588ab1c7.png)

综上，我们不需要遍历m个训练样本来一次一次计算z和a，你可以用一行代码来实现同时计算所有的z。以及使用sigmoid函数来同时计算所有的a。这就是如何通过向量化同时实现所有m个训练样本的前向传播。

##### Vectorizing Logistic Regression's Gradient Output

在上一节你已经看到如何通过向量化同时计算出整个训练集的激活值a。在这一节中你将看到如何使用向量化计算全部m个训练样本的梯度。

你也许记得在讲梯度计算时 计算第一个样本的dz_(1)的步骤，即dz^(1)=a^(1)-y^(1)，dz^(2)=a^(2)-y^(2)，以此类推。
![vlrgoimg-1](https://user-images.githubusercontent.com/29684201/48274695-d972ed00-e47e-11e8-8f81-e8e2993d1091.png)

如此对所有m个训练样本进行同样的计算，然后我们可以定义一个新变量dZ=[dz^(1) dz^(2) ... dz^(m)]，注意，所有dz横向排列，所以这是一个1乘m的矩阵，也可以说是一个m维行向量。
![vlrgoimg-2](https://user-images.githubusercontent.com/29684201/48274698-da0b8380-e47e-11e8-919b-152deef93029.png)

回想一下在之前我们已经了解了如何计算A，即A=[a^(1)...a^(m)]，我们也已经定义了Y，即Y=[y^(1) ... y^(m)] ，它们也是横向排列的。
![vlrgoimg-3](https://user-images.githubusercontent.com/29684201/48274700-da0b8380-e47e-11e8-8bb9-0e5c83c7406c.png)

那么基于这些定义，你也许会发现我们可以这样计算dZ，dZ=A-Y，这等同于 dZ=[a^(1)-y^(1), a^(2)-y^(2) ...]。这里的第一个元素a^(1)-y^(1)就是dz^(1)，第二个元素就是dz^(2)等等。所以仅需要一行代码，你就可以同时完成这所有的计算。
![vlrgoimg-4](https://user-images.githubusercontent.com/29684201/48274701-daa41a00-e47e-11e8-85a6-0b2685af0b7f.png)

在之前的实现中，我们已经去掉了一个for循环，但是我们仍然有一个遍历训练集的循环。我们将dw初始化为0向量，但是我们还是需要遍历训练样本。对第一个训练样本计算dw+=x^(1)\*dz^(1)，对第二个训练样本计算dw+=x^(2)\*dz^(2)，等等。我们重复m次，接着计算dw/=m。
![vlrgoimg-5](https://user-images.githubusercontent.com/29684201/48274702-daa41a00-e47e-11e8-80fc-15913719358b.png)

对于b也类似，db被初始化为0向量，然后db+=dz^(1)， db+=dz^(2)这样重复到dz^(m)。接着计算db/=m。
![vlrgoimg-6](https://user-images.githubusercontent.com/29684201/48274704-db3cb080-e47e-11e8-8059-efc5dde9821d.png)


你可以以下两个式子来实现db和dw的计算，注意我们没有在训练集上使用for循环。
![vlrgoimg-7](https://user-images.githubusercontent.com/29684201/48274705-db3cb080-e47e-11e8-9333-b8e7aa50b142.png)

现在我们总结一下看看到底应该如何实现逻辑回归，左边是我们原来的非常低效、没有向量化的实现。右边是向量化的实现，至此你已经完成了前向传播和反向传播，完成了对所有m个训练样本的预测和求导，并且没有使用一个for循环。然后更新梯度下降参数，w的更新为w=w-alpha\*dw，b的更新为b=b-alpha\*db，其中alpha是学习率。
![vlrgoimg-8](https://user-images.githubusercontent.com/29684201/48274706-dbd54700-e47e-11e8-9070-fec6dc8cb29e.png)

有了这些，你就实现了逻辑回归梯度下降的一次迭代。虽然我之前说过我们要尽量避免使用显式的for循环，但如果要实现梯度下降的多次迭代，那么你仍然需要使用for循环去迭代指定的次数。 如果你想让梯度下降迭代1000次，你可能还是需要一个for循环 来迭代指定的次数，像这个最外面的for循环，我认为没有办法能把它也去掉。
![vlrgoimg-9](https://user-images.githubusercontent.com/29684201/48274707-dbd54700-e47e-11e8-9e7d-26fa772773bb.png)

##### Broadcasting in Python

广播不难，一张图概括。
![bipimg-1](https://user-images.githubusercontent.com/29684201/48274836-248d0000-e47f-11e8-88c2-5fd6e139e9a7.png)

##### A note on python/numpy vectors 

Python提供了广播操作的能力，更广泛地说Python和NumPy带来了极佳的灵活性，我认为这既是Python作为一门编程语言的优势也是它的劣势。其优势在于增加了语言的表达性，凭借其强大的灵活性，你只用仅仅一行代码就能完成大量的工作。但这也带来一些缺点，因为广播操作和其强大的灵活性，有时会引入十分微妙或者非常奇怪的bug。例如如果你将一个列向量与行向量相加，你可能会期望它抛出维度不匹配或者类型错误之类的报错，但实际上你会得到一个行向量和列向量求和后的矩阵，Python的这些奇怪表现有其内在的逻辑，但如果你对Python不熟悉就会写出非常奇怪且非常难以发现的bug。

令a=np.random.randn(5)会产生5个高斯随机变量并储存在数组a中，输入print(a)结果表明a的形状是这种(5,)的结构，这在Python中叫做秩为1的数组，它既不是行向量，也不是列向量 这会略微导致一些不直观的影响。比如 打印a的转置，它的结果看上去和a一样。
![noteimg-1](https://user-images.githubusercontent.com/29684201/48274837-248d0000-e47f-11e8-84f0-a77fd3e39970.png)

所以我建议你在编写神经网络时不要使用这种数据结构，即形如(5,)或者(n,)这样的秩为1的数组，它的行为并不总与行向量或者列向量相一致， 这使得它会带来一些不直观的影响。
![noteimg-2](https://user-images.githubusercontent.com/29684201/48274839-25259680-e47f-11e8-9e9a-79f8b84b0664.png)

令a的形状为(5,1)或(1,5)，这会使a成为一个5乘1的列向量或1乘5的行向量。
![noteimg-3](https://user-images.githubusercontent.com/29684201/48274830-23f46980-e47f-11e8-8158-761917214658.png)

如果出于某些原因你得到了一个秩1为数组，你可以用reshape来改变它的形状，a=a.reshape((5,1)) 比如使其成为(5,1)或者(1,5)的数组，这样它就会始终表现为列向量或者行向量。
![noteimg-4](https://user-images.githubusercontent.com/29684201/48274831-23f46980-e47f-11e8-803b-bc657e53c930.png)

我通常会将其放入断言语句中用来确保a是5乘1的列向量。执行这些断言的成本很低，并且还能充当代码的文档。
![noteimg-5](https://user-images.githubusercontent.com/29684201/48274833-248d0000-e47f-11e8-8031-4f6fb9f12e69.png)

综上，本节要点是为了简化代码不要使用秩为1的数组，始终使用n乘1的矩阵，本质上是列向量。或者使用1乘n的矩阵，本质上是行向量。自由使用断言语句来复查矩阵和数组的维度，使用reshape操作来确保矩阵和向量是你所需要的维度。

#### QUIZ

Consider the two following random arrays "a" and "b":
```
a = np.random.randn(4, 3) # a.shape = (4, 3)
b = np.random.randn(3, 2) # b.shape = (3, 2)
c = a*b
```
What will be the shape of "c"?
* c.shape = (4, 3)
* c.shape = (4, 2)
* <font color="green">The computation cannot happen because the sizes don't match. It's going to be "Error"!</font>
* c.shape = (3, 3)

第二个选项是错误的，解析如下
>No! In numpy the "\*" operator indicates element-wise multiplication. It is different from "np.dot()". If you would try "c = np.dot(a,b)" you would get c.shape = (4, 2).
Also, the broadcasting cannot happen because of the shape of b. b should have been something like (4, 1) or (1, 3) to broadcast properly. So a*b leads to an error!

Note:
1. A*B的形式是做对应点的乘积，np.dot(A,B)这个函数执行的是严格的矩阵乘法。https://blog.csdn.net/wqtltm/article/details/79882928
2. [numpy official documantation](https://docs.scipy.org/doc/numpy-1.10.1/reference/generated/numpy.exp.html) 
3. np.dot() performs a matrix-matrix or matrix-vector multiplication. This is different from np.multiply() and the \* operator (which is equivalent to .\* in Matlab/Octave), which performs an element-wise multiplication.（同第一点）
