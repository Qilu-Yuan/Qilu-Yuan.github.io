---
layout: page
permalink: /blogs/Install/linux-web/index.html
title: 在无法连接外网的服务器上，设置代理以连接网络
---

## 在无法连接外网的服务器上，设置代理以连接网络

单位内部的服务器无法连接外网，而我们有时候有联网需求，此时需要设置代理，来将个人主机作为中转服务器。

### 1.搭建本地服务器

需要将个人主机设置为代理服务器。可以使用clashverg或其他软件。这里以clash为例。 [https://clashverge.net/en/](https://clashverge.net/en/)

### 2.配置代理

在clash中配置代理，设置好端口号。假设端口号为7897。

### 3.设置环境变量
在服务器上设置环境变量，指向本地代理服务器。可以在.bashrc文件中添加以下内容：

```bash
export ftp_proxy=http://127.0.0.1:7890
export all_proxy=http://127.0.0.1:7890
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
```
### 4.ssh 连接服务器
使用ssh连接服务器时，添加代理参数：
```bash
ssh -R 7890:localhost:7897 user@server_ip
```
### 5.验证代理设置
在连接后，可以使用以下命令验证代理是否设置成功：
```bash
curl -I http://example.com
```