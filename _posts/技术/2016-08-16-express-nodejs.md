---
layout: post
title: "express学习"
description: ""
category: "技术"
tags: "nodejs express" 
---


###1. 建立工程   

 - 进入工程目录

			mkdir workplace
			cd workplace

 - 全局安装express，express作为命令被安装到了系统中.
 
			npm install -g express

 - 查看express版本

			express -V

 - **注意：**在express4.x版本中已经不含有express命令了。需要安装 express-generator

			npm install express-generator -g   
 - 创建项目

			$ express -e nodejs-demo
			create : nodejs-demo （项目名）
			create : nodejs-demo/package.json （项目包的信息）
			create : nodejs-demo/app.js (主程序)
			create : nodejs-demo/public (公开目录)
			create : nodejs-demo/public/images
			create : nodejs-demo/public/javascripts
			create : nodejs-demo/public/stylesheets
			create : nodejs-demo/public/stylesheets/style.css
			create : nodejs-demo/routes (路由目录,以后在这个目录下开发程序，然后在app.js里use)
			create : nodejs-demo/routes/index.js
			create : nodejs-demo/routes/users.js
			create : nodejs-demo/views (视图目录，视图模板文件等)
			create : nodejs-demo/views/index.ejs
			create : nodejs-demo/views/error.ejs
			create : nodejs-demo/bin
			create : nodejs-demo/bin/www （启动文件，用于启动app.js）

 - install dependencies:

			$ cd nodejs-demo && npm install

 - run the app:

			$ DEBUG=nodejs-demo ./bin/www
项目创建成功。

 - 根据上述提示安装依赖：

			cd nodejs-demo && npm install

 - 根据提示启动web：
 
			$ DEBUG=nodejs-demo ./bin/www

不过我们这里不打算使用该方法启动程序。原因是我们在开发过程中需要使用nodemon这么一个工具。   
nodemon用于动态识别开发过程中项目的改变，然后动态加载（这是Eclipse种开发java web类似）。该工具是开发web的必备啊

 - 安装nodemon：

	npm install nodemon -g

那么为什么我们上面不使用./bin/www脚本呢？   
原因是nodemon ./bin/www 这样是没有办法识别项目的改动。   
修改app.js：   
把最有一行//module.exports = app;注释掉   
换成：app.listen(3000);   
使用下面命令启动app.js主程序：

	nodemon app.js

hadoop@sven:~/workspace/nodeJs/nodejs-demo$ nodemon app.js   
然后修改程序，看看是否会动态加载。会有下面提示：   

	1 Dec 16:22:07 – [nodemon] restarting due to changes…    
	1 Dec 16:22:07 – [nodemon] starting `node app.js`   

表示生效。   
测试：   
本地的3000端口被打开，通过浏览器访问: localhost:3000   

如果运行nodejs代码Error: listen EADDRINUSE   
错误listen EADDRINUSE 是比较常见的错误。‘EADDRINUSE’，借助有道的翻译，意思是：错误地址使用。‘EADDRINUSE’应该是‘error address in use’的缩写。后来借助google找到了合理的解释，说是你监听的端口已经被使用了!换个端口号。