---
title: 搭建 Git 服务器
date: 2022-11-18 21:55:40
tags:
    - Git
    - 服务器
categories: 服务器
cover: /assets/img/cover/dark.webp
---

# 搭建 Git 服务器

## 1. 本地生成登录用户的密钥

``` bash
# 生成密钥
ssh-keygen -t rsa -C "youremail@example.com"
# 查看密钥
cd ~/.ssh && vim id_rsa.pub
# 复制上述密钥留作后面粘贴到服务器的 /home/git/.ssh/authorized_keys
```

## 2. 服务器安装 Git（以 centos 为例）

``` bash
# 更新 yum
yum update
# 安装 git
yum install git
# 查看安装好的 git
git --version
```

## 3. 创建一个 Git 用户，用来运行 Git 服务

``` bash
adduser git
```

## 4. 导入用户的公钥

``` bash
# 切换到用户目录
cd /home/git
# 新建.ssh目录
mkdir .ssh && cd .ssh
# 新建用户认证文件
touch authorized_keys && vim authorized_keys
# 粘贴上述的本地用户公钥到该文件中
```

## 5. 初始化 Git 项目

``` bash
# 假定是 /srv/sample.git
cd /srv
git init --bare sample.git
```

## 6. 将该项目 owner 改为 git 用户

``` bash
chown -R git:git sample.git
```

## 7. 禁用 shell 登录

``` bash
# 出于安全考虑，第三步创建的 git 用户不允许登录 shell，可以正常通过 ssh 使用 git
vim /etc/passwd
#修改 git:x:1001:1001:,,,:/home/git:/bin/bash 为
# git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

## 8. 克隆远程仓库

``` bash
git clone git@server_ip:/srv/sample.git
```

## 9. 管理多人密钥

[Gitosis](https://github.com/res0nat0r/gitosis)

## 10. 管理权限

[Gitolite](https://github.com/sitaramc/gitolite)

转载自廖雪峰博客[搭建Git服务器](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)

