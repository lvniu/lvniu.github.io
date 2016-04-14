---
layout: post
title: "sublime text 3配置"
description: ""
category: "技术" 
tags: "sublime" 
---

###1、安裝install packages     
在Preferences(设置)菜单中打开Package Control(插件管理器)      
打开菜单后找到install packages,回车执行，稍等一会看到左下角提示安装成功就好了     


###2、安装Ctags插件        
- 通过 Preference -> Package Control -> Install Package安装Ctags插件           
- 下载 Ctags.exe，[下载地址](http://nchc.dl.sourceforge.net/project/ctags/ctags/5.8/ctags58.zip), 通过 Preference -> Package Settings -> Ctags -> Settings Default 中的内容拷贝到 Setting User中，将 command": "" 中的 "" 填入Ctags.exe的路径位置                  
- 在工程根目录上点击右键，选择Ctags:Rebuild tags           
[其他博客](https://www.zybuluo.com/lanxinyuchs/note/33551)                       



### 3、sublime快捷键    
文件切换： ctrl+p              
替换 ： ctrl+shift+f               

函数查找 ctrl+p 然后输入：@                      
或者是 ctrl+r，选择指定函数            
跳到指定行 ctrl+p 然后输入：:行数                    

跳到某个类某个方法 ctrl+p 输入 类名@函数名                         

调出命令面板 ctrl+shift+p                             

生成.ctags ctrl + t + r（相当于Ctags:Rebuild tags）                              

跳转到声明： ctrl + t + t ，ctrl+> ，ctrl+shift+left_click                      
跳转返回： ctrl + t + b ，ctrl+< ，ctrl+shift+right_click                    

### 4、Sublime使用及FtpSync远程同步

[请查看博客](http://liuwanlin.info/sublimeshi-yong-ji-ftpsyncyuan-cheng-tong-bu/)    
使用SFTP更牛掰，直接通过ctrl+shift+p Install Package 来查找SFTP进行安装，完成后，再进行配置host、username和password

### 5、There are no packages available for installation问题解决办法
- 打开windows控制台，输入 ping sublime.wbond.net 然后看响应ping包的IP地址是多少，我这里是 50.116.33.29
- 然后打开系统的host文件：C:\Windows\system32\drivers\etc\，在最后添加一行：50.116.33.29 sublime.wbond.net，原理就不细讲了，这个就是域名和IP的一个映射关系。保存，关闭。
- 重启Sublime，然后ctrl+shift+P, 输入install，就会发现可以解析到插件了。   
[参考博客](http://blog.csdn.net/u013647382/article/details/46547291)
