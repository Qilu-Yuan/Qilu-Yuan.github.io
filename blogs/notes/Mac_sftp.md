---
layout: page
permalink: /blogs/notes/Mac_sftp/index.html
title: Mac电脑使用CommanderOnePro在Finder上挂载远程服务器，并且终端直接打开远程路径
---

# 在 Mac 上通过 Commander One Pro 挂载 SFTP 服务器，并实现终端直接打开远程路径


<br>本人需要频繁在远程服务器提交任务和处理数据，图形化界面操作一直是我首选的工作方式。在 Ubuntu 系统中，我习惯通过文件管理器直接挂载 SFTP 服务器，并利用「在远程打开终端」的功能快速进入工作目录。然而，当近期换用 Mac 后，我需要寻找一种替代方案来延续这一高效的工作流。

---

## 方案选择与配置：Commander One Pro 的实践

<br>在 Mac 生态中, **Commander One Pro** 和 **RemoteDrive** 两款付费工具可以实现上述流程。以下是以前者为例的使用流程

### 步骤详解：挂载 SFTP 到 Finder

1. **安装 Commander One Pro**  <br>

2. **创建 SFTP 连接**  <br>
   - 点击右上角 **"连接"** 按钮：  <br>
     ![连接按钮](/Figure/Mac_sftp/1.png)  
   - 选择 **FTP** 协议：  <br>
     ![选择 FTP](/Figure/Mac_sftp/2.png)  
   - 填写配置：  <br>
     - **用户名**：需以 `username@hostname` 格式填写（如 `devuser@192.168.1.100`）<br>
     - **类型**：选择SFTP  <br>
     - **服务器**：服务器的IP  <br>
     - **登陆和密码**：个人在服务上的用户名于密码  <br>
     ![填写信息](/Figure/Mac_sftp/3.png)  <br>
   - 点击 **连接**，即可在 Finder 的 `.COVolumes` 目录中看到挂载的远程文件。<br>

3. **Finder中显示远程文件夹**  <br>
   
   - 需要在**Commander One Pro**的界面上直接双击打开一个文件<br>

   - 然后就能在Finder上的用户家目录（本人是/Users/yuanqilu）下的`.COVolumes`文件夹内找到远程的目录了<br>
    
---

## 关键优化：终端直接进入远程路径

尽管 Finder 可视化操作便捷，但开发者常需在终端执行命令。Mac 的 Finder 默认右键「在终端中打开」功能仅能进入本地挂载点路径（如 `/Users/yourname/.COVolumes/username@hostname`），而非真正的远程服务器路径。<br>

ps：（option+command+P）可打开路径显示<br>

### 解决方案：Python 脚本自动化跳转
我编写了一个 Python 脚本 **`CdSftp.py`**，通过解析本地路径自动建立 SSH 连接并定位到远程对应目录：<br>

```python
import os
import sys
from subprocess import call

def getssh():
    current_path = os.getcwd().split('/')
    
    # 检查路径是否符合 .COVolumes 结构
    if len(current_path) > 4 and current_path[3] == '.COVolumes':
        # 解析用户名和主机名
        user_host = current_path[4].split('@')
        host = user_host[1]
        user = user_host[0][1:]  # 去除开头的 '.'（因路径格式为 .username@hostname）
        
        # 拼接远程路径
        remote_path = '/'.join(current_path[5:]) or '/'

        print(remote_path)
        # 执行 SSH 并跳转到目标路径
        call(f'ssh -t {user}@{host} "cd /{remote_path}; exec bash --login"', shell=True)

if __name__ == "__main__":
    getssh()
```

#### 脚本说明：

- **路径解析逻辑**：通过分割本地路径 `.COVolumes/username@hostname/path/to/dir`，提取主机信息并构造远程路径。<br>

- **SSH 参数**：`-t` 强制分配终端，`exec bash --login` 确保环境变量正确加载。<br>

### 自动化集成：一键调用

将脚本路径添加到 `~/.zshrc`（或 `~/.bashrc`），创建别名实现快捷操作：<br>

```bash
# 1. 将脚本保存到指定路径（如 ~/scripts/CdSftp.py）
# 2. 在终端执行：
echo 'alias sftp-cd="python ~/scripts/CdSftp.py"' >> ~/.zshrc
source ~/.zshrc
```

#### 使用方式：

1. 在 Finder 中右键点击目录 → **在终端中打开**  <br>

2. 输入 `sftp-cd`，即可直接进入远程对应路径！<br>

---

## 使用体验与注意事项

1. **路径一致性**：确保本地挂载路径与远程目录结构完全一致，否则脚本可能无法正确跳转。<br>

2. **SSH 密钥配置**：若使用密钥认证，需提前在 `~/.ssh/config` 中配置服务器信息，避免每次输入密码。<br>

3. **性能优化**：大文件传输建议直接使用 Commander One Pro 的传输功能，终端 SSH 更适合轻量操作。<br>

---

## 总结

通过 Commander One Pro 的图形化挂载与自定义脚本的结合，我成功在 Mac 上复现了 Ubuntu 的 SFTP 工作流。这一方案不仅提升了跨平台开发的便利性，更通过代码自动化减少了手动操作的冗余。希望这篇指南能帮助同样需要 Mac SFTP 集成的开发者节省探索时间！<br>

