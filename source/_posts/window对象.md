---
title: window对象
date: 2017-07-10 15:44:40
tags: [javascript,window]
categories: 前端
---
#### 1.全浏览器兼容，获取浏览器视口大小

    var pageWidth = window.innerWidth,
        pageHeight = window.innerHeight;
    if(typeof pageWidth != "number"){
        if(document.compatMode == "CSS1Compat"){
            pageWidth = document.documentElement.clinetWidth;
            pageHeight = document.documentElement.clinetHeight;
        }else{
            pageWidth = document.body.clinetWidth;
            pageHeight = document.body.clinetHeight;
        }
    }
#### 2.location对象

属性名

    href:设置或返回完整的url.
    host:设置或返回主机名和当前的URL的端口号。
    hostname:设置或返回当前URL的主机名。
    hash:设置或返回从井号（#）开始的URL（锚）。
    pathname:设置或返回当前URL的路径部分。
    port:设置或返回当前URL的端口号。
    protocol:设置或返回当前URL的协议。
    search:设置或返回从问号 (?) 开始的 URL（查询部分）
    
查询制定参数的值
  
    function getQuery(name){
    　  var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
        var r = window.location.search.substr(1).match(reg);
        if (r!=null){
            return decodeURIComponent (r[2]);
        } 
        return null;
    }
    
location操作
    
    location.assign(url) || window.location = url ||location.href = url
    location.replace(url) //没有历史记录
    location.reload(true) //强制刷新
    
#### 3.navigator对象
    
    userAgent
#### 4.screen对象

#### 5.history对象

    history.go(-1) //后退一页
    history.back()
    history.go(1) //前进一页
    history.forward()
    history.go(url)
    