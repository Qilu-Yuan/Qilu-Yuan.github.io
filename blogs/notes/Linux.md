---
layout: page
permalink: /blogs/notes/Linux/index.html
title: Linux常用命令与操作
---

## **Linux常用命令与操作**

## 1. 系统信息

```bash
cat /proc/cpuinfo #显示CPU info的信息
cat /proc/interrupts #显示中断
cat /proc/meminfo #校验内存使用和空闲情况
cat /proc/locks #列出当前持有锁的文件
cat /proc/version #查看内核的版本
```

## 2. 文件和目录

### 1. **ls命令**

   ```bash
   ls -l #显示文件和目录的详细资料
   ls -a #显示所有文件和目录(包括隐藏的)
   ls -R #递归列出子目录
   ls -t #按时间排序
   ls -S #按文件大小排序
   ls -r #反向排序
   ls -F #在文件名后添加符号，以区分不同类型
   ```

### 2. **cd命令**

   ```bash
   cd #进入用户主目录
   cd ~ #进入用户主目录
   cd - #返回上次所在的目录
   cd .. #返回上一级目录
   cd ../.. #返回上两级目录
   cd / #进入根目录
   cd /usr/local #进入“/usr/local”目录
   cd /usr #进入“/usr”目录
   cd -P #跳转到实际物理路径，而非符号链接路径
   ```

### 3. **pwd命令**

   ```bash
   pwd #显示当前工作路径
   ```

### 4. **mkdir命令**

   ```bash
   mkdir dir1 #创建一个叫做'dir1'的目录
   mkdir dir1 dir2 #同时创建两个目录
   mkdir -p /tmp/dir1/dir2 #创建一个目录树
   ```


### 5. **cp命令**

   ```bash
   cp file1 file2 #复制file1为file2
   cp file1 file2 dir #复制file1为dir/file2
   cp -a dir1 dir2 #复制一个目录
   cp -i #若目标文件存在时，询问是否覆盖
   cp -r #递归复制整个目录
   cp -u #若目标文件存在且比源文件旧，则更新
   ```

### 6. **mv命令**

   ```bash
   mv old_file new_file #重命名文件或移动文件
   mv dir1 dir2 #移动整个目录
   ```

### 7. **rm命令**

   ```bash
   rm file #删除“file”
   rm -i file #交互式删除
   rm -r dir #删除非空目录
   rm -f file #强制删除文件
   rm -rf dir #强制删除非空目录
   ```

### 8. **ln命令**

   ```bash
   ln source_file target_file #创建硬链接
   ln -s source_file target_file #创建符号链接
   ```

### 9. **find命令** 

   ```bash
   find dir -name file #在目录中查找文件
   find dir -type f -name file #在目录中查找文件
   find dir -type d -name dir #在目录中查找目录
   find dir -size +100M #查找大于100M的文件
   find dir -mtime +7 #查找7天前修改的文件
   find dir -user user #查找用户user的文件
   ```

### 10. **grep命令**

   ```bash
   grep pattern file #在文件中查找模式
   grep -r pattern dir #在目录中递归查找模式
   grep -i pattern file #忽略大小写查找模式
   grep -v pattern file #反向查找模式
   ```

### 11. **tar命令**

   ```bash
   tar -c #创建新的归档文件
   tar -x #从归档文件中提取文件
   tar -t #列出归档文件的内容
   tar -z #使用gzip压缩/解压缩归档文件
   tar -j #使用bzip2压缩/解压缩归档文件
   tar -v #显示详细信息
   tar -f #指定归档文件名
   tar -C #指定提取目录
   ```

    压缩<br>
   tar -czvf archive.tar.gz dir #将目录压缩为gzip格式的归档文件
    解压<br>
   tar -xzvf archive.tar.gz #将gzip格式的归档文件解压缩到当前目录
   tar -xzvf archive.tar.gz -C /path/to/dir #将gzip格式的归档文件解压缩到指定目录

### 12. **zip与unzip命令**

    ```bash
    zip archive.zip file #将文件压缩为zip格式的归档文件
    unzip archive.zip #将zip格式的归档文件解压缩到当前目录
    unzip archive.zip -d /path/to/dir #将zip格式的归档文件解压缩到指定目录
    ```


## 3.网络相关

### 1. **rsync命令**

   ```bash
   rsync source_file target_file #将文件同步到目标文件
   rsync source_dir target_dir #将目录同步到目标目录
   rsync -a source_dir target_dir #以归档模式同步目录
   rsync -v source_dir target_dir #显示详细信息
   rsync -z source_dir target_dir #使用压缩传输数据
   rsync -r source_dir target_dir #递归同步目录
   rsync -u source_dir target_dir #仅同步更新的文件
   ```

### 2. **ssh命令**

   ```bash
   ssh user@hostname #连接到远程主机
   ssh -L local_port:remote_host:remote_port user@hostname #将本地端口转发到远程主机
   ssh -R remote_port:local_host:local_port user@hostname #将远程端口转发到本地主机
   ssh -D local_port user@hostname #创建一个SOCKS代理
   ssh -p port user@hostname #使用指定端口连接到远程主机
   ssh -i identity_file user@hostname #使用指定私钥文件连接到远程主机
   ssh -v user@hostname #显示详细信息
   ```


### 3. **ssh-keygen命令**

   ```bash
   ssh-keygen #生成SSH密钥对
   ssh-keygen -t rsa #生成RSA密钥对
   ssh-keygen -t dsa #生成DSA密钥对
   ssh-keygen -t ecdsa #生成ECDSA密钥对
   ssh-keygen -t ed25519 #生成ED25519密钥对
   ssh-keygen -b bits #设置密钥长度
   ssh-keygen -C comment #添加注释
   ssh-keygen -f filename #指定密钥文件名
   ssh-keygen -p #更改密钥密码
   ssh-keygen -l #显示公钥信息
   ssh-keygen -y #显示私钥信息
   ```

### 4. **ssh-copy-id命令**

   ```bash
   ssh-copy-id user@hostname #将公钥复制到远程主机
   ssh-copy-id -i identity_file user@hostname #使用指定私钥文件复制公钥
   ssh-copy-id -f filename user@hostname #指定密钥文件名
   ssh-copy-id -p port user@hostname #使用指定端口连接到远程主机
   ssh-copy-id -v user@hostname #显示详细信息
   ```

### 5. **ss命令**

   ```bash
   ss #显示所有网络连接
   ss -t #显示TCP连接
   ss -u #显示UDP连接
   ss -l #显示监听端口
   ss -n #显示数字地址和端口号
   ss -p #显示进程信息
   ss -m #显示内存使用情况
   ss -o #显示计时器信息
   ss -i #显示ICMP信息
   ```   

### 6. **scp命令**

   ```bash
   scp #复制文件和目录
   scp local_file remote_user@remote_host:remote_directory #将本地文件复制到远程主机
   scp remote_user@remote_host:remote_directory local_directory #从远程主机复制文件到本地
   scp -r local_directory remote_user@remote_host:remote_directory #将本地目录复制到远程主机
   scp -r remote_user@remote_host:remote_directory local_directory #从远程主机复制目录到本地
   scp -P port local_file remote_user@remote_host:remote_directory #使用指定端口连接到远程主机
   scp -v local_file remote_user@remote_host:remote_directory #显示详细信息
   scp -p local_file remote_user@remote_host:remote_directory #保留源文件的修改时间、访问时间和访问权限
   scp -r -p local_directory remote_user@remote_host:remote_directory #保留源目录的修改时间、访问时间和访问权限
   ```

## 4. 系统管理

### 1. **df命令**

   ```bash
   df #显示文件系统的磁盘空间使用情况
   df -h #以人类可读的格式显示文件系统的磁盘空间使用情况
   df -T #显示文件系统的类型
   df -i #显示inode使用情况
   df -t ext4 #显示ext4文件系统的磁盘空间使用情况
   df -t ext4 -h #以人类可读的格式显示ext4文件系统的磁盘空间使用情况
   df -t ext4 -i #显示ext4文件系统的inode使用情况
   ```

### 2. **du命令**

   ```bash
   du #显示目录或文件的大小
   du -h #以人类可读的格式显示目录或文件的大小
   du -s #显示目录或文件的总大小
   du -a #显示目录或文件的大小，包括子目录和文件
   du -c #显示目录或文件的大小，包括子目录和文件的总大小

   du -sh /home #显示/home目录的大小
   du -sh /home/* #显示/home目录下所有文件和子目录的大小
   du -sh /home/* | sort -hr #以人类可读的格式显示/home目录下所有文件和子目录的大小，并按大小排序
   du -sh /home/* | sort -hr | head -n 10 #以人类可读的格式显示/home目录下所有文件和子目录的大小，并按大小排序，只显示前10个
   ```

### 3. **free命令**

   ```bash
   free #显示内存使用情况
   free -h #以人类可读的格式显示内存使用情况
   free -m #以MB为单位显示内存使用情况
   free -g #以GB为单位显示内存使用情况
   free -t #显示内存使用情况，包括交换空间
   free -b #以字节为单位显示内存使用情况
   free -o #以人类可读的格式显示内存使用情况，不包括交换空间
   free -s 5 #每5秒显示一次内存使用情况
   ```

### 4. **top命令**

   ```bash
   top #显示系统进程信息
   top -c #显示进程命令行
   top -u user #显示指定用户的进程信息
   top -p pid #显示指定进程的详细信息
   top -b -n 1 #以批处理模式显示系统进程信息，只显示一次
   ```

## 5.权限管理

### 1. **chmod命令**

   ```bash
   chmod 777 file #修改文件或目录的权限为所有者、所属组和其他用户都有读、写、执行权限

    #7：读、写、执行权限
    #6：读、写权限
    #5：读、执行权限
    #4：读权限
    #3：写、执行权限
    #2：写权限
    #1：执行权限
    #0：无权限

   ```

### 2. **chown命令**

   ```bash
   chown #修改文件或目录的所有者
   chown user file #修改文件或目录的所有者为user
   chown user:group file #修改文件或目录的所有者为user，所属组为group
   chown -R user:group dir #修改目录及其子目录和文件的所有者为user，所属组为group
   ```

### 3. **chgrp命令**

   ```bash
   chgrp #修改文件或目录的所属组
   chgrp group file #修改文件或目录的所属组为group
   chgrp -R group dir #修改目录及其子目录和文件的所属组为group
   ```

## 6.文本处理

### 1. **cat命令**

   ```bash
   cat file #显示文件内容
   cat file1 file2 #将file1和file2的内容合并显示
   cat -n file #显示文件内容，并显示行号
   cat -b file #显示文件内容，不显示空行
   cat -s file #显示文件内容，合并连续的空行
   ```

### 2. **more命令**

   ```bash
   more file #分页显示文件内容
   more -d file #分页显示文件内容，并在屏幕底部显示提示信息
   more -p file #分页显示文件内容，并清除屏幕上的内容
   ```

### 3. **less命令**

   ```bash
   less file #分页显示文件内容，可以向上滚动
   less -N file #分页显示文件内容，并显示行号
   less -S file #分页显示文件内容，不自动换行
   ```

### 4. **head命令**

   ```bash
   head file #显示文件的前10行内容
   head -n 5 file #显示文件的前5行内容
   ```

### 5. **tail命令**

   ```bash
   tail file #显示文件的最后10行内容
   tail -n 5 file #显示文件的最后5行内容
   tail -f file #实时显示文件的最后10行内容
   ```

### 6. **sed命令**

   ```bash
   sed 's/old/new/g' file #将文件中的old替换为new
   sed -i 's/old/new/g' file #将文件中的old替换为new，并直接修改文件
   sed -n '2p' file #显示文件的第二行内容
   sed -n '/pattern/p' file #显示文件中包含pattern的行内容
   sed -e 's/old/new/g' -e 's/old2/new2/g' file #将文件中的old替换为new，old2替换为new2
   ```

### 7. **grep命令**

   ```bash
   grep pattern file #在文件中搜索包含pattern的行
   grep -i pattern file #在文件中搜索包含pattern的行，不区分大小写
   grep -v pattern file #在文件中搜索不包含pattern的行
   grep -r pattern dir #在目录及其子目录中搜索包含pattern的行
   ```


### 8. **管道 | 和 ||**


   ```bash
   command1 | command2 #将command1的输出作为command2的输入
   command1 || command2 #如果command1执行失败，则执行command2
   ```


### 9. **>, >>**

   ```bash
   > file #将标准输出重定向到文件，如果文件不存在则创建，如果文件存在则覆盖
   >> file #将标准输出重定向到文件，如果文件不存在则创建，如果文件存在则在文件末尾追加
   ```

### 10. **<, <<**

   ```bash
   < file #将文件内容作为标准输入
   << EOF #将EOF之间的内容作为标准输入
   ```

### 11. **&**

   ```bash
   command & #将命令放入后台执行
   ```

## 6.挂载系统盘

```bash
mount /dev/sda1 /mnt
```

## 7.软件安装

### 1. **apt-get**

   ```bash
   sudo apt-get update #更新软件包列表
   sudo apt-get install package_name #安装软件包
   sudo apt-get remove package_name #卸载软件包
   sudo apt-get upgrade #升级所有软件包
   ```
    debian

### 2. **yum**

   ```bash
   sudo yum update #更新软件包列表
   sudo yum install package_name #安装软件包
   sudo yum remove package_name #卸载软件包
   sudo yum upgrade #升级所有软件包
   ```
    redhat

### 3. **dnf**

   ```bash
   sudo dnf update #更新软件包列表
   sudo dnf install package_name #安装软件包
   sudo dnf remove package_name #卸载软件包
   sudo dnf upgrade #升级所有软件包
   ```
    fedora

### 4. **pacman**

   ```bash
   sudo pacman -Syu #更新软件包列表并升级所有软件包
   sudo pacman -S package_name #安装软件包
   sudo pacman -R package_name #卸载软件包
   ```
    archlinux

### 5. **dpkg**

   ```bash
   sudo dpkg -i package_name.deb #安装软件包
   sudo dpkg -r package_name #卸载软件包
   ```
