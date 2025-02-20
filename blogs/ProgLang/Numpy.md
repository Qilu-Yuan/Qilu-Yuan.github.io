---
layout: page
permalink: /blogs/ProgLang/Numpy/index.html
title: Numpy常用命令
---


## Numpy简介
Numpy是Python中用于科学计算的库，提供了高性能的多维数组对象和用于处理这些数组的工具。Numpy是Python数据科学的基础库之一，广泛应用于数据分析、机器学习等领域。

## Numpy常用命令

### 1.创建数组

```python
import numpy as np

# 创建一维数组
a = np.array([1, 2, 3, 4, 5])
print(a)
#创建二维数组
b = np.array([[1, 2, 3], [4, 5, 6]])
print(b)

# 创建三维数组
c = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(c)

# 创建全0数组
d = np.zeros((3, 4))
print(d)

# 创建全1数组
e = np.ones((3, 4))
print(e)

# 创建全5数组
f = np.full((3, 4), 5)
print(f)

# 创建对角线为1的数组
g = np.eye(3)
print(g)


# 创建随机数组
h = np.random.rand(3, 4)
print(h)

# 创建随机整数数组
i = np.random.randint(0, 10, size=(3, 4))
print(i)
```

### 2.数组操作

```python
import numpy as np

# 创建数组
a = np.array([1, 2, 3, 4, 5])
b = np.array([[1, 2, 3], [4, 5, 6]])

# 数组形状
print(a.shape)  # (5,)
print(b.shape)  # (2, 3)

# 数组维度
print(a.ndim)  # 1
print(b.ndim)   # 2

# 数组大小
print(a.size)   # 5
print(b.size)   # 6

# 数组元素类型
print(a.dtype)  # int64
print(b.dtype)  # int64

# 数组转置
print(a.T)      # (5,)
print(b.T)      # (3, 2)

# 数组重塑
c = a.reshape((1, 5))
print(c.shape)  # (1, 5)

# 数组切片
print(a[1:4])   # [2 3 4]
print(b[:, 1])  # [2 5]

# 数组拼接
c = np.concatenate((a, b), axis=0)
print(c)        # [1 2 3 4 5 1 2 3 4 5 6]

# 数组分割
d = np.split(c, 2, axis=0)

# 数组复制
e = a.copy()

# 2个一维数组合并为2维
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
c = np.vstack((a, b))
```

### 3.数组运算

```python
import numpy as np

# 创建数组
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# 数组加法
c = a + b
print(c)  # [5 7 9]

# 数组减法
c = a - b
print(c)  # [-3 -3 -3]

# 数组乘法
c = a * b
print(c)  # [ 4 10 18]

# 数组除法

c = a / b
print(c)  # [0.25 0.4  0.5 ]

# 数组乘方
c = a ** 2
print(c)  # [1 4 9]
```

### 4.数组统计

```python
import numpy as np

# 创建数组
a = np.array([1, 2, 3])
b = np.array([[1, 2, 3], [4, 5, 6]])

# 数组求和
c = np.sum(a)
print(c)  # 6

# 数组求和
c = np.sum(b)
print(c)  # 21

# 数组累乘
c = np.prod(a)
print(c)  # 6

# 数组平均值
c = np.mean(a)
print(c)  # 2.0

# 数组最大值
c = np.max(a)
print(c)  # 3

# 数组最小值
c = np.min(a)
print(c)  # 1


```

### 5. IO操作

```python
import numpy as np

# 保存数组
np.save('array.npy', a)

# 加载数组
b = np.load('array.npy')
print(b)  # [1 2 3]

# 保存数组为文本文件
np.savetxt('array.txt', a)

# 加载数组
b = np.loadtxt('array.txt')
print(b)  # [1. 2. 3.]

# 保存数组为二进制文件
np.savez('array.npz', a=a, b=b)

# 加载数组
with np.load('array.npz') as data:
    a = data['a']
    b = data['b']
```

### 6. 线性代数

```python
import numpy as np

# 创建数组
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

# 数组乘法
c = np.dot(a, b)
print(c)  # [[19 22] [43 50]]

# 数组转置
c = np.transpose(a)
print(c)  # [[1 3] [2 4]]

# 数组逆矩阵
c = np.linalg.inv(a)
print(c)  # [[-2.  1.] [ 1. -0.5]]

# 数组特征值
c = np.linalg.eigvals(a)
print(c)  # [5. 1.]

# 数组特征向量
c, d = np.linalg.eig(a)
print(c)  # 特征值 [5. 1.] 
print(d)  # 特征向量 [[-0.89442719  0.70710678] [ 0.4472136  -0.70710678]]
```