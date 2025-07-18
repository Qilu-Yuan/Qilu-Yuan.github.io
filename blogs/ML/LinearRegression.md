---
layout: page
permalink: /blogs/ML/LinearRegression/index.html
title: 线性回归
---

## 线性回归

### 1 线性回归基本概念

<br>

线性模型在数学中“简约而不简单”，既能体现基本思想，又能构建强大的非线性模型。在机器学习中，**线性回归**是一项基本任务，应用了深远的数学工具。<br>

**线性回归**假设输出是若干输入的线性组合，目标是求解最优系数。其模型易于拟合，统计特性明确，因而广泛应用。在机器学习中，线性回归可用于对任意输入预测连续输出。<br>

1875年，英国统计学家弗朗西斯·高尔顿研究父子身高关系时，发现数据呈线性正相关，并观察到“**回归效应**”：矮个子父亲的儿子更可能比父亲高，而高个子父亲的儿子更可能比父亲矮。他提出了第一个线性回归表达式：*y*=0.516*x*+33.73，其中*y* 和 *x* 分别代表子代和父代身高。<br>

在机器学习中，如果引入常量$x_0=1$ ，线性回归通过学习一组参数 $w_i$，使预测输出 <br>

$$
f(\mathtt{x})=\mathtt{w}^T\mathtt{x}=\sum_{i=0}^n w_i\cdot x_i
$$

成为实例属性的线性组合。当实例只有一个属性时，关系为二维直线；属性较多时，关系为 *n* 维空间中的超平面。<br>
 
---

### 2 误差

<br>

在训练集上确定系数 $w_i$ 时，核心指标是预测输出*f*(*x*)与真实输出*y*之间的误差。在线性回归中，误差以**均方误差**（MSE）定义。当模型为二维直线时，均方误差即预测值与真实值之间的**欧几里得距离**，也就是向量差的 $L^2$范数。以使均方误差最小化为目标的求解方法称为**最小二乘法**，其表达式为：<br>

$$
\mathtt{w}^*=arg min_w \sum_{k=1}(\mathtt{w}^T \mathtt{x}_k - y_k)^2=arg min_w \sum_{k=1}||\mathtt{w}^T \mathtt{x}_k - y_k||^2
$$

式中每个$x_k$代表训练集中的一个样本。**在单变量线性回归任务中，最小二乘法的作用就是找到一条直线，使所有样本到直线的欧式距离之和最小**。<br>

从概率论的角度看，**最小化均方误差**的参数之所以是最优模型，是因为线性回归的结果是统计意义上的拟合。在单变量情况下，样本点可能不完全落在回归直线上。这是因为真实样本点是理想分布与噪声叠加的结果，噪声 $y_k - f(x_k)$ 导致了偏差。<br>

假设噪声服从均值为0、方差为 $\sigma^2$的正态分布，这意味着噪声为0的概率最大，噪声幅度越大出现的概率越小。基于此，参数 **w** 的推导可以通过**最大似然估计**进行，即在已知样本数据及其分布的条件下，找到使样本数据出现概率最大的假设。<br>

单个样本 x_k 出现的概率等于噪声 $y_k - f(x_k)$ 的概率，而所有独立样本同时出现的概率是每个样本概率的乘积，表达式为：<br>

$$
p(\mathtt{x}_1,\mathtt{x}_2,...\mathtt{x}_k,...|\mathtt{w})=\prod_k \frac{1}{\sqrt{2\pi}\sigma}\exp\left[ -\frac{1}{2\sigma^2}(\mathtt{w}^T \mathtt{x}_k - y_k)^2\right]
$$

**最大似然估计**的目标是最大化上述表达式。为简化计算，对表达式取对数（不改变单调性），将其转化为求和形式。经过运算，最大化问题等效于最小化：<br>

$$
\sum_{k=1}(\mathtt{w}^T \mathtt{x}_k - y_k)^2
$$

这正是**最小二乘法**的目标。因此，最小二乘法与最大似然估计在正态分布噪声假设下是一致的。因此，**对于单变量线性回归而言，在误差函数服从正态分布的情况下，从几何意义出发的最小二乘法与从概率意义出发的最大似然估计是等价的**。<br>

---

### 3 多元线性回归

<br>

在单变量线性回归中，回归方程为$y=w_1 x+w_0$。通过最小化均方误差，对 $w_1$ 和 $w_0$ 求偏导并令其为零，得到最优解的解析式：<br>

$$
w_1 = \frac{\sum_{k=1}^m y_k(x_k-\frac{1}{m}\sum_{k=1}^m x_k)}{\sum_{k=1}^m x_k^2 - \frac{1}{m}(\sum_{k=1}^m x_k)^2}
\\
w_0= \frac{1}{m}\sum_{k=1}^m (y_k -w_1 x_k)
$$

**单变量线性回归是最简单的特例**。实际问题中，输出可能由多个属性决定，例如子代身高不仅受遗传影响，还受营养、环境等因素影响。这类问题称为**多元线性回归**。<br>

多元线性回归的参数**w** 也可用最小二乘法估计，最优解同样用偏导数确定，多元线性回归的最优参数为：<br>

$$
\mathtt{w}^*=(\mathtt{X}^T \mathtt{X})^{-1}\mathtt{X}^T\mathtt{y}
$$

式中的**X**是由所有样本$x=(x_0;x_1;x_2;...;x_n)$ 的转置共同构成的矩阵,但这一表达式只在矩阵( $\mathtt{X^T X}$ )的逆矩阵存在时成立。在大量复杂的实际任务中，每个样本中属性的数目甚至会超过训练集中的样本总数，此时求出的最优解$w^*$就不是唯一的，解的选择将依赖于学习算法的归纳偏好。<br>

---

### 4.优化方法

#### 4.1最小二乘法

<br>

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


#### 4.2 梯度下降法

<br>

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
 x_1\\x_2\\.\\.\\.\\x_n
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


### 5 正则化方法

过拟合的本质源于多解性，导致模型对微小扰动极度敏感，稳定性差。正则化是解决过拟合的核心手段，常见方法为岭回归和LASSO回归：<br>

1 . **岭回归**（参数衰减）<br>

(1) 添加参数二范数惩罚项：即最小化的对象变为<br>

$$
y_k- \mathtt{w}^T \mathtt{x}_k|^2 +|\Gamma \mathtt{w}|^2 ，
$$

其中的 $\Gamma$ 被称为**季霍诺夫矩阵**，通常可以简化为一个常数<br>

(2) 约束解在高维空间球内，通过缩放削弱参数贡献，保留所有特征但降低权重。<br>

2 . **LASSO回归**  “**最小绝对缩减和选择算子**”（Least Absolute Shrinkage and Selection Operator）<br>

(1) 添加参数一范数惩罚项：<br>

(2) 即最小化的对象变为 <br>

$$
|y_k- \mathtt{w}^T \mathtt{x}_k|^2 +\lambda|\mathtt{w}|_1 ，
$$

其中的 $\lambda$ 是一个常数。<br>

(3) **引入稀疏性**，将部分参数归零，实现特征选择（奥卡姆剃刀原理），简化模型复杂度。<br>

3 . **弹性网回归**<br>

(1) 添加参数一范数和二范数惩罚项：<br>

(2) 即最小化的对象变为 <br>

$$
|y_k- \mathtt{w}^T \mathtt{x}_k|^2 +\lambda|\mathtt{w}|_1 +\lambda|\Gamma \mathtt{w}|^2 ，
$$

其中的 $\lambda$ 是一个常数。<br>

3 . **核心差异**

(1) 岭回归：正态先验，参数衰减；<br>

(2) LASSO：拉普拉斯先验，特征稀疏化。<br>

(3) 弹性网：岭回归和LASSO的混合，参数衰减和特征稀疏化。

4 . **共性**

通过惩罚项牺牲训练精度，提升模型泛化性，抑制过拟合。<br>

稀疏性思想跨领域应用广泛（如数据压缩、信号处理）。

---

### 6 代码实现

```python
import numpy as np
import matplotlib.pyplot as plt

# 生成数据
np.random.seed(0)
X = np.random.rand(100, 1)
y = 4 + 3 * X + np.random.rand(100, 1)

# 添加偏置项
X_b = np.c_[np.ones((100, 1)), X]

# 初始化参数
theta_best = np.random.rand(2, 1)

# 梯度下降
n_epochs = 1000
t0, t1 = 5, 50

def learning_schedule(t):
    return t0 / (t + t1)

for epoch in range(n_epochs):
    random_index = np.random.randint(len(X_b))
    xi = X_b[random_index:random_index + 1]
    yi = y[random_index:random_index + 1]

    gradients = 2 * xi.T.dot(xi.dot(theta_best) - yi)
    eta = learning_schedule(epoch)
    theta_best -= eta * gradients

print(theta_best)
```
