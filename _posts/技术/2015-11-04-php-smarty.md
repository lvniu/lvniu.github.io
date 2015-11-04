---
layout: post
title: "php模板-smarty"
description: ""
category: "技术" 
tags: "php smarty" 
---

### 1、assign()
主要是把程序里面的值付给模板,因为使用smarty时,模板里面是没有PHP代码的,无法显示在操作过程序产生的变量的值,所以就通过个函数把PHP里面的值给smarty,这样就能在模板里显示了       



例如:     
如果我想在页面上显示一个变量的值,如     
		$abc = "这是一个变量的值";            


然后我在程序里用SMARTY的ASSIGN()函数如下:     
		$smarty->assign("aaa",$abc);        


这时,在smarty类里面就会有一个变量aaa里面保存着$abc的值,这样在模板里就可以像如下的方式显示出他的值。      
变量的值是:{$aaa}              

*注意：*       
- 如果html的代码中有{}，在html{}中间必须加{literal}{/literal}，这样才能正常显示。              

- PHP在linux的调试可以使用：php XXX.php 这样就能显示错误信息了。                   
