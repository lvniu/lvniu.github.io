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



### 11、php超全局变量   
PHP 中的许多预定义变量都是“超全局的”，这意味着它们在一个脚本的全部作用域中都可用。在函数或方法中无需执行 global $variable; 就可以访问它们。        
这些超全局变量是(9个)：         



- $GLOBALS     
- $_SERVER    
- $_REQUEST     
- $_POST     
- $_GET    
- $_FILES     
- $_ENV    
- $_COOKIE     
- $_SESSION     




### 12、表单处理：get和post      
get：通过 GET 方法从表单发送的信息对任何人都是可见的（所有变量名和值都显示在 URL 中）。GET 对所发送信息的数量也有限制。限制在大于 2000 个字符。不过，由于变量显示在 URL 中，把页面添加到书签中也更为方便。      
post：通过 POST 方法从表单发送的信息对其他人是不可见的（所有名称/值会被嵌入 HTTP 请求的主体中），并且对所发送信息的数量也无限制。此外 POST 支持高阶功能，比如在向服务器上传文件时进行 multi-part 二进制输入。不过，由于变量未显示在 URL 中，也就无法将页面添加到书签。      
使用 htmlspecialchars() 对前端的一些敏感信息进行处理。    
在用户提交该表单时，我们还要做两件事：     
- （通过 PHP trim() 函数）去除用户输入数据中不必要的字符（多余的空格、制表符、换行）     
- （通过 PHP stripslashes() 函数）删除用户输入数据中的反斜杠（\）    
新创建一个php文件：index.php，可以添加验证函数，实现相关变量的验证，如下：   
	


		<! DCOTYPE HTML>
		<html>
		<head>
			<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />  
			<style>
				.error {color: #FF0000;}
			</style>
		<body>
			<?php
				//定义变量并设置为空值
				$nameErr = $emailErr = $genderErr = "";
				$name = $email = $gender = "";
				if($_SERVER["REQUEST_METHOD"] == "POST"){
					if(empty($_POST["name"])){
			      $nameErr = "姓名是必填的";
			  }
			  else{
			      $name = test_input($_POST["name"]);
			      if(!preg_match("/^[a-zA-Z]*$/", $name)){
			         $nameErr = "只允许字母和空格";
			      }
			  }
			  if(empty($POST["email"])){
			      $emailErr = "邮箱是必填的";
			  }
			  else{
			      $email = test_input($_POST["email"]);
			      if(!preg_match("/([\w\-]+\@[\w\-]+\.[\w\-]+)/", $email)){
			         $emailErr = "无效的email格式";
			      }
			  }
			  if(empty($_POST["gender"])){
			      $genderErr = "性别是必选的";
			  }
			  else{
			      $gender = test_input($_POST["gender"]);
			  }
												    
			}

			function test_input($data){
				$data = trim($data);
			  $data = stripslashes($data);
			  $data = htmlspecialchars($data);
			  return $data;
			}
		?>

		<h2>php 验证实例</h2>
		<p><span class = "error">* 必填字段</span></p>
		<form method = "post" action = "<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>">
   		 姓名：<input type = "text" name = "name">
		   <span class = "error">* <?php echo $nameErr; ?></span>
		   <br><br>
		   邮箱：<input type = "text" name = "email">
		   <span class = "error">* <?php echo $emailErr; ?></span>
		   <br><br>
		   评论：<textarea name = "comment" rows = "5" cols = "40"></textarea>
		   <br><br>
		   性别：
		   <input type = "radio" name = "gender" value = "female">女
		   <input type = "radio" name = "gender" value = "male">男
		   <span class = "error">* <?php echo $genderErr; ?> </span>
		   <br><br>
		   <input type = "submit" name = "submit" value = "提交">
		</form>

		<?php
			echo "<h2>您的输入：</h2>";
			echo $name;
			echo "<br>";
			echo $email;
			echo "<br>";
			echo $gender;
		?>
</body>
</head>
</html>

### 13、include和require      
include 和 require 语句是相同的，除了错误处理方面：     
- require 会生成致命错误（E_COMPILE_ERROR）并停止脚本    
- include 只生成警告（E_WARNING），并且脚本会继续    
*注释：*     
- 请在此时使用 require：当文件被应用程序请求时。     
- 请在此时使用 include：当文件不是必需的，且应用程序在文件未找到时应该继续运行时。   


