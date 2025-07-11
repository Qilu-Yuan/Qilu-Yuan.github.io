---
layout: page
permalink: /blogs/ML/Clustering/index.html
title: 聚类分析
---

## 聚类分析

### **1. 基本概念与核心问题**

- **定义**：聚类分析是一种无监督学习方法，旨在将未标记的数据划分为内在的类别（聚类/簇），揭示数据分布规律。<br>

- **核心任务**：

**判定同类样本**：基于相似性度量（如距离），确保类内差异小、类间差异大。

<br>**聚类形成机制**：通过算法设计将相似样本聚集。

- **与分类的区别**：<br>

**分类**：已知类别标签，按标签划分数据。<br>  

<br>**聚类**：数据划分后定义类别，无需先验标签。<br>  

---

### **2. 相似性度量：距离测度**

- **闵可夫斯基距离**：<br>

$$
\mathtt{dist_{mk}}(\mathtt{x}_i,\mathtt{x}_j) = \left(\sum_{n=1}^N|x_{in}-x_{jn}|^p\right)^{1/p}
$$

<br>

- **欧式距离**（$p=2$）：几何空间中的直线距离。  <br>

- **曼哈顿距离**（$p=1$）：沿坐标轴的距离总和。  <br>

- **切比雪夫距离**（$p\to ∞$）：各维度最大差值。  <br>

---

### **3. 主要聚类方法**

#### **3.1 层次聚类（基于连接）**

<br>(1)**核心思想**：样本与邻近样本更相关，通过树状图（层次结构）划分聚类。

<br>(2)**策略**：

- **自底向上（会聚）**：初始每个样本为一类，逐步合并最近类，直至预设聚类数。<br>

- **距离计算方式**：<br>

**单链接**：类间最小样本距离（易形成长链状聚类）。

<br>**全链接**：类间最大样本距离（偏好紧凑聚类）。

<br>**均链接**：类间平均样本距离（平衡单/全链接）。

<br>

(3)**特点**：计算复杂度高，适合小数据集

#### **3.2 原型聚类（基于质心）**

(1)**核心思想**：每个聚类由质心（中心向量）表示，通过迭代优化质心位置。

<br>(2)**典型算法**：**k均值算法** 

- **步骤**：  <br>

<br>

a .随机选k个初始质心。<br>

b .分配样本到最近质心，形成聚类。<br>

c .重新计算聚类质心（均值）。<br>  

d .重复直至质心稳定。<br>

- **优化目标**：最小化类内样本到质心的距离平方和。<br>

- **局限性**：需预设k值；对噪声敏感；偏好球形聚类。<br>  

#### **3.3 分布聚类（基于概率模型）**

<br>(1)**核心思想**：假设数据由隐藏的概率分布生成（如高斯分布），通过参数估计确定聚类。

<br>(2)**典型算法**：**期望最大化（EM）算法**

- **步骤**：<br>  

<br>

a .**期望步（E-step）**：估计样本所属类的概率。<br>

b .**最大化步（M-step）**：更新模型参数以最大化似然函数。<br>

- **应用场景**：适合假设数据符合特定分布的情况（如混合高斯模型）。<br>

- **风险**：模型假设不成立时可能导致过拟合。<br>

#### **3.4密度聚类（基于密度）**

<br>  (1) **核心思想**：聚类由高密度区域构成，低密度区为噪声。

<br>  (2)**典型算法**：**DBSCAN**

- **核心概念**:

<br>a.**ε-邻域**：样本周围ε半径内的区域。

<br>b.**核心点**：ε邻域内样本数≥阈值MinPts。

<br>c.**密度可达**：通过核心点连接的样本链。

- **步骤**：

<br>a.标记核心点、边界点、噪声点。

<br>b.合并密度可达的核心点形成聚类。

- **优势**：无需预设聚类数；可识别任意形状聚类；抗噪声。<br>  

---

### **4. 应用场景**


- **用户画像**：通过行为数据、人口学特征等划分用户群体，为后续分类模型（如推荐系统）提供基础。<br>

- **其他场景**：图像分割、异常检测、社交网络分析等。<br>

---

### **5. 扩展方法**

- **谱聚类**：基于图论，利用数据相似性矩阵的特征向量划分聚类，适合非凸结构。<br>

- **模糊聚类**：允许样本以概率隶属多个类（如模糊C均值算法）。<br>

---

### **6. 关键挑战**

- **算法选择**：数据特性（分布、噪声、形状）决定适用方法（如DBSCAN处理噪声，k均值处理球形聚类）。<br>

- **参数调整**：k值（k均值）、ε和 MinPts（DBSCAN）等需结合领域知识或评估指标（如轮廓系数）。<br>

通过聚类分析，数据的内在模式得以揭示，为后续有监督学习或业务决策提供基础支持。<br>

### 7 总结

- 聚类分析是一种无监督学习方法，通过学习没有分类标记的训练样本发现数据的内在性质和规律；<br>

- 数据之间的相似性通常用距离度量，类内差异应尽可能小，类间差异应尽可能大；根据形成聚类方式的不同，聚类算法可以分为层次聚类、原型聚类、分布聚类、密度聚类等几类；<br>

- 聚类分析的一个重要应用是对用户进行分组与归类。<br>