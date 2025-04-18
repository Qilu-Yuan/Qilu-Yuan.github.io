---
layout: page
permalink: /blogs/notes/CMake/index.html
title: CMake学习笔记及简易使用流程
---

## CMake学习笔记及简易使用流程

### 1. CMake简介

CMake 是个一个开源的跨平台自动化建构系统，用来管理软件建置的程序，并不依赖于某特定编译器，并可支持多层目录、多个应用程序与多个函数库。

### 2 Linux系统安装CMake

<br>**在Ubuntu系统下安装CMake**

```bash
sudo apt-get install cmake
```

<br>**检查是否安装成功**

```bash
cmake --version
```

<br>**安装成功**


### 3. CMake基本使用

#### 3.1 CMakeLists.txt文件

<br>**CMakeLists.txt文件是CMake的配置文件，用于描述项目信息，编译规则等。**



<br>**CMakeLists.txt文件的基本结构如下：**

<br> 以下是一个简单的CMakeLists.txt文件示例：主要采用C++20标准，生成可执行文件MyProject，源文件为main.cpp，并指定C++编译器为g++, 调用了chemfiles库

```bash
cmake_minimum_required(VERSION 3.10) # 指定CMake的最低版本要求
#set(CMAKE_CXX_STANDARD 20) # 指定C++的标准
add_executable(MyProject main.cpp) # 指定要生成的可执行文件及其源文件

set (CMAKE_CXX_COMPILER "g++") # 指定C++编译器

set(Chemfile_PATH "path/of/chemfile") # 设置变量 chemfiles库路径

set(target "RunChem") # 设置变量 可执行文件名

add_compile_options(-std=c++20 -O3 -Wall) # 添加编译选项 C++20标准，优化级别3，开启所有警告

add_link_options(-static-libstdc++) # 添加链接选项 静态链接libstdc++库

project(GetChem CXX) # 指定项目名称和语言

aux_source_directory (./src/ SRC_LIST) # 查找指定目录下的所有源文件，并保存到SRC_LIST变量中

include_directories(${Chemfile_PATH}/include) # 添加头文件搜索路径

link_directories(${Chemfile_PATH}/lib) # 添加库文件搜索路径

add_executable(${target} GetStat.cpp ${SRC_LIST} ${Chemfile_PATH}) # 指定要生成的可执行文件及其源文件
target_link_libraries(${target} chemfiles) # 链接库文件

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/../../) # 设置可执行文件输出路径

#set_target_properties(${target} PROPERTIES LINKER_LANGUAGE CXX) # 设置链接语言为C++


```

#### 3.2 CMake常用指令

<br>**1. cmake_minimum_required(VERSION version_number)**
<br>指定CMake的最低版本要求

<br>**2. project(project_name)**
<br>指定项目的名称

<br>**3. set(variable value)**
<br>设置变量的值

<br>**4. add_executable(executable_name source_file1 source_file2 ...)**
<br>指定要生成的可执行文件及其源文件

<br>**5. add_library(library_name source_file1 source_file2 ...)**
<br>指定要生成的库文件及其源文件

<br>**6. target_link_libraries(target library1 library2 ...)**
<br>指定要链接的库文件

<br>**7. include_directories(directory1 directory2 ...)**
<br>指定头文件的搜索路径

<br>**8. link_directories(directory1 directory2 ...)**
<br>指定库文件的搜索路径

<br>**9. find_package(package_name)**
<br>查找并加载指定的包

<br>10. message(message)
<br>输出消息到控制台

<br>**11. if(condition)**
<br>**12. elseif(condition)**
<br>**13. else()**
<br>**14. endif()**
<br>条件语句

<br>
<br>**15. foreach(variable value1 value2 ...)**
<br>**16. endforeach()**
<br>循环语句
<br>

<br>**17. while(condition)**
<br>**18. endwhile()**
<br>循环语句
<br>

<br>**19. break()**
<br>**20. continue()**
<br>循环控制语句

<br>
<br>**21. function(function_name)**

<br>**22. endfunction()**
<br>定义函数
