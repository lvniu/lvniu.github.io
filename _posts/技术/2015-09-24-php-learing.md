---
layout: post
title: "php学习笔记"
description: ""
category: "技术" 
tags: "php" 
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



### 4、常量      
有效的常量名以字符或下划线开头（常量名称前面没有 $ 符号）   
如需设置常量，请使用 define() 函数 - 它使用三个参数：    
- 首个参数定义常量的名称    
- 第二个参数定义常量的值    
- 可选的第三个参数规定常量名是否对大小写敏感。默认是 false(对大小写敏感的常量),如果修改为true（对大小写不敏感的常量）。      
		define("TEST", "test");   
		echo TEST."\n"; 



### 5、==和===的区别    
		$str = "test";  
		if($str==0){      
				echo 1;     
		}              
		else{     
				echo 2;       
		}    



结果：1   

		if($str===0){                           
		    echo 1;                                
		}                                      
		else{                                               
		    echo 2;                                  
		}      



结果：2    
*原因：* php是弱类型语言，==只进行数值对比，没有类型判断，对于字符串$str,从左侧开始查找，有没有数字，如果没有，即判断为0。===不光进行数值对比，还进行类型判断，$str是字符串，0是整数，所以不等。




### 6、PHP 逻辑运算符   
- xor	异或


### 7、数组运算   
		$app1 = array("t1", "t2", "t3");  
		$app2 = array("a" => "t4", "b" => "t5", "t1");  
		var_dump($app1 + $app2);       
		var_dump($app1 == $app2);       
		var_dump($app1 != $app2);        
		var_dump($app1 !== $app2);

		
		
结果：   
		array(5) {
				[0]=>
						string(2) "t1"
			  [1]=>
					  string(2) "t2"
			  [2]=>
					  string(2) "t3"
			  ["a"]=>
					  string(2) "t4"
			  ["b"]=>
					  string(2) "t5"
		}
		bool(false)
		bool(true)
		bool(true)



### 8、foreach 循环只适用于数组，并用于遍历数组中的每个键/值对。   
		$app2 = array("a" => "t4", "b" => "t5", "c" => "t6");   
		foreach($app2 as $key => $value){   
				echo $key."=>".$value."\n";     
		}  



### 9、页面加载时函数不会立即执行。函数只有在被调用时才会执行。    
*注释：* 函数名对大小写不敏感。    
默认参数：    

		function Test($name = "xiaoming"){ 
				echo "My name is $name"."\n";  
		}   
		Test(); //使用默认参数值xiaoming                          
		Test("wangwu");  

		
		
结果：    
		My name is xiaoming
		My name is wangwu



### 10、数组    
在 PHP 中，有三种数组类型：   
- 索引数组：带有数字索引的数组   
- 关联数组：带有指定键的数组    
- 多维数组：包含一个或多个数组的数组



*注释：* 如果在运行该函数时两个或多个键相同，则最后的元素会覆盖其他元素    
		$app = array("a" => "t4", "a" => "t5", "b" => "t6");
		echo $app;

		
		
结果：     
		array(2) {
				["a"]=>
						string(2) "t5"
			  ["b"]=>
					  string(2) "t6"
		}
