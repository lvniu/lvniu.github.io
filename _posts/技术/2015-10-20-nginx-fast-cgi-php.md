---
layout: post
title: "ubuntu中配置nginx和fast-cgi来解析php"
description: ""
category: "nginx" 
tags: "技术" 
---

### 1、nginx和fast-cgi解析php模式       
Nginx完全是轻量级的，必须借助第三方的FastCGI处理器才可以对PHP进行解析，因此其实这样看来Nginx是非常灵活的，它可以和任何第三方提供解析的处理器实现连接从而实现对PHP的解析(在nginx.conf中很容易设置)。    



Nginx可以使用spwan-fcgi。在早期版本中需要安装lighttpd，但是在9.10版本以后直接安装spawn-fcgi就可以。现在出现了新的第三方的PHP的FastCGI处理器，叫做PHP-FPM，可以了解一下。本文基于spawn-fcgi实现对PHP模块的支持。      



### 2、nginx安装     
nginx下载地址：http://nginx.org/en/download.html    
源码安装：     


		$wget http://nginx.org/download/nginx-1.9.5.tar.gz
		$./configure --prefix=/usr/local/nginx
		$make
		$make install       	



安装成功之后，nginx放置在/usr/local/nginx目录下，主要的配置文件为conf目录下的nginx.conf,nginx的启动文件在sbin目录下的nginx文件。     



### 3、启动nginx     
		$cd /usr/local/nginx
		$sbin/nginx    
然后就可以访问了，http://localhost/index.html    
如果可以成功访问，说明nginx安装成功，可以解析例如html静态页面了，但是还无法解析php页面。如果不能访问请查看原因，可以查看/logs目录下的error.log日志。    


### 4、安装fast-cgi    
		$wget http://www.lighttpd.net/download/spawn-fcgi-1.6.3.tar.gz
		$./configure --prefix=/usr/local/nginx
		$make
		$make install     
安装之后，spawn-fcgi命令就可以直接使用了，它的可执行文件在/usr/local/bin/spawn-fcgi。    



### 5、fast-cgi启动    
fast-cgi启动时，主要是解析相应版本php，如果安装多个版本的php，需要选择特定版本下的php-cgi文件，完成fast-cgi的启动。   
		$spawn-fcgi -a 127.0.0.1 -p 9000 -C 10 -u www-data -f /usr/local/php/bin/php-cgi    



### 6、配置nginx    
到此为止，nginx和fast-cgi已经基本安装完成。但是还不能解析php，还需要配置nginx。nginx配置文件在/usr/local/nginx/conf目录下的nginx.conf。        

首先，修改服务端口。如果服务器上同时安装有apache，则需要注意端口不要重复，我这里把端口修改为了8089。在location中添加php的入口，即index.php。然后，打开fastcgi的监听端口，即第二个location。特别要注意。服务路径root要修改为自己的服务路径。fastcgi_param中的变量$fastcgi_script_name要跟root的服务路径相同。     



		server {
				listen       8089;
				server_name  localhost;
				location / {
            root   html;
            index  index.html index.htm index.php;
        }
        location ~ \.php$ {
            root           /usr/local/nginx/html;
            fastcgi_pass   127.0.0.1:9000;
            #fastcgi_pass   182.92.4.218:8089;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx/html/$fastcgi_script_name;
						include        fastcgi_params;
				}    
		}      





 
