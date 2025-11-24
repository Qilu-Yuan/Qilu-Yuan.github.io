---
layout: page
permalink: /blogs/SubMD/HarmonicSphere/index.html
title: 球谐函数的代码实现
---

## 球谐函数的代码实现

### 球谐函数基本介绍
<br>
球谐函数（Spherical Harmonics）是一类定义在球面上的特殊函数，广泛应用于物理学、工程学和计算机科学等领域。它们在量子力学、地球物理学、计算机图形学等方面有重要应用。 简单来说，球谐函数是球面上角度变量的正交函数集，可以用来表示和分析球面上的各种现象和数据。<br>

球谐函数通常表示为Y_l^m(θ, φ)，其中l是非负整数，m是整数，满足-l ≤ m ≤ l。θ和φ分别是球坐标系中的极角和方位角。 球谐函数的数学表达式为：
$$
Y_{lm}（\theta,\phi） = \sqrt{2} K_l^m \cos(m\phi) P_l^m(\cos\theta) \quad \text{for } m > 0\\
Y_{lm}（\theta,\phi） = K_l^0 P_l^0(\cos\theta) \quad \text{for } m = 0\\
Y_{lm}（\theta,\phi） = \sqrt{2} K_l^{|m|} \sin(|m|\phi) P_l^{|m|}(\cos\theta) \quad \text{for } m < 0
$$
<br>其中，$K_l^m$是归一化常数，定义为：
$$
K_l^m = \sqrt{\frac{(2l + 1)}{4\pi} \frac{(l - m)!}{(l + m)!}}
$$
<br>关联勒让德多项式$P_l^m(x)$定义为：
$$
$P_l^m(x) = (-1)^m (1-x^2)^{m/2} \frac{d^m}{dx^m}(P_l(x))$
$$
<br>其中，$P_l(x)$是勒让德多项式，定义为：
$$
P_l(x) = \frac{1}{2^l l!} \frac{d^l}{dx^l} (x^2 - 1)^l
$$
​<br>


### 球谐函数的性质
<br>球谐函数具有以下重要性质：
- 正交性：不同阶数和次数的球谐函数在球面上是正交的，即：
$$
\int_0^{2\pi} \int_0^{\pi} Y_{l_1}^{m_1}(\theta, \phi) Y_{l_2}^{m_2}(\theta, \phi)^* \sin\theta d\theta d\phi = \delta_{l_1 l_2} \delta_{m_1 m_2}
$$
- 完备性：任意平方可积的函数都可以表示为球谐函数的线性组合。
- 旋转变换：球谐函数在旋转下具有良好的变换性质，适用于描述旋转对称系统。    
<br>

在程序里我们可以通过关联勒让德多项式的特殊值与递归关系来计算球谐函数的值。

- 特殊值
$$
P_m^m(x) = (-1)^m (2m - 1)!! (1 - x^2)^{m/2}
$$
其中，(2m - 1)!!表示双阶乘，定义为：
$$
n!! = n \cdot (n - 2) \cdot (n - 4) \cdots
$$
- 递归关系
$$
P_{l}^{m}(x) = \frac{(2l - 1)x P_{l - 1}^{m}(x) - (l + m - 1) P_{l - 2}^{m}(x)}{l - m}
$$
<br>

### Python代码实现球谐函数

```python
import numpy as npimport numpy as np
import scipy.special as sp

#factorial
def factorial(n):
    if n == 0:
        return 1
    else:
        return n*factorial(n-1)

#doublefactorial
def doublefactorial(n):
    if n == 0 or n == 1 or n == -1:
        return 1
    else:
        return (n)*doublefactorial(n-2)


def K(l,m):
    x1 = (2*l+1)/(4*np.pi)
    m_abs = abs(m)
    x2 = factorial(l-m_abs)/factorial(l+m_abs)
    return np.sqrt(x1*x2)

def Plm(l,m,x):
    pmm =  (-1)**m * doublefactorial(2*m-1) *(1-x**2)**(m/2)
    if l==m:
        return pmm
    elif l==m+1:
        return x*(2*m+1)*Plm(l-1,m,x)
    else:
        return ((2*l-1)*x*Plm(l-1,m,x)-(l+m-1)*Plm(l-2,m,x))/(l-m)


# spherical harmonics x and y are polar and azimuthal angles (theta, phi)
def SH(l,m,x,y):
    if m < 0:
        Y = np.sqrt(2)*K(l,m)*np.sin(-m*y)*Plm(l,-m,np.cos(x))
    elif m == 0:
        Y = K(l,m)*Plm(l,m,np.cos(x))
    else:
        Y = np.sqrt(2)*K(l,m)*np.cos(m*y)*Plm(l,m,np.cos(x))
    return Y
```

此外，SciPy库中也提供了计算球谐函数的函数`scipy.special.sph_harm`，可以直接使用：

```python
from scipy.special import sph_harm
def SH_scipy(l, m, theta, phi):
    return sph_harm(m, l, phi, theta)
```
对比一下二者绘制出的图像
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import special
import mpl_toolkits.mplot3d.axes3d as axes3d

# Using our SH function
theta, phi = np.linspace(0, np.pi, 100), np.linspace(0, 2*np.pi, 100)
THETA, PHI = np.meshgrid(theta, phi)
#help(special.sph_harm)
R = (SH(3,1,THETA,PHI))**2
X = R * np.sin(THETA) * np.cos(PHI)
Y = R * np.sin(THETA) * np.sin(PHI)
Z = R * np.cos(THETA)
fig = plt.figure()
ax = fig.add_subplot(1,1,1, projection='3d')
plot = ax.plot_surface(
    X, Y, Z, rstride=1, cstride=1, cmap=plt.get_cmap('jet'),
    linewidth=0, antialiased=False, alpha=0.5)

# below are codes copied from stackoverflow, to make the scaling correct
max_range = np.array([X.max()-X.min(), Y.max()-Y.min(), Z.max()-Z.min()]).max() / 2.0
mid_x = (X.max()+X.min()) * 0.5
mid_y = (Y.max()+Y.min()) * 0.5
mid_z = (Z.max()+Z.min()) * 0.5
ax.set_xlim(mid_x - max_range, mid_x + max_range)
ax.set_ylim(mid_y - max_range, mid_y + max_range)
ax.set_zlim(mid_z - max_range, mid_z + max_range)
plt.show()
```

<center>
<img src="https://qilu-yuan.github.io/Figure/HarmonicSphere/1.png" width="500" height="500" alt="AltText" />
</center>

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import special
import mpl_toolkits.mplot3d.axes3d as axes3d

# Using scipy special.sph_harm
theta, phi = np.linspace(0, np.pi, 100), np.linspace(0, 2*np.pi, 100)
THETA, PHI = np.meshgrid(theta, phi)
#help(special.sph_harm)
R = (special.sph_harm(1,3,PHI,THETA).real)**2
X = R * np.sin(THETA) * np.cos(PHI)
Y = R * np.sin(THETA) * np.sin(PHI)
Z = R * np.cos(THETA)
fig = plt.figure()
ax = fig.add_subplot(1,1,1, projection='3d')
plot = ax.plot_surface(
    X, Y, Z, rstride=1, cstride=1, cmap=plt.get_cmap('jet'),
    linewidth=0, antialiased=False, alpha=0.5)

# below are codes copied from stackoverflow, to make the scaling correct
max_range = np.array([X.max()-X.min(), Y.max()-Y.min(), Z.max()-Z.min()]).max() / 2.0
mid_x = (X.max()+X.min()) * 0.5
mid_y = (Y.max()+Y.min()) * 0.5
mid_z = (Z.max()+Z.min()) * 0.5
ax.set_xlim(mid_x - max_range, mid_x + max_range)
ax.set_ylim(mid_y - max_range, mid_y + max_range)
ax.set_zlim(mid_z - max_range, mid_z + max_range)
plt.show()
```

<center>
<img src="https://qilu-yuan.github.io/Figure/HarmonicSphere/1.png" width="500" height="500" alt="AltText" />
</center>

可以看出二者绘制的图像是一致的。

​### Fortran和c++代码实现球谐函数


下面是C++代码实现球谐函数的示例：
```c++
#include <cmath>
#include <iostream>
double factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
double doubleFactorial(int n) {
    if (n == 0 || n == 1 || n == -1) return 1;
    return n * doubleFactorial(n - 2);
}
double K(int l, int m) {
    double x1 = (2.0 * l + 1.0) / (4.0 * M_PI);
    int m_abs = std::abs(m);
    double x2 = static_cast<double>(factorial(l - m_abs)) / static_cast<double>(factorial(l + m_abs));
    return std::sqrt(x1 * x2);
}
double Plm(int l, int m, double x) {
    double pmm = std::pow(-1.0, m) * doubleFactorial(2 * m - 1) * std::pow(1 - x * x, m / 2.0);
    if (l == m) {
        return pmm;
    } else if (l == m + 1) {
        return x * (2 * m + 1) * Plm(l - 1, m, x);
    } else {
        return ((2.0 * l - 1.0) * x * Plm(l - 1, m, x) - (l + m - 1) * Plm(l - 2, m, x)) / (l - m);
    }
}
double SH(int l, int m, double x, double y) {
    if (m < 0) {
        return std::sqrt(2.0) * K(l, m) * std::sin(-m * y) * Plm(l, -m, std::cos(x));
    } else if (m == 0) {
        return K(l, m) * Plm(l, m, std::cos(x));
    } else {
        return std::sqrt(2.0) * K(l, m) * std::cos(m * y) * Plm(l, m, std::cos(x));
    }
}
```


最后，下面是Fortran代码实现球谐函数的示例：

```fortran
FUNCTION SH(l,m,x,y) RESULT(res)
	IMPLICIT NONE
	INTEGER, INTENT(IN) :: l, m
	DOUBLE PRECISION, INTENT(IN) :: x, y
	DOUBLE PRECISION :: res
	DOUBLE PRECISION :: Klm, Plm !function
!===========================================
	! function to compute spherical harmonics Y_lm
	! l: degree, m: order, x: polar angle (theta), y: azimuthal angle (phi)
	! res: value of Y_lm at (x,y)
	
	IF (m < 0) THEN
		res = SQRT(2.0)*Klm(l,m)*SIN(-m*y)*Plm(l,-m,COS(x))
	ELSE IF (m == 0) THEN
		res = Klm(l,m)*Plm(l,m,COS(x))
	ELSE
		res = SQRT(2.0)*Klm(l,m)*COS(m*y)*Plm(l,m,COS(x))
	END IF
END FUNCTION SH

FUNCTION Klm(l,m) RESULT(res)
	IMPLICIT NONE
	INTEGER, INTENT(IN) :: l, m
	DOUBLE PRECISION :: res
	DOUBLE PRECISION :: x1, x2 
	INTEGER :: Factorial !function
!===========================================
	x1 = (2*l+1)/(4*3.141592653589793d0)
	x2 = Factorial(l-ABS(m))/Factorial(l+ABS(m))
	res = SQRT(x1*x2)
END FUNCTION Klm

RECURSIVE FUNCTION Plm(l,m,x) RESULT(res)
	IMPLICIT NONE
	INTEGER, INTENT(IN) :: l, m
	DOUBLE PRECISION, INTENT(IN) :: x
	DOUBLE PRECISION :: res
	DOUBLE PRECISION :: pmm
	INTEGER :: DoubleFactorial !function
!===========================================
	pmm =  (-1)**m * DoubleFactorial(2*m-1) *(1-x**2)**(m/2)
	IF (l==m) THEN
		res = pmm
	ELSE IF (l==m+1) THEN
		res = x*(2*m+1)*Plm(l-1,m,x)
	ELSE
		res = ((2*l-1)*x*Plm(l-1,m,x)-(l+m-1)*Plm(l-2,m,x))/(l-m)
	END IF
END FUNCTION Plm

RECURSIVE FUNCTION Factorial(n) RESULT(fact)
	IMPLICIT NONE
	INTEGER, INTENT(IN) :: n
	INTEGER :: fact
	IF (n == 0) THEN
		fact = 1
	ELSE
		fact = n * Factorial(n - 1)
	END IF
END FUNCTION Factorial

RECURSIVE FUNCTION DoubleFactorial(n) RESULT(dfact)
	IMPLICIT NONE
	INTEGER, INTENT(IN) :: n
	INTEGER :: dfact
	IF (n == 0 .OR. n == 1 .OR. n == -1) THEN
		dfact = 1
	ELSE
		dfact = n * DoubleFactorial(n - 2)
	END IF
END FUNCTION DoubleFactorial
```
