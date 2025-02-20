---
layout: page
permalink: /blogs/ML/LinearRegression/index.html
title: 线性回归
---


## 线性回归

### 1. 线性回归的数学模型

线性回归试图学习一个线性模型来拟合输入特征和输出标签之间的关系，其数学模型可以表示为：<br>

$$
y = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + ... + \theta_n x_n + \epsilon
$$

<br>其中，$y$ 是输出标签，$x_1, x_2, ..., x_n$ 是输入特征，$\theta_0, \theta_1, ..., \theta_n$ 是模型的参数，$\epsilon$ 是误差项。

### 2. 线性回归的损失函数

线性回归的损失函数通常使用均方误差（Mean Squared Error, MSE）来衡量模型预测值和真实值之间的差异，其数学表达式为：<br>

$$
J(\theta) = \frac{1}{2m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})^2
$$

<br>其中，$m$ 是样本数量，$h_\theta(x^{(i)})$ 是模型对第 $i$ 个样本的预测值，$y^{(i)}$ 是第 $i$ 个样本的真实值。

### 3. 线性回归的优化方法

线性回归的优化方法通常使用梯度下降（Gradient Descent）来最小化损失函数。梯度下降的迭代公式为：<br>

$$
\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta)
$$

<br>其中，$\alpha$ 是学习率，$\theta_j$ 是模型的参数，$\frac{\partial}{\partial \theta_j} J(\theta)$ 是损失函数 $J(\theta)$ 对 $\theta_j$ 的偏导数。

### 4. 线性回归的评估指标

线性回归的评估指标通常使用均方根误差（Root Mean Squared Error, RMSE）来衡量模型预测值和真实值之间的差异，其数学表达式为：<br>

$$
RMSE = \sqrt{\frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})^2}
$$

### 5. 线性回归的应用场景

线性回归是一种简单而有效的回归算法，可以用于各种应用场景，包括但不限于：<br>

- 房价预测：根据房屋面积、房间数量、楼层等信息预测房价。<br>
- 股票价格预测：根据历史股票价格、成交量等信息预测未来股票价格。<br>

