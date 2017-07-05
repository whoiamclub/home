---
title: ajax浅析
date: 2017-07-02 13:32:29
tags: [javascript]
categories: 前端
description: 数据交互与dom操作并列前端两大基石
---

<!-- toc -->
AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。
AJAX = 异步 JavaScript和XML（标准通用标记语言的子集）。
AJAX 是一种用于创建快速动态网页的技术。
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
<!--more-->
## XMLHttpRequest 是 AJAX 的基础
注：IE5 和 IE6 使用 ActiveXObject。

## 创建 XMLHttpRequest 对象
所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。
创建 XMLHttpRequest 对象的语法：
>variable=new XMLHttpRequest();

Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：
>variable=new ActiveXObject("Microsoft.XMLHTTP");

``` bash
//创建
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
```

## XMLHttpRequest对象用于和服务器交换数据

### XMLHttpRequest对象的方法
open(method,url,async)
>method：请求的类型；GET 或 POST
>url：文件在服务器上的位置
>async：true（异步）或 false（同步）

POST请求 send(string)
GET请求 send()

setRequestHeader(header,value)
>header: 规定头的名称
>value: 规定头的值

### XMLHttpRequest对象的属性
onreadystatechange  当 readyState 属性改变时，就会触发该事件

readyState	 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
>0: 请求未初始化
>1: 服务器连接已建立
>2: 请求已接收
>3: 请求处理中
>4: 请求已完成，且响应已就绪

status	
>200: "OK"
>300~307: 重定向类
>40*: 请求错误
>50*: 服务器错误

## 服务器响应
>responseText	获得字符串形式的响应数据。
>responseXML	获得 XML 形式的响应数据。

## 例子
### get请求
``` bash
//创建XMLHttpRequest对象
var xmlHttp = new XMLHttpRequest();

//配置XMLHttpRequest对象
xmlHttp.open("get", "url?key=value");

//设置回调函数
xmlHttp.onreadystatechange = function () {
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
        var result= xmlHttp.responseText;
    }
}
//发送请求
xmlHttp.send(null);
```
### post请求
``` bash
//创建XMLHttpRequest对象
var xmlHttp = new XMLHttpRequest();

//配置XMLHttpRequest对象
xmlHttp.open("post", "url", data);

//设置回调函数
xmlHttp.onreadystatechange = function () {
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
        var result= xmlHttp.responseText;
    }
}
//发送请求
xmlHttp.send(data);
```

## ajax简单封装实例

``` bash
<script type="text/javascript">
	function ajax(config) {

	  	var xhr = null;
	  	try{
			xhr = new XMLHttpRequest();
	  	}catch(e){
			try{
				xhr = new ActiveXObject('MSXML2.XMLHttp');
			}catch(e){
				xhr = new ActiveXObject('Microsoft.XMLHTTP');
			}
		}

		var date = new Date();
	  	config.url = config.url + '?timestamp=' + date.getTime();

		if (config.method === 'get') {
			var arr = [];
			for (var i in config.data) {
			    arr.push(encodeURIComponent(i) + '=' + encodeURIComponent(config.data[i]));
		  	}
		  	config.data = arr.join('&')
		    config.url += config.data; 
		}

		if (config.async === true) { 
		    xhr.onreadystatechange = function () {
		      	if (xhr.readyState == 4) {
		        	callback();
		      	}
		    };
		}

	  	xhr.open(config.method, config.url, config.async);

		if (config.method === 'post') {
		    xhr.setRequestHeader('Content-Type', 'application/json');
		    xhr.send(JSON.stringify(config.data));
		} else {
		    xhr.send(null);
		}

		if (config.async === false) {
		    callback();
		}

		function callback() {
		    if (xhr.status == 200) {
		      	config.success(xhr.responseText);
		    } else {
		      	alert('获取数据错误！错误代号：' + xhr.status + '，错误信息：' + xhr.statusText);
		    }	
		}
	}	
</script>
```