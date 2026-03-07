---
title: 在wsl中使用docker
top: false
cover: false
toc: true
mathjax: true
author: moea
img: https://cdn.jsdelivr.net/gh/nudoo/nudoo.github.io@master/gallery/imgs/11.jpg
date: 2026-03-07 21:30:45
password:
summary: 在wsl中安装docker及网络配置
tags:
  - docker
categories: 开发工具
---

# 在wsl中安装配置docker

一键脚本：
```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror AzureChinaCloud
```

## 一、安装步骤
```bash
# 更新并安装基础依赖
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release

# 添加 Docker 官方 GPG 密钥和仓库
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 安装
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## 二、配置 WSL 内部代理
因为 WSL 与宿主机是不同的网络空间，需要让 WSL 里的 Docker 守护进程能通过宿主机的代理拉取镜像。

### 第一步：获取宿主机 IP
在 WSL 中输入 cat /etc/resolv.conf 查看 nameserver 后面的 IP，通常这是宿主机的虚拟 IP。


>**如果你使用的是 Win11 的最新版 WSL，建议开启 镜像网络模式 (Mirrored)。**
>在 Windows 用户目录下（C:\Users\你的用户名\）创建或编辑 .wslconfig 文件。
>添加以下配置：
>```Ini, TOML
>[wsl2]
>networkingMode=mirrored
>```
>好处： 开启后，WSL 和 Windows 共享 IP 栈。在 WSL 里直接用 127.0.0.1:端口 就能访问宿主机的代理软件，无需再查找复杂的虚拟 IP。


### 第二步：配置 Docker 代理服务
创建配置目录：

```Bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```
在文件中写入（假设宿主机代理端口是 10809）：

```Ini, TOML
[Service]
Environment="HTTP_PROXY=http://宿主机IP:10809"
Environment="HTTPS_PROXY=http://宿主机IP:10809"
Environment="NO_PROXY=localhost,127.0.0.1"
```

### 第三步：重启服务

```Bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```