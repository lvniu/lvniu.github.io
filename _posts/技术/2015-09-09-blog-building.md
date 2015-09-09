---
layout: post
title: "ubuntu 14.04使用github pages和jekyll搭建静态博客"
description: ""
category: "技术"
tags: "github jekyll" 
---


###1. 环境配置   

####1.1 安装ruby
- `$sudo apt-get install ruby1.9.1-full`  
安装完成后，在终端输入`ruby -v`,查看是否安装成功。    

####1.2 安装nodejs    
安装ruby时，会同时安装上gem。然而，使用命令`gem -v`,却提示一下内容   
- `var/lib/gems/1.9.1/gems/execjs-2.5.2/lib/execjs/runtimes.rb:48:in 'autodetect': Could not find a JavaScript runtime. See https://github.com/rails/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)` 
这是因为，ruby的gem管理需要nodejs的支持，所以需要安装nodejs。   
- `$sudo apt-get install nodejs`   

####1.3 安装jekyll   
- `$sudo gem install jekyll`    
如果报错，请安装ruby1.9.1的扩展组件的头文件。   
- `$sudo apt-get install ruby1.9.1-dev`    
安装完成后，就可以在终端使用jekyll命令创建博客了。    
- `$jekyll new myblog`   

####1.4 git安装   
- `$sudo apt-get install git`    
在终端输入`git -version`，出现git版本信息，说明安装成功。   

###2. github上创建repository   
在github上创建新的仓库，仓库名称为：*username.github.io*   
具体操作![请查看](https://pages.github.com/)   

