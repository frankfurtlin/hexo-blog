---
title: VSCode 配置 C++ 运行环境
date: 2023-04-25 23:26:54
tags:
    - VSCode
    - C++
categories: C++
cover: http://cdn.frankfurtlin.top/blog/covers/cover10.jpg
---

# VSCode 配置 C++ 运行环境

## Windows

- 安装编译工具
``` bash
# 安装 Microsoft Visual Studio
(https://visualstudio.microsoft.com/zh-hans/)
# 安装 cmake
(https://cmake.org/download/)
```

- 配置环境
``` bash
# 设置系统变量 INCLUDE
D:\vs2022\IDE\VC\Tools\MSVC\14.33.31629\include（仅供参考）
# 设置系统变量 LIB
D:\vs2022\IDE\VC\Tools\MSVC\14.33.31629\lib\x86;
D:\vs2022\IDE\VC\Tools\MSVC\14.33.31629\lib\x64
# 设置 Path 变量添加如下
D:\vs2022\IDE\VC\Tools\MSVC\14.33.31629\bin\Hostx64\x64
D:\vs2022\IDE\VC\Tools\MSVC\14.33.31629\bin\Hostx64\x86
D:\cmake\bin
```

- 确认环境配置
``` bash
# 确认 MSVC 编译器
cl
# 输出类似于
# 用于 x64 的 Microsoft (R) C/C++ 优化编译器 19.33.31630 版
# 版权所有(C) Microsoft Corporation。保留所有权利。
# 用法: cl [ 选项... ] 文件名... [ /link 链接选项... ]
cmake --version
# 输出类似于
# cmake version 3.25.1
# CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

- 配置 VSCode 的 C/C++ 编译器版本
``` json
"C_Cpp.default.cppStandard": "c++20",
"C_Cpp.default.cStandard": "c11",
```

- 在项目同级目录下编写 CMakeLists.txt
``` cmake
cmake_minimum_required(VERSION 3.10)

# 设置项目名称和版本号
project(MyProject VERSION 1.0)

# 设置每次构建都是重新构建
# set(CMAKE_ALWAYS_BUILD TRUE)

# 设置C++标准为C++14
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 设置构建类型
# set(CMAKE_BUILD_TYPE Release)

# 获取当前文件夹下所有的源文件
aux_source_directory(. DIR_SRCS)

# 遍历所有源文件并添加到可执行文件
foreach(src_file ${DIR_SRCS})
    # 获取不带文件后缀的文件名作为可执行文件的文件名
    get_filename_component(exe_name ${src_file} NAME_WE)
    # 添加可执行文件
    add_executable(${exe_name} ${src_file})
    # 设置编译选项
    # target_compile_options(${exe_name} PRIVATE -Wall -Wextra -pedantic)
    # 设置 C++ 标准为 C++17
    # target_compile_features(${exe_name} PRIVATE cxx_std_17)
endforeach()

# 设置链接选项
# target_link_libraries(${exe_name} PRIVATE MyLibrary)

# 添加自定义命令，用于运行可执行文件
# add_custom_command(TARGET ${exe_name} POST_BUILD
#                    COMMAND ${EXECUTABLE_OUTPUT_PATH}/${exe_name})
```

- 编译构建项目
``` bash
mkdir build && cd build
cmake ..
cmake --build . --config Release
# 最后即可在 Debug/Release 目录下生成可执行文件
```

## MacOS

- 安装 cmake
``` bash
brew install cmake
```

- 验证环境
``` bash
g++ -v
cmake --version
```

- 在项目同级目录下编写 CMakeLists.txt
``` cmake
cmake_minimum_required(VERSION 3.10)

# 设置项目名称和版本号
project(my_executable VERSION 1.0)

# 设置每次都是重新构建
# set(CMAKE_ALWAYS_BUILD TRUE)

# 获取当前文件下所有的源文件
aux_source_directory(. DIR_SRCS)

# 遍历每个文件添加到可执行目标文件
foreach(src_file ${DIR_SRCS})
    get_filename_component(exe_name ${src_file} NAME_WE)
    add_executable(${exe_name} ${src_file})
    # 设置输出路径
    set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
    # 设置编译选项
    target_compile_options(${exe_name} PRIVATE -Wall -Wextra -pedantic)
    # 将C++标准设置为C++11
    target_compile_features(${exe_name} PRIVATE cxx_std_14)
endforeach(src_file ${DIR_S})

# 添加可执行文件
# add_executable(my_executable thread.cpp)

# 设置链接选项
# target_link_libraries(my_executable PRIVATE MyLibrary)

# 添加自定义命令，用于运行可执行文件
# add_custom_command(TARGET my_executable POST_BUILD
#                    COMMAND ${EXECUTABLE_OUTPUT_PATH}/my_executable)
```

- 编译构建项目
``` bash
mkdir build && cd build
cmake ..
make
# 即可在 bin 目录下生成可执行文件
```