---
layout: page
permalink: /blogs/SubMD/VMD/index.html
title: 使用VMD可视化lammpsdata文件并渲染出图片简易教程
---

## VMD 绘制分子示意图--lammps

### 读取lammps的data文件 
  
<br>**与主界面相对位置：Extensions---Tk Console**
<br>

```bash
# 进入data文件所在目录
cd work_dir
# 读取data文件
topo readlammpsdata **.dat
# 输出VMD可读的psf文件方便后续直接读取
animate write psf read.psf
```

<br>读取成功

### 绘制美观的分子示意图
  
<br>**与主界面相对位置：Graphic--representations**
<br>Drawing Mrthod：CPK
<br>Resolution 50左右
<br>Create Rep   创建不同的图层
<br>Selected Atoms 选择不同原子
<br>Coloring Method 设置颜色
<br>Material 选择不同材质

### 渲染出图片
<br>**与主界面相对位置：File---Render**
<br>第一栏选择 Tachyon
<br>第二栏 设置图片文件名（一定要设置）
<br>第三栏加上 命令中插入 -res 2560 1440

### 其余部分可选操作
#### Display

##### 景深
<br>Depth Cueing

##### 视角
<br>Orthographic(正交视图) or Perspective(透视视图)