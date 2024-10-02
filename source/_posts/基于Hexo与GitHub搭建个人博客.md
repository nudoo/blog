## 0.前期准备
开始之前，请确保已安装以下工具：git、npm
在github创建一个仓库：username.github.io
在本地建一个同名的目录


## 1.安装hexo
  ```sh
npm install -g hexo-cli
  ```
  
1.1 初始化
执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件：

  ```sh
$ hexo init <folder>
$ cd <folder>
$ npm install
  ```
  
1.2 更改配置
修改_config.yml:(注意配置的键值之间要有空格)

# 网站

title: 存在于梦境的真实之地 //网站标题
subtitle: 网站副标题
description: 网站描述
author: moea //你的名字
language: zh-Hans //语言 中文
timezone: Asia/Shanghai //网站时区 
theme: next //主题名称
  

# 网址
设置	描述	默认值
url	网址, 必须以 http:// 或 https:// 开头	
root	网站根目录	url's pathname
permalink	文章的 永久链接 格式	:year/:month/:day/:title/
permalink_defaults	永久链接中各部分的默认值	
pretty_urls	改写 permalink 的值来美化 URL	
pretty_urls.trailing_index	是否在永久链接中保留尾部的 index.html，设置为 false 时去除	true
pretty_urls.trailing_html	是否在永久链接中保留尾部的 .html, 设置为 false 时去除 (对尾部的 index.html无效)	true

>网站存放在子目录
>如果您的网站存放在子目录中，例如 http://example.com/blog，则请将您的 url 设为 http://example.com/blog 并把 root 设为 /blog/。


1.3 安装主题
这里选择的是keep主题。使用git clone：
 ```sh
$ cd <folder>
$ git clone https://github.com/XPoet/hexo-theme-keep themes/keep
  ```
  
或使用npm安装：
 ```sh
$ cd <folder>
$ npm install hexo-theme-keep
  ```
  
Keep 主题安装完成后，在 Hexo 配置文件 _config.yml 中将 theme 设置为 keep。
更新主题：
通过 Git 更新到最新的 master 分支：
 ```sh
$ cd <folder>/themes/keep
$ git pull
  ```
  
或通过 NPM 安装最新版本
 ```sh
$ cd <folder>
$ npm install hexo-theme-keep@latest
  ```
* 两种方式不要混用


1.4 写文章
在<folder>/source/_posts下创建你的第一个博客吧

1.5 测试
 ```sh
hexo server  //hexo s
  ```
测试服务启动后，可以在浏览器输入localhost:4000进行访问。
（本人的网站存放在子目录中，输入localhost:4000/blog/访问）

## 远程部署
1.6 安装hexo-deployer-git自动部署发布工具 
```sh
$ npm install hexo-deployer-git --save
  ```
  
配置_config.yml:
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
  
  
-----------
为了将博客放在子目录(即nudoo.github.io/blog)下，需要新建一个github仓库(blog)，注意需要是公开的，
在 GitHub 仓库的设置中，导航至 Settings > Pages > Source 。 将 source 更改为 GitHub Actions，然后保存。
编辑 _config.yml，将 url: 更改为 nudoo.github.io/blog
Commit 并 push 到默认分支上。（hexo clean & hexo g & hexo d)
访问nudoo.github.io/blog查看

-----------

1.7 发布
清除之前生成的东西
```javascript
hexo clean
  ```
生成静态文章
```javascript
hexo generate // hexo g
 ```
 部署文章
 ```javascript
 hexo deploy // hexo d
 ```
也可以写在一起
 ```javascript
$ hexo clean && hexo g && hexo d
 ```