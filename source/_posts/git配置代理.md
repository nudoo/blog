---
title: git配置代理
date: 2024-10-02 14:39:44
author: moea
summary: 使用V2ray对Git/npm进行代理加速
img: https://gd-hbimg.huaban.com/1a6ad216a3e7e3ab52fe976492a92490bf60e507fe5f0-WmQZtv_fw658webp
categories: 开发工具
tags:
  - github
  - git
  - npm
---

## git

  ```bash
$ # socks5协议，v2ray默认监听10808端口
$ git config –global http.proxy socks5://127.0.0.1:10808
$ git config –global https.proxy socks5://127.0.0.1:10808
$ # http协议，v2ray默认监听10809端口
$ git config –global http.proxy http://127.0.0.1:10809
$ git config –global https.proxy https://127.0.0.1:10809
$ # 查看设置
$ git config -l
  ```

## github
如果单独给github配置代理，设置如下：
```bash
# 走 socks5 代理
git config --global http.https://github.com.proxy "socks5://127.0.0.1:1080"
# 走 http 代理
git config --global http.https://github.com.proxy "http://127.0.0.1:10809"
# 取消设置
git config --global --unset http.https://github.com.proxy
```

## npm
```bash
npm config set proxy http://127.0.0.1:10809
npm config set https-proxy http://127.0.0.1:10809
```


参考链接：
[各常用包管理器配置科学上网代理](https://www.codeover.cn/proxy-settings/)
[使用V2ray对Git进行加速](https://igghelper.com/helper/?p=152)
