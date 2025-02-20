---
layout: page
permalink: /blogs/ML/LinearRegression/index.html
title: 线性回归
---


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
 

### 8.2 损失函数 （loss function）

1.目的 衡量预测值与真实值之间的差异<br>
2.假设真实值为 $y$， 估计值为 $\hat{y}$ , 可以比较<br>

$$
e_{MAE} = |y-\hat{y}|\ 平均绝对误差 
e_{MSE} = (y-\hat{y})^2\ 均方误差
$$

3.假设有 n 个样本，损失$L = \frac{1}{n}\sum_n e_n$<br>

4.损失L是关于w和b的函数：$L(w,b)$ <br>

5.优化目标：找到使得损失函数最小的参数 $w$ 和$b$：$w^*,b^*=arg\ \ce{min}_{w,b}\ L$ <br>



### 8.3最小二乘法

以**一元线性回归**为例：<br>

1.定义损失函数：$L(w,b)= \frac{1}{n} \sum_{i=1}^n (y_i - (wx_i+b))^2$<br>

2.求使得损失函数最小的 w 和 b，令偏导数=0<br>

$$
\frac{\partial L}{\partial w} = -2\cdot \frac{1}{n} \sum_{i=1}^n x_i(y_i -w x_i-b)=0\\ 
\frac{\partial L}{\partial b} = -2\cdot \frac{1}{n} \sum_{i=1}^n(y_i -w x_i-b)=0
$$

3.求解方程组，得到w和b的表达式为：<br>

$$
w = \frac {\sum_{i=1}^n (x_i -\bar x)(y_i -\bar y)}{\sum_{i=1}^n (x_i -\bar x)^2}\\
b = \bar y -w \bar x
$$

4.将数据点带入，即可得到线性回归方程 $y= wx+b$<br>

5.得到预测值<br>
  

最小二乘法的一般解法：<br>

<img src="https://qilu-yuan.github.io/Figure/LinearRegression/1.png" class="floatpic"><br>

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

 

#### 8.4 梯度下降法

**损失平面**：$w^*,b^*=arg\ \ce{min}_{w,b}\ L$

<br><img src="https://qilu-yuan.github.io/Figure/LinearRegression/2.png" class="floatpic"> <br>

如何从Large *L*寻找到 Small *L*？

<img src="https://qilu-yuan.github.io/Figure/LinearRegression/3.png" class="floatpic"> <br>

梯度下降法：<br>

随机选择一个初始的 $w^0$ 

<br>计算$w^0$处*L*的微分 

$$
\frac{\partial L}{\partial w}|_{w = w^0}
$$

<br>斜率为正：增加 $w^0$

<br>斜率为负：减小$w^0$

<br>更新*w*: 
$$
w^1 \Leftarrow w^0-\eta \frac{\partial L}{\partial w}|_{w = w^0}
$$ 
($\eta$:学习率)

<br>不断迭代更新$w$：直至收敛

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



