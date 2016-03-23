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


### 14、文件操作     
fopen(), fread(), fclose()。     
例如：     


		<?php           
			$myfile = fopen("webdictionary.txt", "r") or die("Unable to open file!");                
			echo fread($myfile,filesize("webdictionary.txt"));            
			fclose($myfile);             
		?>           



PHP 检查 End-Of-File - feof()    
-   feof() 函数检查是否已到达 "end-of-file" (EOF)。    
-   feof() 对于遍历未知长度的数据很有用。    



其他文件操作函数，请查看：http://www.w3school.com.cn/php/php_ref_filesystem.asp   



### 15、cookie和session用法    
cookie：   


		<meta http-equiv='Content-Type' content='text/html; charset=utf-8' />                          
		<?php                
		if($_GET['out'])              
			{   //用于注销cookies                  
		    setcookie('id',"");               
		    setcookie('pass',"");               
		    echo "<script>location.href='login.php'</script>"; //因为cookies不是及时生效的，只有你再次刷新时才生效，所以，注销后让页面自动刷新。            
			}             

		if($_POST['name']&&$_POST['password']) //如果变量用户名和密码存在时，在下面设置cookies               
			{   //用于设置cookies                 
		    setcookie('id',$_POST['name'],time()+3600);               
		    setcookie('pass',$_POST['password'],time()+3600);             
		    echo "<script>location.href='login.php'</script>"; //让cookies及时生效                   
			}              
 
		if($_COOKIE['id']&&$_COOKIE['pass'])             
			{   //cookies设置成功后，用于显示cookies            
		    echo "登录成功！<br />用户名：".$_COOKIE['id']."<br/>密码：".$_COOKIE['pass'];             
		    echo "<br />";           
		    echo "<a href='login.php?out=out'>注销cookies</a>";  //双引号内，如果再有引号，需要用单引号。     
			}     
		?>      
		<form action="" method="post">     
		用户ID：    
		<input type="text" name="name" /><br/><br/>    
		密码：    
		<input type="password" name="password" /><br/><br />
		<input type="submit" name="submit">
		</form>



session用法：            


		<meta http-equiv='Content-Type' content='text/html; charset=utf-8' />      
		<?php             
		//session用法实例                   
		session_start();//启动session，必须放在第一句，否则会出错。           
		if($_GET['out'])         
		{          
		    unset($_SESSION['id']);      
				unset($_SESSION['pass']);
		}

		if($_POST['name']&&$_POST['password'])
		{   
		   //用于设置session
		    $_SESSION['id']=$_POST['name'];
		    $_SESSION['pass']=$_POST['password'];
		}

		if($_SESSION['id']&&$_SESSION['pass'])
		{
		    echo "登录成功！<br/>用户ID：".$_SESSION['id']."<br />用户密码：".$_SESSION['pass'];
		    echo "<br />";
		    echo "<a href='login.php?out=out'>注销session</a>";
		}

		?>
		<form action="login.php"  method="post">
		用户ID：
		<input type="text" name="name" /><br/><br/>
		密码：
		<input type="password" name="password" /><br/><br />
		<input type="submit" name="submit">
		</form>



### 16、php过滤器函数和过滤器    
过滤器函数：    
- filter_var() - 通过一个指定的过滤器来过滤单一的变量    
- filter_var_array() - 通过相同的或不同的过滤器来过滤多个变量    
- filter_input - 获取一个输入变量，并对它进行过滤    
- filter_input_array - 获取多个输入变量，并通过相同的或不同的过滤器对它们进行过滤     
[具体请查看：](http://www.w3school.com.cn/php/php_filter.asp)      

Validating 过滤器：     
- 用于验证用户输入    
- 严格的格式规则（比如 URL 或 E-Mail 验证）    
- 如果成功则返回预期的类型，如果失败则返回 FALSE    
Sanitizing 过滤器：    
- 用于允许或禁止字符串中指定的字符    
- 无数据格式规则    
- 始终返回字符串     



### 17、php中的xml解析器    
xml Expat Parser--基于事件的解析器
xml DOM--基于树的解析器
xml SimpleXML--是一种取得元素属性和文本的便利途径

### 18、AJAX
- AJAX实现下拉列表   
[请查看](http://www.w3school.com.cn/php/php_ajax_xml.asp)   
- 读取数据库内容   
[请查看](http://www.w3school.com.cn/php/php_ajax_database.aspi)   
- 把读取的数据库内容保存为xml格式    
[请查看](http://www.w3school.com.cn/php/php_ajax_responsexml.asp)   
- 实时检索    
[请查看](http://www.w3school.com.cn/php/php_ajax_livesearch.asp)    
- 实现RSS阅读工具   
[请查看](http://www.w3school.com.cn/php/php_ajax_rss_reader.asp)    
- 实现选票系统    
[请查看](http://www.w3school.com.cn/php/php_ajax_poll.asp)   

### 19、php链接数据库
查询mysql数据，并以excel形式展示。一开始，我总想着直接导出excel，后来发现，还是比较麻烦的，不适合实时开发使用，可以先导出txt，然后再复制到excel。这里就需要注意，需要对读取的数据进行空格和换行操作，这样才能保证复制到excel里面的数据是规格化的，行列分明。    


多的不说了，直接上代码：     


		<?php
				$mysql_server_name='ip:port'; //自己的mysql数据库服务器地址和端口    
				$mysql_username='sqlname'; //自己的mysql数据库用户名      
				$mysql_password='123456'; //自己的mysql数据库密码      
				$mysql_database='databasename'; //自己的mysql数据库名      
				$conn=mysql_connect($mysql_server_name,$mysql_username,$mysql_password) or die("error connecting") ; //连接数据库         
				mysql_query("set names 'utf8'");        
				mysql_select_db($mysql_database, $conn); //打开数据库       
				ini_set('memory_limit','256M');//这是设置内存大小，防止操作的数据量过大，导致失败      
				$problem = array();      
				$user_id = array(123, 456, 789);     
				foreach($user_id as $val){       
						$sql ="select *  from user_info  where user_id=".$val." ORDER BY create_date DESC" ; //SQL语句       
						$result = mysql_query($sql,$conn); //查询       
						while($row = mysql_fetch_array($result, 1))       
						{     
								$problem[] = $row;     
						}       
				}      
				mysql_close($conn);        
				$fp = fopen('./file.txt', 'a+b');         
				foreach($problem as $item){             
				$str =implode("\t", $item);//对每一行的数据转换为字符串，并空格隔开                 
				fwrite($fp,"$str");             
				$res = fwrite($fp,"\r\n");//对不同行的数据，换行           
        }        
				fclose($fp);   
		?> 



### 20、利用phpExcel读取excel内容       
读取Excel的内容，主要有两个选择，第一个是PHPExcelReader，另外一个是PHPExcel。     


PHPExcelReader比较轻量级，仅支持Excel的读取，实际上就是一个Reader。但是可惜的是不能够支持Excel 2007的格式（.xlsx）。      


PHPExcel比较强大，能够将内存中的数据输出成Excel文件，同时还能够对Excel做各种操作，下面主要介绍下如何使用PHPExcel进行Excel文件的读取。         


首先下载phpExcel：[下载地址](http://download-codeplex.sec.s-msft.com/Download/Release?ProjectName=phpexcel&DownloadId=809026&FileTime=130382506283700000&Build=21031)。       


然后，创建一个php文件，来实现读取excel的操作。我这里创建一个readExcel.php文件，文件内容如下：            


		<?php               

		require_once('./Classes/PHPExcel/IOFactory.php');//我把phpexcel解压到当前文件夹了                 
		$file = "tongji.xlsx";     
		$type = strtolower( pathinfo($file, PATHINFO_EXTENSION) );//因为excel中的行列都是大写字母表示的，所以要先转换为小写       

		$path = './'.$file;            

		if (!file_exists($path)) {              
   		   die('no file!');         
		}          

		//根据不同类型分别操作                 
		if( $type=='xlsx'||$type=='xls' ){               
  		$objPHPExcel = PHPExcel_IOFactory::load($path);              
		}               
		else if( $type=='csv' ){             
   		 $objReader = PHPExcel_IOFactory::createReader('CSV')          
     		    ->setDelimiter(',')                  
       		  ->setInputEncoding('GBK') //不设置将导致中文列内容返回boolean(false)或乱码             
        		->setEnclosure('"')            
        		->setLineEnding("\r\n")             
        		->setSheetIndex(0);          
   		 $objPHPExcel = $objReader->load($path);           

		}                
		else{                 
   		 die('Not supported file types!');           
		}                        
		/*如果想循环操作不同的表        
		$sheetCount = $objPHPExcel->getSheetCount();//获取excel文件包含的总共的表的个数               
		//然后循环操作不同的表     	
		for($i = 0; $i < $sheetCount; $i++)
		{        
				$sheet = $objPHPExcel->getSheet($i);       
				......     
				......    
		}      
		*/
		//选择标签页                
		$sheet = $objPHPExcel->getSheet(0);          

		//获取行数与列数,注意列数需要转换                 
		$highestRowNum = $sheet->getHighestRow();                 
		$highestColumn = $sheet->getHighestColumn();           
		$highestColumnNum = PHPExcel_Cell::columnIndexFromString($highestColumn);         

		//取得字段，这里测试表格中的第一行为数据的字段，因此先取出用来作后面数组的键名             
		$filed = array();                   
		for($i=0; $i<$highestColumnNum;$i++){          
 	 		 $cellName = PHPExcel_Cell::stringFromColumnIndex($i).'1';       
  		 $cellVal = $sheet->getCell($cellName)->getValue();//取得列内容     
  		 $filed []= $cellVal;               
	 	}               
 
		 //开始取出数据并存入数组               
		$data = array();                 
		for($i=2;$i<=$highestRowNum;$i++){                   
   		    //ignore row 1                      
     		  $row = array();          
       		for($j=0; $j<$highestColumnNum;$j++){           
         		    $cellName = PHPExcel_Cell::stringFromColumnIndex($j).$i;             
           		  $cellVal = $sheet->getCell($cellName)->getValue();          
             		$row[ $filed[$j] ] = $cellVal;                       
       		}                 
       		$data []= $row;              
		}              

		print_r($data);           



* 注意：*     
如果出现如下错误：      


		Fatal error: Uncaught exception 'PHPExcel_Reader_Exception' with message 'ZipArchive library is not enabled' in \htdocs\excel\Classes\PHPExcel\Reader\Excel2007.php:87      


原因：ZipArchive library is not enabled：出现这个错误说明是程序在调用'ZipArchive' 这个类的时候没有成功，原因是由于在安装php的时候没有增加php zip的支持（非zlib）。         


windows下解决办法：    
请在php.ini找到extension=php_zip.dll并把前面的分号去掉(如果没有，请添加extension=php_zip.dll此行并确保php_zip.dll文件存在相应的目录)，保存后重启php即可。	         

linux下解决办法：      
php安装zip扩展            


		# wget http://pecl.php.net/get/zip-1.10.2.tgz      
		# tar zxvf zip-1.10.2.tgz         
		# cd zip-1.10.2          
		# /usr/local/php/bin/phpize          


运行了这个zip目录下会自动生成几个文件，其中包括configure        


		# ./configure --with-php-config=/usr/local/php/bin/php-config     
		# make          
		# make install           


安装完成后修改一下php.ini      


		# vim /usr/local/php/etc/php.ini     


加入：      


		extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20060613/zip.so      

之后重启apache。     




### 21、apidoc     
apidoc可以根据代码注释生成web api文档，支持大部分主流语言java javascript php coffeescript erlang perl python ruby go...，相对而言，web接口的注释维护起来更加方便，不需要额外再维护一份文档。    
apidoc从注释生成静态html网页文档，不仅支持项目版本号，还支持api版本号。     
具体操作请查阅如下链接：     
[apidoc官网](http://apidocjs.com/)     
[github地址](https://github.com/apidoc/apidoc)    


### 22、php Function is deprecated 的解决办法                


php升级为5.3后，程序会报 Function split() is deprecated 的错误。         
这是因为种种原因（主要是关于正则的原因，具体见后），split这个函数在新版本不支持了。             
在php中，再使用deprecated的函数会报错，必须改掉。（java里deprecated的函数只是给警告，还可以继续用）                
改为什么呢？ 看第一个参数，如果第一个参数不是正则表达式，split改为 explode；如果是正则表达式，split改为preg_split。explode会比以前快很多，因为以前要考虑正则，explode不考虑正则。                 
* POSIX → PCRE                     
* ereg_replace() → preg_replace()            
* ereg() → preg_match()              
* eregi_replace() → preg_replace()        
* eregi() → preg_match()              
* split() → preg_split()               
* spliti() → preg_split()                     
* sql_regcase() → No equivalent     

           
PHP split() 替代方案                
* 需要regex 的split, 可用preg_split() 代替           
* 不需要regex, 只要要快速分割固定的字串, 可用explode() 代替. (速度会比需要regex 的快很多)                    



### 23、php运行模式             
[查看链接](http://www.cnblogs.com/xia520pi/p/3914964.html)      






 





