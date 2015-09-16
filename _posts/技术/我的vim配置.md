---
published: true
---




vim是一款强大的编辑工具，但是需要自己添加相应的plugin。下面我介绍一下我的vim配置。
###1. vim中实现c++头文件和源文件切换
- 首先，下载文件a.vim，[下载地址](http://www.vim.org/scripts/script.php?script_id=31)；
- 然后，把下载好的a.vim放置到目录~/.vim/plugin下。


按照上面的步骤，配置好以后，我们就可以直接使用了。关于a.vim的几个命令：


| 命令   | 效果           |
| ------- |:---------------:|
| :A  | 在新窗口中实现c/h文件相互切换 |
| :AS  | 横向分割窗口，打开c/h文件      |
| :AV | 纵向分割窗口，打开c/h文件      |
| :AT | 新建一个标签页并打开c/h文件      |


当然，也可以在.vimrc配置文件中添加一行：nnoremap <silent> <F12> :A<CR>。以后编辑的时候，就可以直接使用<F12>直接实现c/h文件的快速切换。
###2. vim配置ctags
- 首先，下载ctags源文件，[下载地址](http://ctags.sourceforge.net/)；
- 然后源码安装，我下载的是ctags-5.8.tar.gz，所以，我的安装buzh步骤为：
		$ tar -xzvf ctags-5.6.tar.gz
		$ cd ctags-5.6
		$ make
		# make install   // 需要root权限
现在就可以在你的工程目录下运行命令：
		`ctags -R`
例如，我的工程目录是：/home/username/leveldb
		$ cd /home/username/leveldb
      $ ctags -R
此时，会在目录/home/username/leveldb下生成一个tags文件。配置到这儿，还差一步就完成了整个ctags的配置。下面这个步骤有两种方法，任意选择一种，都可以完成ctags的配置：
1）. 打开/home/username/leveldb下面的任意一个文件，例如test.c：
		$ vim /home/username/leveldb/test.c
在vim中，执行命令：
      :set tags=/home/username/leveldb/tags
2）. 在.vimrc配置文件中配置：
		set tags=/home/username/leveldb/tags
至此，ctags已经配置完成，你现在可以在工程中的不同文件中跳转了，例如使用Ctrl + ]跳转到变量或函数的定义位置，使用Ctrl + T从变量或函数的定义处返回。






