---
title: VMware 安装 ubuntu 系统
date: 2023-05-13 20:29:09
tags:
    - 服务器
    - linux
    - ubuntu
categories: linux
cover: http://cdn.frankfurtlin.top/blog/covers/cover11.jpg
---

# VMware 安装 ubuntu 系统

## 下载所需软件

``` bash
# 安装 VMware Workstation Pro
https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html
# 安装 ubuntu iso
https://mirrors.ustc.edu.cn/
```

## VMware 安装 ubuntu
  
- 创建虚拟机
- 启动虚拟机

## 安装 VMware Tools

``` bash
sudo apt upgrade
sudo apt install open-vm-tools-desktop -y
sudo reboot
```

## 修改 apt 下载源

``` bash
# 备份配置文件
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
# 修改配置文件
# 阿里源
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
# 中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# 清华源
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# 修改只读文件，vim 命令模式输入
:w !sudo tee %
```

## 安装必要开发环境

``` bash
sudo apt install gcc
sudo apt install openjdk-17-jdk
sudo apt install python3
sudo apt install go
sudo apt install nodejs
sudo apt install npm
```