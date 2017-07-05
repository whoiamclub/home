---
title: 图片预览及Image对象总结
date: 2016-05-29 16:32:54
tags: [html,javascript]
categories: 前端
---

图片预览简单实现

```
<html>
<head>
<meta charset="utf-8" />
<title>图片预览</title>
<script>
function previewFile() {
 var preview = document.querySelector('img');
 var file  = document.querySelector('input[type=file]').files[0];
 var reader = new FileReader();
 reader.onloadend = function () {
  preview.src = reader.result;
 }
 if (file) {
  reader.readAsDataURL(file);
 } else {
  preview.src = "";
 }
}
</script>
</head>
<body>
<input type="file" onchange="previewFile()"><br>
<img src="" height="200" width="300" alt="Image preview..."/>
</body>
</html>
```

<!-- more -->

1、FileReader接口的方法

FileReader接口有4个方法，其中3个用来读取文件，另一个用来中断读取。无论读取成功或失败，方法并不会返回读取结果，这一结果存储在result属性中。

| 方法名             | 参数         	| 描述                  |
| -------------------|------------------|-----------------------|
| readAsBinaryString | file	            | 将文件读取为二进制编码|
| readAsText	     | file,[encoding]	| 将文件读取为文本      |
| readAsDataURL	     | file	            | 将文件读取为DataURL   |
| abort	             | (none)	        | 终端读取操作          |

2、FileReader接口事件
FileReader接口包含了一套完整的事件模型，用于捕获读取文件时的状态。

| 事件          |	描述                   |
| --------------|--------------------------|
| onabort       |	中断                   |
| onerror       |	出错                   |
| onloadstart   |	开始                   |
| onprogress    |	正在读取               |
| onload        |	成功读取               |
| onloadend     |	读取完成，无论成功失败 |


``` bash
<script type="text/javascript">  
var result=document.getElementById("result");  
var file=document.getElementById("file");  
  
//判断浏览器是否支持FileReader接口  
if(typeof FileReader == 'undefined'){  
    result.InnerHTML="<p>你的浏览器不支持FileReader接口！</p>";  
    //使选择控件不可操作  
    file.setAttribute("disabled","disabled");  
}  
  
function readAsDataURL(){  
    //检验是否为图像文件  
    var file = document.getElementById("file").files[0];  
    if(!/image\/\w+/.test(file.type)){  
        alert("看清楚，这个需要图片！");  
        return false;  
    }  
    var reader = new FileReader();  
    //将文件以Data URL形式读入页面  
    reader.readAsDataURL(file);  
    reader.onload=function(e){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML='<img src="' + this.result +'" alt="" />';  
    }  
}  
  
function readAsBinaryString(){  
    var file = document.getElementById("file").files[0];  
    var reader = new FileReader();  
    //将文件以二进制形式读入页面  
    reader.readAsBinaryString(file);  
    reader.onload=function(f){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML=this.result;  
    }  
}  
  
function readAsText(){  
    var file = document.getElementById("file").files[0];  
    var reader = new FileReader();  
    //将文件以文本形式读入页面  
    reader.readAsText(file);  
    reader.onload=function(f){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML=this.result;  
    }  
}  
</script>  
<p>  
    <label>请选择一个文件：</label>  
    <input type="file" id="file" />  
    <input type="button" value="读取图像" onclick="readAsDataURL()" />  
    <input type="button" value="读取二进制数据" onclick="readAsBinaryString()" />  
    <input type="button" value="读取文本文件" onclick="readAsText()" />  
</p>  
<div id="result" name="result"></div>  
```