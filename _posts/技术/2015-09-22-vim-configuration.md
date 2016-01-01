---
layout: post
title: "我的vim配置"
description: ""
category: "技术"
tags: "vim"
---




vim是一款强大的编辑工具，但是需要自己添加相应的plugin。下面我介绍一下我的vim配置。
###1. vim中实现c++头文件和源文件切换
- 首先，下载文件a.vim，[下载地址](http://www.vim.org/scripts/script.php?script_id=31)；
- 然后，把下载好的a.vim放置到目录~/.vim/plugin下。




按照上面的步骤，配置好以后，我们就可以直接使用了。关于a.vim的几个命令：


|| *命令*   || *效果*           ||       
> | ------- |:---------------:|
|| :A  || 在新窗口中实现c/h文件相互切换 ||   
|| :AS  || 横向分割窗口，打开c/h文件      ||
|| :AV || 纵向分割窗口，打开c/h文件      ||   
|| :AT || 新建一个标签页并打开c/h文件      ||


当然，也可以在.vimrc配置文件中添加一行：nnoremap <silent> <F12> :A<CR>。以后编辑的时候，就可以直接使用<F12>直接实现c/h文件的快速切换。
###2. vim配置ctags
- 首先，下载ctags源文件，[下载地址](http://ctags.sourceforge.net/)；
- 然后源码安装，我下载的是ctags-5.8.tar.gz，所以，我的安装buzh步骤为：
		$ tar -xzvf ctags-5.8.tar.gz
		$ cd ctags-5.8
		$ make
		# make install   
现在就可以在你的工程目录下运行命令：
		`ctags -R`     


如果出现工程包含js文件，会出现如下情况：        
		ctags: Warning: ignoring null tag in ………….js     


这种错误，据说是因为“js文件内有特殊结构，不在CTags默认定义列表中”，有两种方法：       
- 将项目中的js文件全部移出去，等生成那两个文件之后再移回来。       
- ctags可以指定生成.tags文件时，只过滤哪种语言的文件，下面的命令是只过滤php文件
cmd切换到项目文件目录，执行：      


		ctags --languages=php  -R      



例如，我的工程目录是：/home/username/leveldb   
		  $ cd /home/username/leveldb
      	$ ctags -R



此时，会在目录/home/username/leveldb下生成一个tags文件。配置到这儿，还差一步就完成了整个ctags的配置。下面这个步骤有两种方法，任意选择一种，都可以完成ctags的配置：


- 1）打开/home/username/leveldb下面的任意一个文件，例如test.c：    
		$ vim /home/username/leveldb/test.c   
在vim中，执行命令：
		:set tags=/home/username/leveldb/tags


- 2）在.vimrc配置文件中配置：
		set tags=/home/username/leveldb/tags
至此，ctags已经配置完成，你现在可以在工程中的不同文件中跳转了，例如使用Ctrl + ]跳转到变量或函数的定义位置，使用Ctrl + T从变量或函数的定义处返回。   
###3. vim中配置自动补全功能   
首先确定你的ctags已安装。然后在~/.vimrc配置文件中添加如下两行命令：
			filetype plugin indent on   
			set completeopt=longest,menu   
此时就可以利用快捷方式进行自动补全了，各类补全快捷方式如下：   



| 命令   |补全方式           |
| ------- |:---------------:|
| Ctrl+X Ctrl+L  | 整行补全 |
| Ctrl+X Ctrl+N | 根据当前文件里关键字补全      |
| Ctrl+X Ctrl+K | 根据字典补全      |
| Ctrl+X Ctrl+T | 根据同义词字典补全      |
| Ctrl+X Ctrl+I | 根据头文件内关键字补全 |
| Ctrl+X Ctrl+] | 根据标签补全      |
| Ctrl+X Ctrl+F | 补全文件名     |
| Ctrl+X Ctrl+D | 补全宏定义      |
| Ctrl+X Ctrl+V | 补全vim命令      |
| Ctrl+X Ctrl+U | 用户自定义补全方式    |
| Ctrl+X Ctrl+S | 拼写建议     |


其他快捷键：   


| 命令   |补全方式           |
| ------- |:---------------:|
| Ctrl+P  | 向前切换成员 |
| Ctrl+N | 向后切换成员      |
| Ctrl+E | 表示退出下拉窗口, 并退回到原来录入的文字      |
| Ctrl+Y | 表示退出下拉窗口, 并接受当前选项      |




### 4、代码折叠   
- 折叠配置   
在.vimrc文件中添加如下命令：   
		set fdm=syntax        
		set foldnestmax=2     如果需要设置折叠深度，可以选择添加此选项     



- 折叠方式    
有6类方法来设定折叠：   
manual           手工定义折叠    
indent           更多的缩进表示更高级别的折叠    
expr             用表达式来定义折叠     
syntax           用语法高亮来定义折叠    
diff             对没有更改的文本进行折叠    
marker           对文中的标志折叠    


- 折叠命令   
zc     折叠    
zC     对所在范围内所有嵌套的折叠点进行折叠      
zo     展开折叠      
zO     对所在范围内所有嵌套的折叠点展开      
zi     折叠/打开所有折叠行      
[z     到当前打开的折叠的开始处。      
]z     到当前打开的折叠的末尾处。        
zj     向下移动。到达下一个折叠的开始处。关闭的折叠也被计入。       
zk     向上移动到前一折叠的结束处。关闭的折叠也被计入。     


### 5、php安装vld扩展    
VLD(Vulcan Logic Dumper)是一个在Zend引擎中，以挂钩的方式实现的用于输出PHP脚本生成的中间代码（执行单元）的扩展。 它可以在一定程序上查看Zend引擎内部的一些实现原理，是我们学习PHP源码的必备良器。    
具体安装方式：[请查看](http://www.jinglingshu.org/?p=8988)        



### 6、vim的基本命令      
[查看地址](http://www.cnblogs.com/softwaretesting/archive/2011/07/12/2104435.html)         

