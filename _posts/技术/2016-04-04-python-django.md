---
layout: post
title: "基于Django框架的python学习"
description: ""
category: "技术"
tags: "python Django" 
---


### 1. 安装   

	$tar zxf Django-1.9.5.tar.gz    
	$cd Django-1.9.5    
	$sudo python setup.py install --record files.txt    
*注释：*--record files.txt 是为了记录django安装的目录，默认是安装在python目录下，我的是安装在了python2.7/site-packages/目录下面    


安装完成后：    

	$which django-admin.py    

如果找到django-admin.py，说明安装成功       
或者：在命令行执行如下内容：       

	>>>import django     
	>>>django.VERSION     
如果显示django版本号(1, 9, 5, 'final', 0)，则说明安装成功           


### 2. 生成第一个Demo项目     

- 新建文件夹        
	`$ mkdir jango-website`          
	`$ cd jango-website`          
- 新建一个网站       
    `$ django-admin.py startproject FirstWebsite`     

- 使用tree命令，查看站点结构：     
	`$ cd FirstWebsite/`       
	`$ tree`            

	|-- FirstWebsite          
	|   |-- __init__.py          
	|   |-- settings.py          
	|   |-- urls.py          
	|   -- wsgi.py          
	|-- manage.py            

	1 directory, 5 files    

### 3. 启动django项目     
- 在FirstWebsite目录下执行下面命令      
    `$python manage.py runserver 0.0.0.0:8002`  
*注：*8002是端口号       

- 在浏览器内输入：http://127.0.0.1:8002，检查django是否运行正常。       

	-- 如果执行python manage.py runserver 0.0.0.0:8002报错：          
You have unapplied migrations; your app may not work properly until they are applied. Run 'python manage.py migrate' to apply them.           
	-- 如果浏览器上显示错误信息：A server error occurred. Please contact the administrator.       
	-- 那就执行一下：python manage.py migrate       
	它可以让我们在修改Model后可以在不影响现有数据的前提下重建表结构。           

### 4. 把项目部署到nginx上      
[请查看博客](http://www.cnblogs.com/xiongpq/p/3381069.html)中的配置uwsgi和设置nginx模块      

### 5. 添加app模块      
django中的app（应用模块）也就是项目里的模块的概念，每个app模块单独的路径目录，方便代码的复用。      

- 新建app模块，执行如下命令：    
	`python manage.py startapp article`    
*注：*article是自定义的app名称    
现在查看树形结构如下：    
	|-- article     
	|   |-- __init__.py    
	|   |-- admin.py    
	|   |-- apps.py    
	|   |-- migrations    
	|   |-- __init__.py    
	|   |-- models.py    
	|   |-- tests.py    
	|   |-- views.py    
	|-- db.sqlite3    
	|-- manage.py    
	|-- FirstWebsite    
	|   |-- __init__.py     
	|   |-- __init__.pyc      
	|   |-- settings.py     
	|   |-- settings.pyc     
	|   |-- urls.py     
	|   |-- urls.pyc     
	|   |-- wsgi.py    
	|   |-- wsgi.pyc    

- 将article模块添加到设定档    
打开FirstWebsite/settings.py，找到 INSTALLED_APPS，調整如下：    
	`# FirstWebsite/settings.py`    
	`... `    
	`# Application definition`    
	`INSTALLED_APPS = (`    
	`    'django.contrib.admin',`    
	`    'django.contrib.auth',`   
	`    'django.contrib.contenttypes',`     
	`    'django.contrib.sessions',`     
	`    'django.contrib.messages',`     
	`    'django.contrib.staticfiles',`     
	`    'article',`     
	`)`     

- 预安裝的 Django app    
	Django 已將常用的app设定为INSTALLED_APPS 。例如，auth（使用者认证）、admin （管理后台）... 等等，我们可依需求自行增減。     
### 6. Django的MTV架构
- 其处理request的流程如下：    
浏览器发送 HTTP request请求    
Django根据URL configuration 分配至对应的 View     
View 进行资料库的操作或其他运算，并返回HttpResponse物件    
浏览器根据 HTTP response 返回内容，显示页面    

- 创建view函数    
在article/view.py中添加如下内容：    


		from django.http import HttpResponse       
		def hello_world(request):       
		     return HttpResponse("Hello World!")      
- url配置    
通常定义在 urls.py文件中，是一连串的规则則 (URL patterns)    
Django 收到 request 时，会一一比对 URL conf 中的规则，決定要执行哪个view function    
在FirstWebsite/urls.py文件中添加如下内容：    



		`# mysite/urls.p    
		from django.conf.urls import include, url    
		from django.contrib import admin     
		     
		from article.views import hello_world    
		     
		urlpatterns = [     
		    url(r'^admin/', include(admin.site.urls)),    
		    url(r'^hello/$', hello_world),    
		]`    

	以上程式通过 url() function 传入两个参数 regex, view：    
	url(regex, view)    
	regex -- 定义url规则    
	规则以 regular expression（正则表示式）来表达    
	r'^hello/$' 代表的是 hello/ 这类URL    
	view -- 对应的 view function    
	指的是 hello_world 这个 view    

ok，现在就可以开启django服务，访问一下试试了：http://127.0.0.1:8000/hello/    


### 6. 关于django的其他细节
关于django的其他内容，包括templates（资料夹）、model层的优化、admin管理等，请[查看博客](https://djangogirlstaipei.gitbooks.io/django-girls-taipei-tutorial/content/index.html)    



