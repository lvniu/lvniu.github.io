---
layout: post
title: "php学习笔记"
description: ""
category: "php" 
tags: "技术" 
---


### 1、在 PHP 中，所有用户定义的函数、类和关键词（例如 if、else、echo 等等）都对大小写不敏感。不过在 PHP 中，所有变量都对大小写敏感。    

### 2、变量是存储信息的容器   

### 3、变量作用域    
函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。     
函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。      
PHP 同时在名为 $GLOBALS[index] 的数组中存储了所有的全局变量。下标存有变量名。这个数组在函数内也可以访问，并能够用于直接更新全局变量。       
		<?php                              
			$app1 = 1;                                                    
			function test(){                                              
				$app2 = 2;                                                
			  global $app1;                                             
			  $GLOBALS['app1'] = 3;                                     
			  echo $app1."\n";                                          
			  echo $GLOBALS['app1']."\n";                               
			}                                                             
			test();                                                       
			echo $app1."\n";                                              
		?>         

