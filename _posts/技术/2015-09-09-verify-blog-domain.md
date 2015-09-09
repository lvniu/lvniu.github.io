---
layout: post
title: "github pages 绑定新网申请的域名"
description: ""
category: "技术"
tags: "github jekyll" 
---

###1. 申请域名   
由于对于域名没有太多的了解，就随便在[新网](http://www.xinnet.com/)上申请了一个.com的域名。关于这个域名，我也是煞费苦心。申请之后无法使用，无法解析，而且注册人名不是我本人。给客服打电话，客服说域名需要过户，具体过程[请查看](http://www.xinnet.com/service/cjwt/domain/guohu/1184.html)。过户完成等了10多分钟才能使用。   


后来，才听同事说，[万网](http://wanwang.aliyun.com/domain/)很好用。然后，我对比了一下，发现新网做的不是一般的差，先不说域名服务如何，但从域名申请和管理的网站上看，新网就差万网一大截。我的心也一下凉了。然而，我又发现了另外一个功能，可以把新网的域名转到万网上，具体流程[请看](http://help.aliyun.com/knowledge_detail/6555809.html?spm=5176.789002828.3.3.lWZUX6)。但是这也需要时间，新网客服说需要二个月时间。哎，申请个域名好憔悴。如果你还没申请域名，而且打算申请，强烈建议在万网申请。   



下面进入正题。    
###2. github工程中创建CNAME文件   
- 在名字为username.github.io的仓库根目录中添加CNAME文件。CNAME的内容为博客要添加的新域名。   
![alt_text](/public/img/github/lvniu.png)   
![alt_text](/public/img/github/CNAME.png)   
- 查看CNAME设置是否正确,如果提示“Your site is published at..”，说明配置成功。   
![alt_text](/public/img/github/Settings1.png)   
![alt_text](/public/img/github/Settings2.png)     



###2. 在新网上配置DNS     

- 使用申请的域名登陆[新网域名自助管理平台](http://dcp.xinnet.com/Modules/agent/domain/domain_manage.jsp)。   
![alt_text](/public/img/github/xinwang.jpg)   
- 进入My DNS功能     
![alt_text](/public/img/github/mydns.png)    
- 追加CNAME记录，别名处添加www就ok了，别名主机填写github上自己仓库的名称：username.github.io。      
![alt_text](/public/img/github/cnamedns.png)   


###3. 查看域名映射结果   
直接在浏览器输入配置好的域名。例如：www.fieelingtime.com。如果能够正常显示username.github.io中的index.html页面，则说明成功了。   


如果显示404，则说明DNS还没有解析成功，请等待一段时间。
