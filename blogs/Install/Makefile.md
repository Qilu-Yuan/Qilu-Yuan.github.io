---
layout: page
permalink: /blogs/Install/Makefile/index.html
title: 使用Makefile安装软件的一般流程
---

## 使用Makefile安装软件的一般流程

当遇到需要使用的软件是使用makefile安装的情况下。没有特定功能需求，只是想快速安装，其中一些软件可以按照以下流程操作：

### 1. 下载源码包

### 2. 解压源码包

### 3. 进入源码包目录

```bash
cd <source_code_directory>
```

### 4. 配置安装路径

```bash
./configure --prefix=<install_directory>
```

### 5. 编译

```bash
make
```

### 6. 安装

```bash
make install
```

### 7. 配置环境变量

```bash
export PATH=<install_directory>/bin:$PATH
```

### 8. 验证安装

```bash
<command> --version
```

## 例如OPEN MPI的安装：

```bash
wget https://download.open-mpi.org/release/open-mpi/v2.1/openmpi-2.1.6.tar.gz
tar -zxvf openmpi-4.1.5.tar.gz
cd openmpi-4.1.5
./configure --prefix=/usr/local/openmpi
make
make install
export PATH=/usr/local/openmpi/bin:$PATH
mpirun --version
```
