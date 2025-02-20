---
layout: page
permalink: /blogs/Install/Gcc/index.html
title: 在无法连接外网的服务器上，无root权限的情况下安装gcc
---

## 在无法连接外网的服务器上，无root权限的情况下安装gcc

课题组自购的服务器无法连接外网，只能在内网内通过电脑连接。某次我需要用到高版本的gcc编译器，但是又没有root权限。因此需要用到本文的方法。本文默认本人电脑可以连接外网，但服务器无法连接外网。本人使用系统为ubuntu22.04，gcc版本为11.2.0。
​
### 1：下载并解压

Ubuntu右键本地终端打开位置。然后下载需要的gcc版本

```bash
#下载 11.2.0版本
wget：https://mirrors.tuna.tsinghua.edu.cn/gnu/gcc/gcc-11.2.0/gcc-11.2.0.tar.gz
#解压并进入gcc目录
tar –zxvf gcc-11.2.0.tar.gz && cd gcc-11.2.0
```

### 2：安装依赖项

由于无法连接外网，而我们需要安装推荐的依赖软件，可以去官网查看并手动安装。更简单的办法是先在本机上下载，然后再到服务器上去安装，具体操作为：

<br>接着上一步的terminal

```bash
./contrib/download_prerequisit
```

<br>下载完成后会显示无法创建软连接，关闭该基于本机的远程目录的terminal

<br>直接打开download_prerequist，将221-228行（for到unset）注释*避免下载，

<br>在gcc底层文件夹， Ubuntu右键远程终端打开。再次输入

```bash
./contrib/download_prerequisite
```

<br>此时已经安装好了依赖项

### 3：建立目录并安装

接着当前的terminal输入以下命令（注意将path改成自己的）

```bash
mkdir temp-11.2.0

cd temp-11.2.0

../configure --prefix=/your/install/path --enable-threads=posix --disable-checking --disable-multilib –enable-language=c,c++,fortran --disable-libsanitizer

make –j 16 && make install
```

<br>更改.bashrc路径(注意将路径改为实际安装路径)

```bash
export PATH=/your/install/path/bin:$PATH

export LD_LIBRARY_PATH=/your/install/path/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/your/install/path/lib:$LD_LIBRARY_PATH
```

<br>PS:如果安装时有错误，可能是之前环境变量有其他依赖，此次切换bash以重置环境变量：

```bash
chsh –s /bin/zsh 安装完成在切换回来 chsh -s /bin/bash
```
