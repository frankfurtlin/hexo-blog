---
title: 内网穿透搭建 Minecraft 服务器
date: 2023-01-31 23:37:22
tags:
    - 服务器
    - Minecraft
categories: 服务器
cover: /assets/img/cover/8.webp
---

# 内网穿透搭建 Minecraft 服务器

## 1. 环境准备

- 开源的反向代理解决方案 [Frp](https://gofrp.org/docs/)
- 拥有公网域名的服务器一台[本教程使用CentOS]
- 本地 Windows 机器一台

## 2. 公网服务器设置

- 下载 frp 到公网服务器
https://github.com/fatedier/frp/releases
- 解压进入 frp 目录
- 修改服务器配置文件 frps.ini
``` bash
[common]
# 客户端与服务器连接的端口
# 记得在服务器后台放开对应的端口
bind_port = 70
# dashboard监控
# 通过 server_ip:71 可访问后台 dashboard
dashboard_port = 71
dashboard_user = username
dashboard_pwd = password
# 权限认证
authentication_method = token
token = server_token
```
- 使用 systemd 控制 frp 服务器的启动、停止、后台运行和开机启动
``` bash
# 下载安装 systemd
yum install systemd

# 创建并编辑 frps.service 文件
vim /etc/systemd/system/frps.service

# 写入以下内容
    [Unit]
    # 服务名称，可自定义
    Description = frp server
    After = network.target syslog.target
    Wants = network.target

    [Service]
    Type = simple
    # 启动frps的命令，需修改为您的frps的安装路径
    ExecStart = /path/to/frps -c /path/to/frps.ini

    [Install]
    WantedBy = multi-user.target

# 启动 frp
systemctl start frps

# 停止 frp
systemctl stop frps

# 重启 frp
systemctl restart frps

# 查看 frp 状态
systemctl status frps

# 配置 frp 开机自启
systemctl enable frps
```

## 3. 客户端设置

- 下载 frp 到本地 Windows
- 修改 frpc.ini 文件
``` bash
[common]
# server ip
server_addr = 1.1.1.1
# 服务器与客户端连接的端口
server_port = 7000
# 写在后面会连接失败
authentication_method = token
token = server_token

# 服务名称
[minecraft]
type = tcp
local_ip = 127.0.0.1
# 本地 Minecraft 开放的端口
local_port = 25565
# 远程服务器提供服务的端口
# 得在远程服务器开放此端口
remote_port = 25565
```
- 编写启动脚本 start.bat
``` bash
frpc.exe -c frpc.ini
pause
```

## 4. 启动 Minecraft 服务端

## 5. 启动游戏
通过 server_ip:25565 加入服务器