---
layout: post
title: "nodejs学习"
description: ""
category: "技术"
tags: "nodejs" 
---


###1. centos安装nodejs   

- nodejs安装方式很多，花费了很长时间在源码安装上，因为源码安装需要依赖其他的配置，包括gcc等。所以安装起来比较麻烦。后来发现，使用nvm安装相当方便，且能安装到自己的用户下（这一点是我比较在意的）。  

- 下面来说一下安装过程，这些安装方法完全cp自[微魔部落](https://www.vmvps.com/4-ways-to-install-node-js-on-centos-7-servers.html)

####1.1 源码安装

- 下载源码（官网查看最新版本链接）

		wget http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz  
- 解压源码

		tar xzvf node-v* && cd node-v*
- 安装必要的编译软件

		sudo yum install gcc gcc-c++
- 编译

		./configure
		make
- 编译&安装

		sudo make install
- 查看版本（测试安装是否成功）

		node --version

####1.2 使用已编译版本安装

- 下载已编译版本

	[获取最新版本的链接](https://nodejs.org/download/)

		cd ~
		wget http://nodejs.org/dist/v0.10.30/node-v0.10.30-linux-x64.tar.gz
- 解压源码

		sudo tar --strip-components 1 -xzvf node-v* -C /usr/local
- 配置环境变量

		export PATH="$PATH:/usr/local/node-v*/bin"

- 查看版本（测试安装是否成功）

		node --version

####1.3 使用EPEL安装

- 下载EPEL

		sudo rpm -i http://download.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm 
- 安装

		sudo yum install nodejs
- 查看版本（测试安装是否成功）

		node --version
- （可选）安装npm管理包

		sudo yum install npm

####1.4 通过NVM（Node version manager）安装(也是最推荐使用的方法）

- 下载并安装NVM脚本

		curl https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh | bash
		source ~/.bash_profile
- 列出所需要的版本

		nvm list-remote
返回结果如下

		. . .
		v0.10.29
		v0.10.30
		 v0.11.0
		 v0.11.1
		 v0.11.2
		 v0.11.3
		 v0.11.4
		 v0.11.5
		 v0.11.6
		 v0.11.7
		 v0.11.8
		 v0.11.9
		v0.11.10
		v0.11.11
		v0.11.12
		v0.11.13
- 安装相应的版本

		nvm install v0.10.30
- 查看已安装的版本

		nvm list
显示结果

		->  v0.10.30
		      system
- 切换版本

		nvm use v0.10.30
- 设置默认版本

		nvm alias default v0.10.30

###2. npm常用命令

npm是一个node包管理和分发工具，已经成为了非官方的发布node模块（包）的标准。有了npm，可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。

- npm install moduleNames：安装Node模块   
安装完毕后会产生一个node_modules目录，其目录下就是安装的各个node模块。   
node的安装分为全局模式和本地模式。   
一般情况下会以本地模式运行，包会被安装到和你的应用程序代码的本地node_modules目录下。   
在全局模式下，Node包会被安装到Node的安装目录下的node_modules下。      
全局安装命令为$npm install -g moduleName。   
获知使用$npm set global=true来设定安装模式，$npm get global可以查看当前使用的安装模式。   
示例：   

		npm install express 
默认会安装express的最新版本，也可以通过在后面加版本号的方式安装指定版本，如npm install express@3.0.6   

		npm install <name> -g    
将包安装到全局环境中   
但是代码中，直接通过require()的方式是没有办法调用全局安装的包的。全局的安装是供命令行使用的，就好像全局安装了vmarket后，就可以在命令行中直接运行vm命令   

		npm install <name> --save 
安装的同时，将信息写入package.json中项目路径中如果有package.json文件时，直接使用npm install方法就可以根据dependencies配置安装所有的依赖包，这样代码提交到github时，就不用提交node_modules这个文件夹了。

- npm view moduleNames：查看node模块的package.json文件夹   
注意事项：如果想要查看package.json文件夹下某个标签的内容，可以使用$npm view moduleName labelName

- npm list：查看当前目录下已安装的node包   
注意事项：Node模块搜索是从代码执行的当前目录开始的，搜索结果取决于当前使用的目录中的node_modules下的内容。$ npm list parseable=true可以目录的形式来展现当前安装的所有node包

- npm help：查看帮助命令

- npm view moudleName dependencies：查看包的依赖关系

- npm view moduleName repository.url：查看包的源文件地址

- npm view moduleName engines：查看包所依赖的Node的版本

- npm help folders：查看npm使用的所有文件夹

- npm rebuild moduleName：用于更改包内容后进行重建

- npm outdated：检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新

- npm update moduleName：更新node模块

- npm uninstall moudleName：卸载node模块

- 一个npm包是包含了package.json的文件夹，package.json描述了这个文件夹的结构。访问npm的json文件夹的方法如下：

		$ npm help json 
此命令会以默认的方式打开一个网页，如果更改了默认打开程序则可能不会以网页的形式打开。

- 发布一个npm包的时候，需要检验某个包名是否已存在

		$ npm search packageName

- npm init：会引导你创建一个package.json文件，包括名称、版本、作者这些信息等

- npm root：查看当前包的安装路径

		npm root -g：查看全局的包的安装路径

- npm -v：查看npm安装的版本

- 更多命令请参看npm[官方文档](https://www.npmjs.org/doc/)

###3. 安装apidoc    
局部安装方式

		npm install apidoc
全局安装方式(如果局部安装失败，请使用全局安装方式)

		npm install apidoc -g
如果报错：NPM problem: npm ERR! extraneous   
请使用命令：

		npm prune

