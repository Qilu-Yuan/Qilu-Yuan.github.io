---
layout: page
permalink: /blogs/ProgLang/Fortran/index.html
title: Fortran基本语法暨学习笔记
---

## **Fortran基本语法暨学习笔记**

## 1. Fortran简介

Fortran是一种高级编程语言，由IBM公司在1957年推出，主要用于科学计算和工程应用。Fortran语言的设计初衷是为了提高数值计算的效率，因此它具有很高的执行效率和良好的数值计算性能。Fortran语言在科学计算领域有着广泛的应用，特别是在数值模拟、天气预报、流体力学、量子力学等领域。

## 2. Fortran基本语法

Fortran是一种面向过程的编程语言，它以过程（子程序）为单位进行程序设计。下面是一些Fortran的基本语法：

```fortran
program main
    ! 程序开始
    ! 变量声明
    ! 程序逻辑
    ! 程序结束
end program main
```


### 2.1 变量声明

在Fortran中，变量必须先声明后使用。变量声明通常放在程序的开头部分，使用`INTEGER`、`REAL`、`CHARACTER`等关键字来声明变量的类型和名称。例如：

```fortran
INTEGER :: i, j
REAL :: x, y
CHARACTER(LEN=10) :: name
```

### 2.2 数据类型


Fortran支持多种数据类型，包括整数类型、浮点数类型和字符类型。整数类型包括`INTEGER`、`LOGICAL`等，浮点数类型包括`REAL`、`DOUBLE PRECISION`等，字符类型包括`CHARACTER`等。例如：

```fortran
INTEGER :: i = 10
REAL :: x = 3.14
CHARACTER(LEN=10) :: name = "Hello"
LOGICAL :: a = .TRUE.
```


### 2.3 运算符
Fortran支持多种运算符，包括算术运算符、关系运算符和逻辑运算符。算术运算符包括`+`、`-`、`*`、`/`等，关系运算符包括`==`、`/=`、`<`、`>`、`<=`、`>=`等，逻辑运算符包括`AND`、`OR`、`NOT`等。例如：

```fortran
INTEGER :: i = 10, j = 20
REAL :: x = 3.14, y = 2.71
LOGICAL :: a = .TRUE., b = .FALSE.

i = i + j
x = x - y
a = a .AND. b
```

### 2.4 控制结构
#### 2.4.1 条件语句

Fortran支持条件语句，包括`IF`语句和`SELECT CASE`语句。`IF`语句用于根据条件执行不同的代码块，`SELECT CASE`语句用于根据表达式的值选择不同的代码块。例如：

```fortran
INTEGER :: i = 10

IF (i > 0) THEN
    PRINT *, "i is positive"
ELSE
    PRINT *, "i is non-positive"
END IF

SELECT CASE (i)
    CASE (1)
        PRINT *, "i is 1"
    CASE (2)
        PRINT *, "i is 2"
    CASE DEFAULT
        PRINT *, "i is neither 1 nor 2"
END SELECT
```

#### 2.4.2 循环语句

Fortran支持循环语句，包括`DO`循环和`WHILE`循环。`DO`循环用于重复执行一段代码，`WHILE`循环用于在条件为真时重复执行一段代码。例如：

```fortran
INTEGER :: i

DO i = 1, 10
    PRINT *, i
END DO

i = 1
DO WHILE (i <= 10)
    PRINT *, i
    i = i + 1
END DO
```


### 2.5 函数和子程序

Fortran支持函数和子程序，用于封装和复用代码。函数和子程序可以接受参数并返回结果。例如：

```fortran
FUNCTION add(a, b)
    INTEGER :: a, b
    INTEGER :: add
    add = a + b
END FUNCTION

SUBROUTINE print_message(message)
    CHARACTER(*) :: message
    PRINT *, message
END SUBROUTINE

INTEGER :: result = add(3, 4)
CALL print_message("Hello, world!")
```

### 2.6 数组

Fortran支持一维和多维数组。数组可以用于存储和操作一组数据。例如：

```fortran
INTEGER, DIMENSION(5) :: arr = [1, 2, 3, 4, 5]
INTEGER :: i
DO i = 1, 5
    PRINT *, arr(i)
END DO
```

二维数组<br>
```fortran
INTEGER, DIMENSION(3, 3) :: arr = RESHAPE([1, 2, 3, 4, 5, 6, 7, 8, 9], [3, 3])
INTEGER :: i, j
DO i = 1, 3
    DO j = 1, 3
        PRINT *, arr(i, j)
    END DO
END DO
```

动态数组<br>

```fortran
INTEGER, DIMENSION(:), ALLOCATABLE :: arr
INTEGER :: i
ALLOCATE(arr(5)) ! 分配内存
arr = [1, 2, 3, 4, 5]
DO i = 1, 5
    PRINT *, arr(i)
END DO
DEALLOCATE(arr) !释放内存
```

### 2.7 模块

Fortran支持模块，用于封装和复用代码。模块可以包含变量、函数和子程序。例如：

```fortran
MODULE my_module
    INTEGER :: my_variable = 10
    FUNCTION add(a, b)
        INTEGER :: a, b
        INTEGER :: add
        add = a + b
    END FUNCTION
END MODULE

USE my_module
INTEGER :: result = add(3, 4)
PRINT *, my_variable
```

### 2.8 文件操作

Fortran支持文件操作，可以用于读写文件。例如：

```fortran
OPEN(UNIT=1, FILE='data.txt', STATUS='OLD', ACTION='READ')
INTEGER :: i
READ(1, *) i
CLOSE(1)

OPEN(UNIT=2, FILE='output.txt', STATUS='NEW', ACTION='WRITE')
WRITE(2, *) i
CLOSE(2)

```

new和old分别表示创建新文件和打开现有文件。

### 2.9 输入输出

Fortran支持输入输出，可以用于读取和写入数据。例如：

```fortran
PRINT *, "Enter your name: "
CHARACTER(LEN=20) :: name
READ *, name
PRINT *, "Hello, ", name, "!"
```

### 2.10 内置函数

以下是Fortran中常用的内置函数的Markdown格式：


#### 1. 数学函数

- `ABS(X)`：返回X的绝对值。<br>
- `SQRT(X)`：返回X的平方根。<br>
- `EXP(X)`：返回e的X次方。<br>
- `LOG(X)`：返回X的自然对数。<br>
- `LOG10(X)`：返回X的以10为底的对数。<br>
- `SIN(X)`：返回X的正弦值（弧度）。<br>
- `COS(X)`：返回X的余弦值（弧度）。<br>
- `TAN(X)`：返回X的正切值（弧度）。<br>
- `ASIN(X)`：返回X的反正弦值（弧度）。<br>
- `ACOS(X)`：返回X的反余弦值（弧度）。<br>
- `ATAN(X)`：返回X的反正切值（弧度）。<br>

#### 2. 字符串处理函数

- `LEN(STRING)`：返回字符串的长度。<br>
- `TRIM(STRING)`：去掉字符串末尾的空格。<br>
- `UPCASE(STRING)`：将字符串转换为大写。<br>
- `LOWCASE(STRING)`：将字符串转换为小写。<br>
- `INDEX(STRING, SUBSTRING)`：返回子字符串在字符串中首次出现的位置。<br>

#### 3. 输入输出函数

- `READ(*,*)`：从标准输入读取数据。<br>
- `WRITE(*,*)`：向标准输出写入数据。<br>
- `PRINT`：格式化输出。<br>

#### 4. 逻辑函数

- `AND(A, B)`：返回A和B的逻辑与。<br>
- `OR(A, B)`：返回A和B的逻辑或。<br>
- `NOT(A)`：返回A的逻辑非。<br>

#### 5. 其他常用函数

- `MAX(A, B)`：返回A和B中的最大值。<br>
- `MIN(A, B)`：返回A和B中的最小值。<br>
- `MOD(A, B)`：返回A除以B的余数。<br>
- `IAND(A, B)`：返回A和B的按位与。<br>
- `IOR(A, B)`：返回A和B的按位或。<br>

### 2.11 Implicit none

任何以字母i,j,k,l,m,n开头的变量名假定为INETEGER，其他字母开头的变量名则假定为REAL。默认情况下没有变量的类型为字符型。<br>

在Fortran中，`implicit none`语句用于禁止隐式类型声明。这意味着在程序中必须显式声明所有变量，否则编译器会报错。<br>

例如：

```fortran
program example
  implicit none
  integer :: i
  real :: x
  character(len=20) :: name
  i = 10
  x = 3.14
  name = "John"
end program example
```

## 3. 实例-计算圆的面积

```fortran
program circle_area
  implicit none
  real :: radius, area
  real, parameter :: pi = ATAN(1.0)*4.0

  ! 输入半径
  write(*,*) "Enter the radius of the circle: "
  read(*,*) radius

  ! 计算面积
  area = pi * radius**2

  ! 输出结果
  write(*,*) "The area of the circle is: ", area
end program circle_area
```

## 4. 实例-冒泡排序

```fortran
program bubble_sort
  implicit none
  integer, dimension(10000000) :: arr
  integer :: i, j, temp
  integer :: n

  ! 输入数组长度
  write(*,*) "Enter the number of elements: "
  read(*,*) n

  ! 输入数组元素
  write(*,*) "Enter the elements: "
  do i = 1, n
    read(*,*) arr(i)
  end do

  ! 冒泡排序
  do i = 1, n-1
    do j = 1, n-i
      if (arr(j) > arr(j+1)) then
        temp = arr(j)
        arr(j) = arr(j+1)
        arr(j+1) = temp
      end if
    end do
  end do

  ! 输出排序后的数组
  write(*,*) "Sorted array: "
  do i = 1, n
    write(*,*) arr(i)
  end do

end program bubble_sort
```

## 5. 实例-矩阵相乘

```fortran
program matrix_multiply
  implicit none
  integer, dimension(3, 3) :: A, B, C
  integer :: i, j, k

  ! 输入矩阵A
  write(*,*) "Enter elements of matrix A: "
  do i = 1, 3
    do j = 1, 3
      read(*,*) A(i, j)
    end do
  end do

  ! 输入矩阵B
  write(*,*) "Enter elements of matrix B: "
  do i = 1, 3
    do j = 1, 3
      read(*,*) B(i, j)
    end do
  end do

  ! 矩阵相乘
  do i = 1, 3
    do j = 1, 3
      C(i, j) = 0
      do k = 1, 3
        C(i, j) = C(i, j) + A(i, k) * B(k, j)
      end do
    end do
  end do

  ! 输出结果矩阵 
  write(*,*) "Resultant matrix: "
  do i = 1, 3
    do j = 1, 3
      write(*,*) C(i, j)
    end do
  end do

end program matrix_multiply
```