---
layout: post
title: "ubuntu中crontab的基本用法"
description: ""
category: "技术" 
tags: "ubuntu crontab" 
---

### 1、crontab入门命令      
cron是linux中的守护进程，用来定期执行一些任务。基本的命令包括以下几个：     


- crontab  -e 　编辑该用户的crontab，当指定crontab  不存在时新建。     
- crontab  -l 　列出该用户的crontab。       
- crontab  -r 　删除该用户的crontab。              
- crontab  -u <用户名称> 　指定要设定crontab的用户名称。       
- crontab –v 显示上一次编辑的时间（只在某些操作系统上可用）          


作为一个新用户，首先需要的操作是，执行命令：        


		$ crontab -e     


- 在linux系统中，不同的用户打开的crontab文件是不同的。当你打开你用户所属的crontab,第一次用这个命令，会让你选择文本编辑器。我的电脑上显示4中编辑器，如下，我选择是vim.basic。      


		  1. /bin/ed         
		  2. /bin/nano        <---- easiest           
			3. /usr/bin/vim.basic              
		  4. /usr/bin/vim.tiny                


如果你编辑时，选择错了编辑器，或者是想更改，可以使用下面的命令进行重新选择：           


		$ select-editor    


打开后的crontab内容如下：                   


		# m h  dom mon dow   command      
		*/2 * * * * date >> ~/time.log    


- 第二行是我为了测试写的一个定期任务，它的意思是，每隔两分钟就执行 date >> ~/time.log 命令（记录当前时间到time.log文件）。你可以把它加入你的crontab中，然后保存退出。                


保存了crontab之后，我们还需要重启cron来应用这个计划任务。使用以下命令：       


		sudo service cron restart      


### 2、crontab命令的基本含义         
crontab中的每一行代表一个定期执行的任务，分为6个部分。前5个部分表示何时执行命令，最后一个部分表示执行的命令。每个部分以空格分隔，除了最后一个部分（命令）可以在内部使用空格之外，其他部分都不能使用空格。前5个部分分别代表：分钟，小时，天，月，星期，每个部分的取值范围如下：                    


- 分钟          0 - 59                  
- 小时          0 - 23          
- 天            1 - 31        
- 月            1 - 12          
- 星期          0 - 6       0表示星期天          

 

除了这些固定值外，还可以配合星号（*），逗号（,），和斜线（/）来表示一些其他的含义：               

 

- 星号          表示任意值，比如在小时部分填写 * 代表任意小时（每小时）                    
- 逗号          可以允许在一个部分中填写多个值，比如在分钟部分填写 1,3 表示一分钟或三分钟               
- 斜线          一般配合 * 使用，代表每隔多长时间，比如在小时部分填写 */2 代表每隔两分钟。所以 */1 和 * 没有区别,*/2 可以看成是能被2整除的任意值。                 

 

以下是一些例子（省略了命令部分）：

 

- \* * * * *                   # 每隔一分钟执行一次任务                 
- 0 * * * *                    # 每小时的0点执行一次任务，比如6:00，10:00                
- 6,10 * 2 * *                 # 每个月2号，每小时的6分和10分执行一次任务                       
- \*/3,*/5 * * * *             # 每隔3分钟或5分钟执行一次任务，比如10:03，10:05，10:06                 



### 3、开启日志功能            
1) 修改配置文件：/etc/rsyslog.d/50-default.conf                 



		vim /etc/rsyslog.d/50-default.conf    


在配置文件中，把              


		#cron.*       /var/log/cron.log                


前面的注释#号去掉就OK了。       


2) 重启rsyslog服务             


		service rsyslog restart           


3) 再次查看cron日志              


		ls /var/log/cron.log           


备注：这里就有了 crontab  日志。    



