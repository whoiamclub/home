---
title: jsonp
date: 2017-07-02 13:32:48
tags: [javascript,跨域]
categories: 前端
description: 数据交互与dom操作并列前端两大基石
---

JSONP(JSON with Padding)是JSON的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。由于同源策略，一般来说位于 server1.example.com 的网页无法与不是 server1.example.com的服务器沟通，而 HTML 的&lt;script&gt;元素是一个例外。利用 &lt;script&gt;元素的这个开放策略，网页可以得到从其他来源动态产生的 JSON 资料，而这种使用模式就是所谓的 JSONP。用 JSONP 抓到的资料并不是 JSON，而是任意的JavaScript，用 JavaScript 直译器执行而不是用 JSON 解析器解析。
<!--more-->
## Jsonp原理 
在客户端定义一个callbackFunction, 然后把callbackFunction的名字传给服务器。

服务器先生成 json 数据。然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的参数 jsonp的值.

最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。

客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，传入到了客户端预先定义好的 callbackFunction 函数里.（动态执行回调函数）

## 服务器端对JSONP支持

请求： http://example.com/servlet?jsonp=callbackFunction。
期望数据：["param1","param2"]
前段通过&lt;script&gt;加载文档并调用。实现callbackFunction函数调用

Java:
``` bash
return request.getParameter("callbackFunction")+"("+JsonString+")";
```
返回内容像：callbackFunction(["param1","param2"])

## 客户端实现跨域请求

在客户端调用提供JSONP支持的URL Service，获取JSONP格式数据。
### 创建script标签
``` bash
var head= document.getElementsByTagName('head')[0]; 
var script= document.createElement('script'); 
script.type= 'text/javascript'; 
script.src= 'http://example.com/servlet?jsonp=callbackFunction'; 
head.appendChild(script); 
```
结果：
``` bash
<head>
	...
	<script type="text/javascript" src="http://example.com/servlet?jsonp=callbackFunction"></script>
</head>
```
### 客户端实现 callbackFunction 函数(全局)
``` bash
function callbackFunction(result) {  
    for(var i in result) {  
        alert(i+":"+result[i]); 
    }  
}  
```

## 监听jsonp

Jsonp本质上就是一个异步的get请求，但是他跟ajax理论上毫无关联。
创建的script标签加载过程中同样拥有onreadystatechange事件与onload事件，同样也拥有onerror事件。我们可以通过这些来观察jsonp回调。
``` bash
<script type="text/javascript">
	var head= document.getElementsByTagName('head')[0]; 
	var script= document.createElement('script'); 
	script.type= 'text/javascript'; 
	script.onload = script.onreadystatechange = function() { 
		if (!this.readyState || this.readyState === "loaded" || this.readyState === "complete" ) { 
			alert('加载成功')
			script.onload = script.onreadystatechange = null; 
		} 
	}; 
	script.onerror = function(){
		alert('加载失败')
	}
	script.src= 'jsonp.js'; 
	head.appendChild(script); 
</script>
```
除此之外，考虑到安全问题，我们可以通过使用正则表达式检查 JSON 字符。

js代码
``` bash
	var my_JSON_object = !(/[^,:{}\[\]0-9.\-+Eaeflnr-u \n\r\t]/.test(text.replace(/"(\\.|[^"\\])*"/g, ' '))) && eval('(' + text + ')');  
```
