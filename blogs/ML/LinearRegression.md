---
layout: page
permalink: /blogs/ML/LinearRegression/index.html
title: 线性模型
---


# 线性模型

"线性"：参数之间是线性关系，即参数之间没有乘法关系<br>

## 线性回归

### 1. 线性回归的定义

1. 定义：线性回归是一种用于描述自变量x和因变量y之间线性关系的统计模型。<br>

2. 一元线性回归，使用一个自变量x预测一个因变量y<br>

   例如 : 已知以下数据，估计一个身高182的人的体重是多少？<br>

   | 样本 | 身高（cm） | 体重（Kg） |
   | ---- | ---------- | ---------- |
   | 1    | 160        | 55         |
   | 2    | 170        | 63         |
   | 3    | 175        | 68         |
   | 4    | 180        | 72         |
   | 5    | 190        | 82         |

   回归方程：`y = ax + b`，求解出a，b，最后将182带入即可得到预测体重<br>

3. 多元线性回归，使用多个自变量(`x_i`)预测一个因变量(`y`)<br>

   | 样本 | 身高（cm） | 性别 | 年龄 | 地区 | 头发长度 | 体重 |
   | ---- | ---------- | ---- | ---- | ---- | -------- | ---- |
   | 1    | 160        | 女   | 25   | 北方 | 25       | 55   |
   | 2    | 170        | 男   | 30   | 南方 | 10       | 63   |
   | 3    | 175        | 女   | 35   | 南方 | 30       | 68   |
   | 4    | 180        | 男   | 40   | 北方 | 10       | 72   |
   | 5    | 190        | 男   | 45   | 南方 | 10       | 82   |

   回归方程：$y = w_1 x_1 + w_2 x_2+ w_3 x_3 + ...+ w_p x_p +b$ w: 权重weight，b：偏置bias<br>

#### 处理离散类型变量

one-hot编码<br>

1. one-hot编码将离散标签转化为而进制向量，使得**每个类之间的欧氏距离相等**<br>

例如：男=>（1,0） 女=>(0,1)<br>

上述特征转化为<br>

| 样本 | 身高（cm） | 男   | 女   | 年龄 | 北方 | 南方 | 头发长度 | 体重 |
| ---- | ---------- | ---- | ---- | ---- | ---- | ---- | -------- | ---- |
| 1    | 160        | 0    | 1    | 25   | 1    | 0    | 25       | 55   |
| 2    | 170        | 1    | 0    | 30   | 0    | 1    | 10       | 63   |
| 3    | 175        | 0    | 1    | 35   | 0    | 1    | 30       | 68   |
| 4    | 180        | 1    | 0    | 40   | 1    | 0    | 10       | 72   |
| 5    | 190        | 1    | 0    | 45   | 0    | 1    | 10       | 82   |

2. Multi-hot 编码可以处理样本属于多个类别的情况<br>

多选题：A=> (1,0) B=>(0,1) AB=>(1,1)<br>

#### 线性回归的一般形式

1.给定n维输入<br>

$$
\mathtt{x} = [x_1,x_2,...,x_n]^T
$$

2.线性模型有一个**n维权重**和一个**标量偏差**<br>

$$
\mathtt{w} = [w_1,w_2,...,w_n]^T , b
$$

3.输出是输入的**加权和**<br>

$$
y = w_1x_1+w_2x_2+...+w_nx_n+b
$$

4.向量形式<br>

$$
   y=<\mathtt{w,x}>+b
$$
 

### 2 损失函数 （loss function）

1.目的 衡量预测值与真实值之间的差异<br>
2.假设真实值为 $y$， 估计值为 $\hat{y}$ , 可以比较<br>

$$
e_{MAE} = |y-\hat{y}|\ 平均绝对误差 
e_{MSE} = (y-\hat{y})^2\ 均方误差
$$

3.假设有 n 个样本，损失$L = \frac{1}{n}\sum_n e_n$<br>

4.损失L是关于w和b的函数:$L(w,b)$ <br>

5.优化目标：找到使得损失函数最小的参数 $w$ 和$b$:
$$
w^*,b^*=arg\ \ce{min}_{w,b}\ L
$$

### 3最小二乘法

以**一元线性回归**为例:<br>

1.定义损失函数：$L(w,b)= \frac{1}{n} \sum_{i=1}^n (y_i - (wx_i+b))^2$<br>

2.求使得损失函数最小的 w 和 b,令偏导数=0<br>

$$
\frac{\partial L}{\partial w} = -2\cdot \frac{1}{n} \sum_{i=1}^n x_i(y_i -w x_i-b)=0\\
$$

$$ 
\frac{\partial L}{\partial b} = -2\cdot \frac{1}{n} \sum_{i=1}^n(y_i -w x_i-b)=0
$$

3.求解方程组，得到w和b的表达式为:<br>

$$
w = \frac {\sum_{i=1}^n (x_i -\bar x)(y_i -\bar y)}{\sum_{i=1}^n (x_i -\bar x)^2}\\
$$

$$
b = \bar y -w \bar x
$$

4.将数据点带入,即可得到线性回归方程 $y= wx+b$<br>

5.得到预测值<br>
  
**最小二乘法的一般解法:**<br>

<center>
<img src="https://qilu-yuan.github.io/Figure/LinearRegression/1.png" width="500" height="500" alt="AltText" />
</center>

多元线性回归的一般形式为：$y=<\mathtt{w},\mathtt{x}>+b$<br>

1.首先添加一列全为1的特征，同时给权重向量也添加一个维度值为b，即：<br>

$$
\mathtt{X} \gets [\mathtt{X},1] \ \ \mathtt{w} \gets \begin{bmatrix}
\mathtt{w}\\ b
\end{bmatrix}
$$

2.损失函数：<br>

$$
\ell (\mathtt{X,y,w}) = \frac{1}{2n} || \mathtt{y-Xw}||^2
$$

3.求解最优*** w\****

$$
\ \ \ \frac{\partial}{\partial \mathtt{w}} \ell (\mathtt{X,y,w}) = 0
\\\Leftrightarrow \frac{1}{n}(\mathtt{y-Xw})^T\mathtt{X} = 0
\\\Leftrightarrow  \mathtt{w^*} = (\mathtt{X}^T \mathtt{X})^{-1}\mathtt{X}^T \mathtt{y}
$$

 

#### 4 梯度下降法

**损失平面**：
$$
w^*,b^*=arg\ min_{w,b}\ L
$$

<center>
<img src="https://qilu-yuan.github.io/Figure/LinearRegression/2.png" width="500" height="500" alt="AltText" />
</center>

如何从Large *L*寻找到 Small *L*？

<center>
<img src="https://qilu-yuan.github.io/Figure/LinearRegression/3.png" width="500" height="500" alt="AltText" />
</center>


**梯度下降法:**<br>

1.随机选择一个初始的 $w^0$ 

<br>2.计算$w^0$处*L*的微分 
$$
\frac{\partial L}{\partial w}|_{w = w^0}
$$

<br>3.斜率为正：增加 $w^0$; 斜率为负：减小$w^0$

<br>4.更新*w*: 
$$
w^1 \Leftarrow w^0-\eta \frac{\partial L}{\partial w}|_{w = w^0}
$$ 
(超参数$\eta$:学习率)

<br>5.不断迭代更新$w$：直至收敛

##### 学习率

过小：收敛太慢，浪费计算资源，容易陷入局部最优解<br>

过大：振动幅度大，模型难以收敛<br>

##### 梯度：标量对向量的微分

$$
\mathtt{x}= \begin{bmatrix}
 x_1\\x_2
\\.\\.\\.
\\x_n
\end{bmatrix}           \bigtriangledown f_x(\mathtt{x}) = \frac{\partial y}{\partial \mathtt x} = \left[ \frac{\partial y}{\partial x_1}, \frac{\partial y}{\partial  x_2}, ..., \frac{\partial y}{\partial  x_n} \right]
$$



函数对每个变量的偏导数组成的**向量**就是梯度，梯度指向函数值**上升**最快的方向。优化时，需要计算损失函数*L*（标量）对参数（向量）的微分<br>

##### 小批量随机梯度下降法（mini-batch stochastic gradient descent）

由于在整个训练集上计算梯度的复杂度太高，所以采用小批量随机梯度下降法<br>

随机采样b个样本来近似整个训练集的梯度<br>

$$
\frac{\partial L}{\partial w}|_{w = w^0} \approx \frac{1}{b} \sum_{i=1}^b \frac{\partial L_i}{\partial w}|_{w = w^0}
$$

批量大小b是另一个超参数，b的选择：b越大，梯度的估计越准确，但计算复杂度也越高；b越小，梯度的估计越不准确，但计算复杂度越低<br>


## 逻辑回归:使用线性回归解决二分类问题

**回归与分类**
1.线性回归的输出是连续的，逻辑回归的输出是离散的<br>

2.逻辑回归的输出是概率，线性回归的输出是预测值<br>

3.逻辑回归的损失函数是交叉熵损失函数，线性回归的损失函数是均方误差损失函数<br>

**逻辑回归:**<br>
1.目的:通过线性回归解决分类问题<br>
2.解决方案:对线性加权和进行sigmoid函数映射，将输出映射到0-1之间<br>
3.sigmoid函数:<br>

$$
\sigma(x) = \frac{1}{1+e^{-x}}
$$

4.逻辑回归的一般形式:<br>

$$
p(y=1|\mathtt{x}) = \sigma(\mathtt{w}^T\mathtt{x})\\
$$

5.由于输出的是概率，所以损失函数是二元交叉熵损失函数<br>

$$
\ell (y,p) = -[y\log p+(1-y)\log (1-p)]
$$

## Softmax回归:使用线性回归解决多分类问题

**Softmax回归:**<br>

1.目的:通过线性回归解决多分类问题<br>

2.解决方案:对线性加权和进行softmax函数映射，将输出转换为概率值<br>

3.softmax函数:<br>

$$
softmax(y_i) = \frac{e^{y_i}}{\sum_{j=1}^n e^{y_j}}
$$

4.逻辑回归的一般形式:<br>

$$
p(y=k|\mathtt{x}) = Softmax(\mathtt{w}^T\mathtt{x})\\
$$

5.由于输出的是概率，所以损失函数是交叉熵损失函数<br>

$$
\ell (y,p) = -\sum_{i=1}^n y_i\log p_i = 
$$

## 均方误差与交叉熵

从损失的角度来看:交叉熵只关注预测正确的损失，而均方误差关注所有预测的损失<br>

从梯度的角度来看:交叉熵的梯度在概率为0是梯度较大，在概率为1时梯度较小,更符合我们需要的结果; 而均方误差在概率为0是梯度较小，在概率为1时梯度较大<br>

## 多项式回归

一元多项式回归的一般形式：$y= w_0 + w_1x + w_2x^2 + ... + w_mx^m$<br>

优化方法可以是梯度下降法，也可以是最小二乘法<br>

模型复杂度：$m$越大，模型越复杂，越容易过拟合<br>

## 模型选择

1.模型复杂度：模型拟合各种数据的能力<br>

2.对于给定的模型种类，模型复杂度主要与**模型参数量**和**参数选择范围**有关

3.误差：训练误差和泛化误差<br>

## 正则化

正则化：在损失函数中添加一个正则化项，用于限制模型复杂度，从而防止过拟合<br>

Lasso回归：正则化项为参数的绝对值之和<br>

$$
\ell (y,\hat{y}) + \lambda ||\mathtt{w}||_1
$$

Ridge回归：正则化项为参数的平方和<br>

$$
\ell (y,\hat{y}) + \lambda ||\mathtt{w}||_2^2
$$

Elastic Net回归：正则化项为参数的L1范数和L2范数的加权和<br>

$$
\ell (y,\hat{y}) + \lambda_1 ||\mathtt{w}||_1 + \lambda_2 ||\mathtt{w}||_2^2
$$

超参数$\lambda$：控制正则化项的权重，$\lambda$越大，正则化项的权重越大，模型复杂度越小，越容易欠拟合<br>

Lasso回归和Ridge回归的区别在于正则化项的不同，Lasso回归的正则化项是参数的绝对值之和，Ridge回归的正则化项是参数的平方和。**Lasso回归的正则化项可以使得一些参数变为0，从而实现特征选择**，而Ridge回归的正则化项可以使得参数的值变小，从而防止过拟合。
