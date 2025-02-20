---
layout: page
permalink: /blogs/SubMD/Chemfiles2/index.html
title: 利用Chemfile读取Gromacs的轨迹与拓扑结构
---

## 利用Chemfile读取Gromacs的轨迹与拓扑结构

​
### 简要说明

gromacs进行模拟的工作中，我们通常需要输出其轨迹方便进行性质的计算。之前的文章，[利用Chemfile读取分子动力学轨迹文件](https://qilu-yuan.github.io/blogs/Chemfiles/)，简要介绍了如何读取gromacs轨迹中的坐标信息。很多时候我们进行后处理计算还需要一些分子拓扑的信息。本文介绍如何采用C++与Chemfile库读取gromacs轨迹的原子坐标与拓扑结构。

​
### Chemfiles介绍

Chemfiles是一个由C++编写的开源的库，主要用于读和写分子模拟中的构型、拓扑与轨迹文件。
​
<br>官网链接：[Chemfiles — read and write chemistry files](https://chemfiles.org/)

<br>Chemfile支持多种程序语言，包括C/C++, Python, Fortran，Julia和Rust


### 轨迹与拓扑读取

在此需要两个文件，分别是包含拓扑结构的tpr文件：data.tpr , 与轨迹文件trj.trr


<br>输出基本信息，包括轨迹文件中的帧数，原子数，键数，角度数，二面角数，残基数，模拟盒子大小

```c++
#include <chemfiles.hpp>
#include <iostream>
#include <vector>
\\其余请自行引用

using namespace std;
using namespace chemfiles;

int NFrame, NAtom;
int NBond, NAngle, NDihedral,NRes;


\\读取轨迹文件
auto input = Trajectory("trj.trr",'r');
input.set_topology("data.tpr", "TPR");

NFrame = input.nsteps();   \\frame的总数

\\读取第一帧的坐标与拓扑结构

auto Frame = input.read();
NAtom = Frame.size(); \\原子数
auto Topo = Frame.topology(); \\读取拓扑结构

\\键数，键角数，二面角数,残基数
NBond = Topo.bonds().size();
NAngle = Topo.angles().size();
NDihedral = Topo.dihedrals().size();
NRes = Topo.residues().size();

\\模拟盒子大小
auto cell = Frame.cell();
float Box = cell.lengths()[0];
float Vol = cell.volume();


```

<br>输出键，键角，二面角的大小，所有原子的坐标

```c++
\\计算键角大小
auto Bonds = Topo.bonds();

for (size_t i = 0; i < (*NBond); i++) {
    \\键长度
    double lb = Frame.distance(Bonds[i][0],Bonds[i][1]);

    cout << "bond "<<i<< ":" <<Bonds[i][0]+1<<","<<Bonds[i][1]+1<<":"<< lb <<endl;
        // cout<<Bond[0]<<" "<<Bond[1]<<endl;        
}

\\计算键角
auto Angles = Topo.angles();

for (size_t i = 0; i < (*NAngle); i++) {
    \\键角大小
    double la = Frame.angle(Angles[i][0],Angles[i][1],Angles[i][2]);
    la = la*180/3.1415926;

    cout << "angle "<<i<< ":" <<Angles[i][0]+1<<","<<Angles[i][1]+1<<","；
    cout<<Angles[i][2]+1 << ":"<<la<<endl;
}
\\计算二面角

auto Dihedrals = Topo.dihedrals();

for (size_t i = 0; i < (*NDihedral); i++) {
    double ld = Frame.dihedral(Dihedrals[i][0],Dihedrals[i][1],Dihedrals[i][2],Dihedrals[i][3]);
    ld = ld*180/3.1415926;
    cout << "dihedral "<<i<< ":" <<Dihedrals[i][0]+1<<","<<Dihedrals[i][1]+1<<",";
    cout<<Dihedrals[i][2]+1<<","<<Dihedrals[i][3]+1<< ":"<< ld <<endl;
}


\\读取每一帧的坐标与拓扑结构
for(int i =0;i<NFrame;i++){
    \\读取第i帧的坐标
    if(i==0){
        \\回到轨迹文件的开头
        auto Frame = input.read_step(size_t 0);
        
    }
    else{
        auto Frame = input.read();    
    }
    
    NAtom = Frame.size(); \\原子数
    auto Coord = Frame.positions();

    \\打印所有原子的坐标
    for(int j =0;j<NAtom;j++){
        cout << "position of the atom " << j+1 << ":" << Coord[j][0] << " " << Coord[j][1] << " " << Coord[j][2] << endl;
    }


    \\ Calculate the properties
}

```
