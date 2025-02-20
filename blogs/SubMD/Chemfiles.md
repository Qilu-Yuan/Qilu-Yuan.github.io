---
layout: page
permalink: /blogs/SubMD/Chemfiles/index.html
title: 利用Chemfile读取分子动力学轨迹文件
---

## 利用Chemfiles读取分子动力学轨迹文件


​
### Chemfiles介绍

Chemfiles是一个由C++编写的开源的库，主要用于读和写分子模拟中的构型、拓扑与轨迹文件。
​
<br>官网链接：[Chemfiles — read and write chemistry files](https://chemfiles.org/)

<br>Chemfile支持多种程序语言，包括C/C++, Python, Fortran，Julia和Rust

<br>本文主要介绍利用C++与Chemfile来读取一条连续分子动力学轨迹。

### Chemfiles安装

```bash
conda install -c conda-forge chemfiles
```

<br>或自行按照官网教程采用源码安装

### 调用Chemfiles程序的编译

```bash
g++ my-code.cpp -o my-code -I<PREFIX>/include -lchemfiles -L<PREFIX>/lib
# PREFIX为chemfiles的安装路径
```

### Chemfiles读取轨迹文件

```c++
#include <chemfiles.hpp>
#include <iostream>
#include <vector>
\\其余请自行引用

using namespace std;
using namespace chemfiles;

int NFrame, NAtom;


\\读取轨迹文件
auto input = Trajectory("trj.xtc",'r');

NFrame = input.nsteps();   \\frame的总数

\\读取每一帧的坐标
for(int i =0;i<NFrame;i++){
    auto Frame = input.read();
    NAtom = Frame.size(); \\原子数
    auto Coord = Frame.positions();

    \\打印所有原子的坐标
    for(int j =0;j<NAtom;j++){
        cout << "position of the atom " << j+1 << ":" << Coord[j][0] << " " << Coord[j][1] << " " << Coord[j][2] << endl;
    }


    \\ Calculate the properties
}

```
