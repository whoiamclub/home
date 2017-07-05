---
title: 浅谈onerror
date: 2016-04-02 12:55:09
tags: [html]
categories: 前端
---

onerror 事件会在文档或图像加载过程中发生错误时被触发，或者页面中出现脚本错误，也会产生 onerror 事件。
如果需要利用 onerror 事件，就必须创建一个处理错误的函数。你可以把这个函数叫作 onerror 事件处理器 (onerror event handler)。这个事件处理器使用三个参数来调用：msg（错误消息）、url（发生错误的页面的 url）、line（发生错误的代码行）。同样，你也可以不使用他们。
<!--more-->
## 监听脚本错误
``` bash
<!DOCTYPE html>
<html lang="en">
	<meta charset="UTF-8">
	<title>Document</title>
<head>
	<script type="text/javascript">
		onerror=handleErr
		var txt=""
		function handleErr(msg,url,l)
		{
			txt="There was an error on this page.\n\n"
			txt+="Error: " + msg + "\n"
			txt+="URL: " + url + "\n"
			txt+="Line: " + l + "\n\n"
			txt+="Click OK to continue.\n\n"
			alert(txt)
			return true
		}
		function message()
		{
			alertdddlert("Welcome guest!")
		}
	</script>
</head>
<body>
	<input type="button" value="View message" onclick="message()" />
</body>
</html>
```

## 监听资源加载
如果装载图像时发生了错误，则显示一个对话框：
``` bash
<img src="image.gif" onerror="alert('The image could not be loaded.')" />
```
支持该事件的 HTML 标签：
>&lt;img&gt;,&lt;script&gt; , &lt;link&gt; 等

## 使用onerror加载图片
``` bash
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<img src="1.jpg" id='image' onerror="setimg()" alt="pic" style='background-image: url(2.jpg)' />
	<script>
	function setimg(){
		var d_image = document.getElementById('image');
		d_image .setAttribute('src','3.jpg');
		d_image .onerror = '';
	}
	</script>
</body>
</html>
```
利用3张图片，保证在加载第三方资源时不会因为无资源出现UI问题;同样也可以利用onerror监听js、css文件加载，实现二次请求。以及监听jsonp失败。

## 参考内容：
[W3C_onerror事件](http://www.w3school.com.cn/jsref/event_onerror.asp)