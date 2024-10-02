---
title: 基于Hexo与GitHub搭建个人博客
date: 2024-10-02 10:36:41
author: moea
img: https://api.paugram.com/wallpaper/
top: true
hide: false
cover: true
coverImg: /images/1.jpg
toc: false
mathjax: false
summary: 基于Hexo与GitHub搭建个人博客
categories: 前端
tags:
  - github
  - hexo
---

## 0.前期准备
开始之前，请确保已安装以下工具：git、npm
在github创建一个仓库：username.github.io
在本地建一个同名的目录


## 1.安装hexo
  ```bash
npm install -g hexo-cli
  ```
  
### 1.1 初始化
执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件：

  ```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
  ```
  
### 1.2 更改配置
修改_config.yml:(注意配置的键值之间要有空格)

#### 网站
|设置	|描述  |
|:------|:-----|
|title	|网站标题
|subtitle	|网站副标题
|description	|网站描述
|keywords	|网站的关键词。 支持多个关键词。
|author	|您的名字
|language	|网站使用的语言。 使用 2 个字母的 ISO-639-1 代码，或 它的变体。 默认为 en。
|timezone	|网站时区。 Hexo 默认使用您电脑的时区。 请参考 时区列表 进行设置，如 America/New_York, Japan, 和 UTC 。 一般的，对于中国大陆地区可以使用

#### 网址
|设置	|描述	|默认值
|:-:|:-:|:-:|
|url	|网址, 必须以 http:// 或 https:// 开头	|
|root	|网站根目录	url's pathname|
|permalink	|文章的 永久链接 格式	:year/:month/:day/:title/|
|permalink_defaults	|永久链接中各部分的默认值	|
|pretty_urls	|改写 permalink 的值来美化 URL	|
|pretty_urls.trailing_index	|是否在永久链接中保留尾部的 index.html，设置为 false 时去除	|true
|pretty_urls.trailing_html	|是否在永久链接中保留尾部的 .html, 设置为 false 时去除 (对尾部的 index.html无效)	|true

>**网站存放在子目录**
>如果您的网站存放在子目录中，例如 [http://example.com/blog] ,则请将您的 url 设为 [http://example.com/blog] ,并把 root 设为 /blog/。


### 1.3 安装主题
这里选择的是keep主题。使用git clone：
 ```bash
$ cd <folder>
$ git clone https://github.com/XPoet/hexo-theme-keep themes/keep
  ```
  
或使用npm安装：
 ```bash
$ cd <folder>
$ npm install hexo-theme-keep
  ```
  
Keep 主题安装完成后，在 Hexo 配置文件 _config.yml 中将 theme 设置为 keep。
更新主题：
通过 Git 更新到最新的 master 分支：
 ```bash
$ cd <folder>/themes/keep
$ git pull
  ```
  
或通过 NPM 安装最新版本
 ```bash
$ cd <folder>
$ npm install hexo-theme-keep@latest
  ```
* 两种方式不要混用


### 1.4 写文章
在<folder>/source/_posts下创建你的第一个博客吧
```bash
$ hexo new post "title"
```

### 1.5 测试
 ```bash
hexo server  //hexo s
  ```
测试服务启动后，可以在浏览器输入localhost:4000进行访问。
（本人的网站存放在子目录中，输入localhost:4000/blog/访问）

## 远程部署
### 1.6 安装hexo-deployer-git自动部署发布工具 
```bash
$ npm install hexo-deployer-git --save
```
  
配置_config.yml:
```yaml
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
```
  

为了将博客放在子目录(即nudoo.github.io/blog)下，需要新建一个github仓库(blog)，注意需要是公开的，
在 GitHub 仓库的设置中，导航至 Settings > Pages > Source 。 将 source 更改为 GitHub Actions，然后保存。
编辑 _config.yml，将 url: 更改为 nudoo.github.io/blog
Commit 并 push 到默认分支上。（hexo clean & hexo g & hexo d)
访问nudoo.github.io/blog查看



### 1.7 发布
清除之前生成的东西
```bash
hexo clean
  ```
生成静态文章
```bash
hexo generate // hexo g
 ```
 部署文章
 ```bash
 hexo deploy // hexo d
 ```
也可以写在一起
 ```bash
$ hexo clean && hexo g && hexo d
 ```
 
附：
## 备份源文件
 hexo deploy只将生成的静态网页文件(public目录)上传到了仓库中，如果想要多个终端同步写作，可以把blog源文件上传到github。
 在github仓库新建一个分支hexo，然后git clone到本地，把.git文件夹拿出来，放在博客根目录下。
 然后git checkout hexo切换到hexo分支，然后git add .，然后git commit -m "xxx"，最后git push origin hexo提交就行了。
 * 也可以新建一个仓库存放源文件


## 宠物

1、安装live2d插件
```bash
npm install --save hexo-helper-live2d
```
3、安装模型
```bash
npm install live2d-widget-model-shizuku
```
4、在配置文件中添加即可
```yaml
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: live2d-widget-model-shizuku
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
  react:
    opacity: 0.7
```