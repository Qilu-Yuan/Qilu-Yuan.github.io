---
layout: page
permalink: /blogs/ML/LogisticRegression/index.html
title: 逻辑回归
---


## 逻辑回归

### 回归与分类

<br>

1.线性回归的输出是连续的，逻辑回归的输出是离散的<br>

2.逻辑回归的输出是概率，线性回归的输出是预测值<br>

3.逻辑回归的损失函数是交叉熵损失函数，线性回归的损失函数是均方误差损失函数<br>

### 1逻辑回归

<br>

1 .目的:通过线性回归解决分类问题<br>

2 .解决方案:对线性加权和进行sigmoid函数映射，将输出映射到0-1之间<br>

3 .sigmoid函数:<br>

$$
\sigma(x) = \frac{1}{1+e^{-x}}
$$

<br>

4 .逻辑回归的一般形式:<br>

$$
p(y=1|\mathtt{x}) = \sigma(\mathtt{w}^T\mathtt{x})\\
$$

**之所以选择对数几率函数，是因为它具备良好的特性**。<br>

首先，对数几率函数能够将线性回归从负无穷到正无穷的输出范围压缩到 (0, 1) 之间，无疑更加符合对二分类任务的直观感觉。<br>

其次，当线性回归的结果$z=0$时，逻辑回归的结果$y =0.5$，这可以视为一个分界点：当$z>0$ 时，$y>0.5$ ，此时逻辑回归的结果就可以判为正例；当$z<0$时，$Y<0.5$ ,逻辑回归的结果就可以判为反例。<br>

如果将对数几率函数的结果$y$视为样本$x$作为正例的可能性，则$1-y$就是其作为反例的可能性,二者比值<br>

$$
\ln \frac{y}{1-y} = w^Tx+b
$$

因此，在逻辑回归模型中，线性回归结果以对数几率形式出现。**逻辑回归模型比较两个条件概率的大小，将实例划分到概率较大的分类中**。**在学习过程中，逻辑回归使用最大似然估计法来确定模型参数**，以最大化每个样本属于其真实标记的概率，从而找到 $w$ 的最优值。<br>

$$
L(w|x) = \Pi_{i=1}^N[p(y=1|x_i,w)]^{y_i} [1-p(y=1|x_i,w)]^{1-y_i}
$$
<br>
5 .由于输出的是概率，所以损失函数是二元交叉熵损失函数<br>

$$
\ell (y,p) = -[y\log p+(1-y)\log (1-p)]
$$

---

### 2.逻辑回归与朴素贝叶斯分类

<br>

朴素贝叶斯分类器是生成模型的代表，首先通过训练数据集估计输入和输出的联合概率分布，然后基于该分布生成符合条件的输出，以后验概率的形式呈现。<br>

逻辑回归模型则是判别模型的代表，先估计输入和输出的条件概率分布，再根据该分布判定给定输入应选择的输出，以似然概率的形式呈现。<br>

尽管原理不同，在特定条件下，逻辑回归与朴素贝叶斯分类器仍然可以等效。<br>

接下来，分析逻辑回归与朴素贝叶斯分类器的区别：<br>

1**模型假设**：当朴素贝叶斯分类的模型假设不成立时，逻辑回归和朴素贝叶斯通常会学习到不同的结果。逻辑回归在训练样本数量接近无穷大时，渐近分类准确率优于朴素贝叶斯。<br>

2**依赖性假设**：逻辑回归不完全依赖于属性之间相互独立的假设。即使数据违反这一假设，逻辑回归的条件似然最大化算法仍会调整参数以实现最佳拟合。而朴素贝叶斯则强烈依赖这一假设。<br>

3**偏差与方差**：逻辑回归的偏差较小，但方差较大。相比之下，朴素贝叶斯的偏差可能较大，但方差较小。<br>

4**收敛速度**：逻辑回归的参数估计收敛速度通常慢于朴素贝叶斯。当训练数据集容量较大时，逻辑回归的性能通常优于朴素贝叶斯；但在训练数据稀缺时，两者的表现可能会反转<br>

---

### 3.多分类

<br>

**多次二分类**<br>

**一种改进方式是通过多次二分类实现多个类别的标记**。这等效为直接将逻辑回归应用在每个类别之上，对每个类别都建立一个二分类器。如果输出的类别标记数目为$m$，就可以得到$m$个针对不同标记的二分类逻辑回归模型，而对一个实例的分类结果就是这$m$ 个分类函数中输出值最大的那个。在这种方式中，对一个实例执行分类需要多次使用逻辑回归算法，其效率显然比较低下。<br>

**Softmax回归**<br>

1.目的:通过线性回归解决多分类问题<br>

2.解决方案:对线性加权和进行softmax函数映射，将输出转换为概率值<br>

3.softmax函数:<br>

$$
softmax(y_i) = \frac{e^{y_i}}{\sum_{j=1}^n e^{y_j}}
$$

<br>

4.Softmax回归的一般形式:<br>

$$
p(y=k|\mathtt{x}) = Softmax(\mathtt{w}^T\mathtt{x})\\
$$

<br>

5.由于输出的是概率，所以损失函数是交叉熵损失函数<br>

$$
\ell (y,p) = -\sum_{i=1}^n y_i\log p_i
$$


---