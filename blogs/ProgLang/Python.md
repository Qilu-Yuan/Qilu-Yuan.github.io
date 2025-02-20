---
layout: page
permalink: /blogs/ProgLang/Python/index.html
title: Python基本语法暨学习笔记
---

## Python基本语法暨学习笔记

## 1. Python简介

Python是一种解释型、面向对象、动态数据类型的高级程序设计语言。Python由Guido van Rossum于1989年底发明，第一个公开发行版发行于1991年。像Perl语言一样，Python 源代码同样遵循 GPL（GNU General Public License）协议。Python语法简洁而清晰，具有很好的可读性，适合作为脚本语言使用。Python可用于快速开发，也非常适合作为学习编程语言的第一个选择。

## 2. Python安装

Python安装包下载地址：https://www.python.org/downloads/

## 3. Python基本语法

### 3.1 Python基础

#### 3.1.1 Python基础语法

- Python中，缩进表示代码块，缩进必须一致，通常使用4个空格。<br>
- Python中，注释使用#号。<br>
- Python中，使用print()函数输出内容。例如：print("Hello, World!")<br>

#### 3.1.2 Python变量

- Python中，变量不需要声明，直接赋值即可。例如：a = 1<br>
- Python中，变量类型由赋值时的数据类型决定。例如：a = 1，a为整数类型；a = "Hello, World!"，a为字符串类型。<br>
- Python中，变量可以同时赋值多个变量。例如：a, b, c = 1, 2, 3 <br>
- Python中，变量可以重新赋值。例如：a = 1，a = "Hello, World!" <br>

``` python
a = 1
print(a)
a = "Hello, World!"
print(a)
```

#### 3.1.3 Python数据类型

- Python中，数据类型包括整数、浮点数、字符串、布尔值、列表、元组、字典、集合等。
- Python中，整数类型包括int和long。
- Python中，浮点数类型包括float和complex。
- Python中，字符串类型包括str和unicode。

``` python
a = 1 # 整数类型
b = 1.0  # 浮点数类型
c = "Hello, World!"  # 字符串类型
d = True  # 布尔值类型
e = [1, 2, 3]  # 列表类型
f = (1, 2, 3)  # 元组类型 单个元素需要加逗号
g = {"name": "Tom", "age": 18} # 字典类型
h = {1, 2, 3} # 集合类型
```

1. **整数**
   - 整数类型包括int和long。
   - int类型表示整数，例如：a = 1。
   - long类型表示长整数，例如：a = 12345678901234567890。

``` python
a = 1 # 整数类型
b = 12345678901234567890 # 长整数类型
```

2. **浮点数**
   - 浮点数类型包括float和complex。
   - float类型表示浮点数，例如：a = 1.0。
   - complex类型表示复数，例如：a = 1 + 2j。

``` python
a = 1.0 # 浮点数类型
b = 1 + 2j # 复数类型

3. **字符串**
   - 字符串类型包括str和unicode。

``` python
a = "Hello, World!" # 字符串类型
b = u"Hello, World!" # unicode字符串类型
```

4. **布尔值**
   - 布尔值类型包括True和False。

``` python
a = True # 布尔值类型
b = False # 布尔值类型
```

5. **列表**
   - 列表类型包括list和tuple。


```pythona = [1, 2, 3] # 列表类型

```

6. **元组**
   - 元组类型包括tuple。

```python
a = (1, 2, 3) # 元组类型
a = (1,) # 单个元素需要加逗号
a = tuple() # 空元组
```

7. **字典**
   - 字典类型包括dict。

```python
a = {"name": "Tom", "age": 18} # 字典类型
```

8. **集合**
   - 集合类型包括set。

```python
a = {1, 2, 3} # 集合类型
```


#### 3.1.4 Python运算符

- Python中，运算符包括算术运算符、比较运算符、逻辑运算符、位运算符、赋值运算符、成员运算符、身份运算符等。<br>
- Python中，算术运算符包括加、减、乘、除、取余、取整除、幂运算等。<br>

```python
a = 10
b = 3
print(a + b)  # 加
print(a - b)  # 减
print(a * b)  # 乘
print(a / b)  # 除
print(a % b)  # 取余
print(a // b)  # 取整除
print(a ** b)  # 幂运算
```

- Python中，比较运算符包括等于、不等于、大于、小于、大于等于、小于等于等。<br>

```python
a = 10
b = 3
print(a == b)  # 等于
print(a != b)  # 不等于
print(a > b)  # 大于
print(a < b)  # 小于
print(a >= b)  # 大于等于
print(a <= b)  # 小于等于
```

- Python中，逻辑运算符包括与、或、非等。

```python
a = True
b = False
print(a and b)  # 与
print(a or b)  # 或
print(not a)  # 非
```

- Python中，位运算符包括按位与、按位或、按位异或、按位取反、左移、右移等。

```python
a = 60  # 60 = 0011 1100
b = 13  # 13 = 0000 1101
print(a & b)  # 按位与 12 = 0000 1100
print(a | b)  # 按位或 61 = 0011 1101
print(a ^ b)  # 按位异或 49 = 0011 0001
print(~a)  # 按位取反 -61 = 1100 0011
print(a << 2)  # 左移 240 = 1111 0000
print(a >> 2)  # 右移 15 = 0000 1111
```

- Python中，赋值运算符包括等于、加等于、减等于、乘等于、除等于、取余等于、取整除等于、幂等于等。

```python
a = 10
b = 3
a += b  # 加等于
a -= b  # 减等于
a *= b  # 乘等于
a /= b  # 除等于
a %= b  # 取余等于
a //= b  # 取整除等于
a **= b  # 幂等于
```

- Python中，成员运算符包括in、not in等。

```python
a = [1, 2, 3, 4, 5]
print(3 in a)  # True
print(6 not in a)  # True
```

- Python中，身份运算符包括is、is not等。

```python
a = [1, 2, 3, 4, 5]
b = a
print(a is b)  # True
print(a is not b)  # False
```

#### 3.1.5 条件语句

- Python中，条件语句包括if、elif、else等。

```python
a = 10
if a > 5:
    print("a大于5")
elif a == 5:
    print("a等于5")
else:
    print("a小于5")
```

#### 3.1.6 循环语句

- Python中，循环语句包括for、while等。

```python
a = [1, 2, 3, 4, 5]
for i in a:
    print(i)

i = 0
while i < 5:
    print(i)
    i += 1
```

#### 3.1.7 函数

- Python中，函数定义使用def关键字。

```python
def add(a, b):
    return a + b

print(add(1, 2))
```

#### 3.1.8 lambda

- Python中，lambda表达式用于创建匿名函数。

```python
add = lambda a, b: a + b
print(add(1, 2))

```

#### 3.1.9 类

- Python中，类定义使用class关键字。

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def say_hello(self):
        print("Hello, my name is " + self.name + ", I am " + str(self.age) + " years old.")

p = Person("Tom", 18)
p.say_hello()
```

#### 3.1.10 异常处理

- Python中，异常处理使用try、except、finally等关键字。

```python
try:
    a = 10 / 0
except ZeroDivisionError:
    print("除数不能为0")
finally:
    print("程序结束")
```

#### 3.1.11 文件操作

- Python中，文件操作使用open、read、write等函数。

```python
f = open("test.txt", "r")
print(f.read())
f.close()

f = open("test.txt", "w")
f.write("Hello, world!")
f.close()
```

#### 3.1.12 模块

- Python中，模块是包含函数、类、变量等的文件。

```python
import math
print(math.sqrt(9))

from math import sqrt
print(sqrt(9))
```

#### 3.1.13 包

- Python中，包是包含模块的文件夹。
- 包的目录结构如下：

```
my_package/
    __init__.py
    module1.py
    module2.py
```

- 使用包时，需要在__init__.py文件中添加以下代码：

```python
from .module1 import *
from .module2 import *
```

- 使用包时，需要在代码中添加以下代码：

```python
import my_package
```

#### 3.1.14 生成器

- Python中，生成器是一种特殊的迭代器，使用yield关键字。

```python
def my_generator():
    yield 1
    yield 2
    yield 3

g = my_generator()
print(next(g))
print(next(g))
print(next(g))
```

#### 3.1.15 装饰器

- Python中，装饰器是一种特殊的函数，用于修改其他函数的行为。

```python
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def my_function():
    print("Inside function")

my_function()


#输出： Before function call 
# Inside function 
# After function call
```

```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")


#输出： Hello, Alice! 
# Hello, Alice! 
# Hello, Alice!
```


#### 3.1.16 异步编程

- Python中，异步编程是一种特殊的编程方式，使用async和await关键字。

```python
import asyncio

async def my_function():
    print("Before function call")
    await asyncio.sleep(1)
    print("After function call")

asyncio.run(my_function())

#输出： Before function call  After function call
```

#### 3.1.17 迭代器

- Python中，迭代器是一种特殊的对象，用于遍历可迭代对象。

```python
my_list = [1, 2, 3]
my_iterator = iter(my_list)
print(next(my_iterator))
print(next(my_iterator))
print(next(my_iterator))
#输出：1 2 3
```

#### 3.1.18 生成器表达式

- Python中，生成器表达式是一种特殊的表达式，用于生成生成器。

```python
my_generator = (x for x in range(10))
print(next(my_generator))
print(next(my_generator))
print(next(my_generator))

#输出：0 1 2

# 生成器表达式可以用于列表推导式
my_list = [x for x in range(10)]
print(my_list)
#输出：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 3.2 标准库函数

#### 3.2.1 os模块

- os模块是Python标准库中用于处理操作系统相关任务的模块。

```python
import os

# 获取当前工作目录
print(os.getcwd())

# 列出当前目录下的文件和文件夹
print(os.listdir())

# 创建文件夹
os.mkdir("my_folder")

# 删除文件夹
os.rmdir("my_folder")

# 获取文件大小
print(os.path.getsize("my_file.txt"))

# 判断文件是否存在
print(os.path.exists("my_file.txt"))

# 获取文件扩展名
print(os.path.splitext("my_file.txt")[1])
#输出：.txt

# 获取文件名
print(os.path.basename("my_file.txt"))
#输出：my_file.txt

# 获取文件路径
print(os.path.dirname("my_file.txt"))
#输出：.

# 命令行操作
os.system("ls")
#输出： my_file.txt

```

#### 3.2.2 sys模块

- sys模块是Python标准库中用于处理系统相关任务的模块。

```python
import sys

# 获取命令行参数
print(sys.argv)

# 退出程序
sys.exit()

# 获取系统平台
print(sys.platform)

# 获取Python版本
print(sys.version)

# 获取Python解释器的路径
print(sys.executable)
```

#### 3.2.3 datetime模块

- datetime模块是Python标准库中用于处理日期和时间的模块。

```python
from datetime import datetime, timedelta

# 获取当前时间
now = datetime.now()
print(now)

# 格式化时间
formatted_now = now.strftime("%Y-%m-%d %H:%M:%S")
print(formatted_now)

# 解析时间字符串
parsed_time = datetime.strptime("2022-01-01 12:00:00", "%Y-%m-%d %H:%M:%S")
print(parsed_time)

# 时间加减
future_time = now + timedelta(days=1, hours=2)
print(future_time)
```

#### 3.2.4 glob模块

- glob模块是Python标准库中用于文件路径匹配的模块。

```python
import glob

# 获取当前目录下所有以.txt结尾的文件
files = glob.glob("*.txt")
print(files)
```

#### 3.2.5 json模块

- json模块是Python标准库中用于处理JSON数据的模块。

```python
import json

# 将Python对象转换为JSON字符串
data = {"name": "Alice", "age": 25}
json_str = json.dumps(data)
print(json_str)

# 将JSON字符串转换为Python对象
json_obj = json.loads(json_str)
print(json_obj)
```

#### 3.2.6 re模块

- re模块是Python标准库中用于处理正则表达式的模块。

```python
import re

# 匹配字符串
pattern = r"\d+"
result = re.match(pattern, "123abc")
print(result)

# 查找所有匹配项
result = re.findall(pattern, "123abc456def")
print(result)
```

#### 3.2.7 subprocess模块

- subprocess模块是Python标准库中用于创建和管理子进程的模块。

```python
import subprocess

# 执行命令
result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print(result.stdout)
```
#### 3.2.8 math模块

- math模块是Python标准库中用于处理数学运算的模块。

```python
import math

# 计算平方根
result = math.sqrt(9)
print(result)

# 计算最大公约数
result = math.gcd(12, 18)
print(result)
```

#### 3.2.9 random模块

- random模块是Python标准库中用于生成随机数的模块。

```python
import random

# 生成随机整数
result = random.randint(1, 10)
print(result)

# 生成随机浮点数
result = random.uniform(1.0, 10.0)
print(result)
```
