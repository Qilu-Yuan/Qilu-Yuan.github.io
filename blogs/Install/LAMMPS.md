---
layout: page
permalink: /blogs/Install/LAMMPS/index.html
title: 并行版本的LAMMPS简易安装教程
---

## 并行版本的LAMMPS简易安装教程

### 1. 下载LAMMPS

[LAMMPS官网](https://lammps.sandia.gov/)<br>

下载LAMMPS源码，选择稳定版本，如`lammps-22Aug18`<br>

### 2. 检查依赖

LAMMPS依赖以下库：

- FFT库：FFTW3<br>

- MPI库：OpenMPI<br>

- 数学库：BLAS/LAPACK<br>

- C++编译器：g++<br>

- C编译器：gcc<br>

- make工具<br>


在终端中输入以下命令检查依赖是否满足：<br>

```bash
mpicc --version
mpirun --version
g++ --version
gcc --version
fftw3-config --version
make --version
```

如果以上命令没有报错，则说明依赖满足。如果有报错，则需要安装相应的库。<br>


### 3. 编译LAMMPS

在LAMMPS的`src`目录下，安装需要使用的包<br>
   
首先输入：<br>
```bash
make ps
```
此时会显示所有可用的包，状态均为`Installed  NO: package *`，选择需要的包，然后输入：<br>

```bash
make yes-MOLECULE
make yes-MC
make yes-kspace
make yes-rigid
make yes-srd
make yes-manybody
make yes-user-meam
make yes-user-uef
```

以上是本人需要的包，具体需要哪些包，请参考LAMMPS的官方文档。<br>

再次输入：<br>

```bash
make ps
```

此时将要编译的包会显示`Installed  YES: package *`<br>

确认无误后，输入以下命令进行编译：<br>

```bash
Make mpi
```

编译完成后，会在`src`目录下生成可执行文件`lmp_mpi`。<br>

### 4. 运行LAMMPS

在终端中输入以下命令运行LAMMPS：<br>

```bash
mpirun -np 4 ./lmp_mpi -in in.lammps
```

其中，`-np 4`表示使用4个进程运行LAMMPS，`-in in.lammps`表示使用`in.lammps`文件作为输入文件。<br>


## open-mpi 安装

```bash
wget https://download.open-mpi.org/release/open-mpi/v2.1/openmpi-2.1.6.tar.gz
tar -zxvf openmpi-4.1.5.tar.gz
cd openmpi-4.1.5
./configure --prefix=/usr/local/openmpi #安装路径根据自己要求更改
make
make install
#在～/.bashrc中添加
#export PATH=/usr/local/openmpi/bin:$PATH
mpirun --version
```

## fftw3 安装

```bash
wget http://www.fftw.org/fftw-3.3.8.tar.gz
tar -zxvf fftw-3.3.8.tar.gz
cd fftw-3.3.8
./configure --prefix=/usr/local/fftw3 --enable-mpi --enable-threads#安装路径根据自己要求更改
make
make install
#在～/.bashrc中添加
#export LD_LIBRARY_PATH=/usr/local/fftw3:$LD_LIBRARY_PATH
mpirun --version
```