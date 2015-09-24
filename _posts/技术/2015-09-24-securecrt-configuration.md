---
layout: post
title: "secureCRT自动断开的解决方法"
description: ""
category: "技术" 
tags: "secureCRT" 
---



使用securecrt进行远程登录时，如果长时间不操作，将会自动断开连接。如果是间断式的使用securecrt，就会造成不断重连麻烦。针对这个问题，解决办法如下：     



Options->Session Options->Terminal->Anti-idle->勾选Send protocol NO-OP   
(中文版：选项->会话选项->终端->反空闲->发送协议NO-OP)   
后面的设置时间默认的是60秒，只要小于自动断开连接的时限就可以了。如下图所示：


![alt text](/public/img/blog/securecrt-config.jpg  "Title")

