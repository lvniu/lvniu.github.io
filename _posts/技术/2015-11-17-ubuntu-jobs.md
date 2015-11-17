---
layout: post
title: "ubuntu工作的前后台切换命令"
description: ""
category: "技术" 
tags: "ubuntu jobs" 
---

### 1、&   
 
加在一个命令的最后，可以把这个命令放到后台执行,如                   


		gftp &                             



### 2、ctrl + z              

可以将一个正在前台执行的命令放到后台，并且处于暂停状态，不可执行                   

### 3、jobs                    

查看当前有多少在后台运行的命令                   



jobs -l选项可显示所有任务的PID，jobs的状态可以是running, stopped, Terminated,但是如果任务被终止了（kill），shell 从当前的shell环境已知的列表中删除任务的进程标识；也就是说，jobs命令显示的是当前shell环境中所起的后台正在运行或者被挂起的任务信息；           



### 4、fg               

将后台中的命令调至前台继续运行                     


如果后台中有多个命令，可以用fg %jobnumber将选中的命令调出，%jobnumber是通过jobs命令查到的后台正在执行的命令的序号(不是pid)                  
 

### 5、bg                  
 
将一个在后台暂停的命令，变成继续执行 （在后台执行）               



如果后台中有多个命令，可以用bg %jobnumber将选中的命令调出，%jobnumber是通过jobs命令查到的后台正在执行的命令的序号(不是pid)              
将任务转移到后台运行：                

先ctrl + z；再bg，这样进程就被移到后台运行，终端还能继续接受命令。                         

如果后台的任务号有2个，[1],[2]；如果当第一个后台任务顺利执行完毕，第二个后台任务还在执行中时，当前任务便会自动变成后台任务号码“[2]” 的后台任务。所以可以得出一点，即当前任务是会变动的。当用户输入“fg”、“bg”和“stop”等命令时，如果不加任何引号，则所变动的均是当前任务                 



### 6、nohup           

如果你正在运行一个进程，而且你觉得在退出帐户时该进程还不会结束，那么可以使用nohup命令。该命令可以在你退出帐户/关闭终端之后继续运行相应的进程。                 


### 7、screen              

虽然nohup很容易使用，但还是比较”简陋”的，对于简单的命令能够应付过来，对于复杂的需要人机交互的任务就麻烦了。                


其实我们可以使用一个更为强大的实用程序screen。流行的Linux发行版（例如Red Hat Enterprise Linux 4）通常会自带screen实用程序，如果没有的话，可以从GNU screen的官方网站下载。                     


简单来说，Screen是一个可以在多个进程之间多路复用一个物理终端的窗口管理器。Screen中有会话的概念，用户可以在一个screen会话 中创建多个screen窗口，在每一个screen窗口中就像操作一个真实的telnet/SSH连接窗口那样。在screen中创建一个新的窗口有这样 几种方式：          


- 直接在命令行键入screen命令         


# screen              


Screen将创建一个执行shell的全屏窗口。你可以执行任意shell程序，就像在ssh窗口中那样。在该窗口中键入exit退出该窗口，如果这是该screen会话的唯一窗口，该screen会话退出，否则screen自动切换到前一个窗口。               



- Screen命令后跟你要执行的程序                    


		# screen vi test.c              


Screen创建一个执行vi test.c的单窗口会话，退出vi将退出该窗口/会话。                   

以上两种方式都创建新的screen会话。我们还可以在一个已有screen会话中创建新的窗口。在当前screen窗口中键入C-a c ，即Ctrl键+a键，之后再按下c键，screen 在该会话内生成一个新的窗口并切换到该窗口。                         

关于screen的其他内容，[请查看](http://blog.csdn.net/wind19/article/details/4986458)                    

### 8、进程的终止          

后台进程的终止：                         

- 方法一：通过jobs命令查看job号（假设为num），然后执行kill %num                

- 方法二：通过ps命令查看job的进程号（PID，假设为pid），然后执行kill pid                      

前台进程的终止：                    


		ctrl+c                     


