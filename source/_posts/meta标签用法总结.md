---
title: meta标签用法总结
date: 2017-07-02 13:08:57
tags: [html,初级]
categories: 前端面试圣经初级
---

<meta>标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。

<!-- more -->

##### SEO优化

    关键字： 
        <meta name="keywords" content="your tags" />
    描述： 
        <meta name="description" content="150 words" />
    搜索引擎索引方式：
        <meta name="robots" content="index,follow" />
         <!--
             all：文件将被检索，且页面上的链接可以被查询；
             none：文件将不被检索，且页面上的链接不可以被查询；
             index：文件将被检索；
             follow：页面上的链接可以被查询；
             noindex：文件将不被检索；
             nofollow：页面上的链接不可以被查询。
          -->
    页面重定向和刷新：
        <meta http-equiv="refresh" content="0;url=" />
    定义网页作者：
        <meta name="author" content="author name" />

##### 移动设备

    viewport：
        <meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
        <!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边  -->
        width：宽度（数值 / device-width）（范围从200 到10,000，默认为980 像素）
        height：高度（数值 / device-height）（范围从223 到10,000）
        initial-scale：初始的缩放比例 （范围从>0 到10）
        minimum-scale：允许用户缩放到的最小比例
        maximum-scale：允许用户缩放到的最大比例
        user-scalable：用户是否可以手动缩 (no,yes)
    WebApp全屏模式：
        伪装app，离线应用   
        <meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->
    隐藏状态栏/设置状态栏颜色：
        只有在开启WebApp全屏模式时才生效。
        content的值为default | black | black-translucent 。
        <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
    添加到主屏后的标题：
        <meta name="apple-mobile-web-app-title" content="标题">
    忽略数字自动识别为电话号码：
        <meta content="telephone=no" name="format-detection" /> 
    忽略识别邮箱：
        <meta content="email=no" name="format-detection" />
    添加智能 App 广告条 Smart App Banner：
        告诉浏览器这个网站对应的app，并在页面上显示下载banner。
        <meta name="apple-itunes-app" 
        content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL"> 
    其他：
        <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
        <meta name="HandheldFriendly" content="true">
        <!-- 微软的老式浏览器 -->
        <meta name="MobileOptimized" content="320">
        <!-- uc强制竖屏 -->
        <meta name="screen-orientation" content="portrait">
        <!-- QQ强制竖屏 -->
        <meta name="x5-orientation" content="portrait">
        <!-- UC强制全屏 -->
        <meta name="full-screen" content="yes">
        <!-- QQ强制全屏 -->
        <meta name="x5-fullscreen" content="true">
        <!-- UC应用模式 -->
        <meta name="browsermode" content="application">
        <!-- QQ应用模式 -->
        <meta name="x5-page-mode" content="app">
        <!-- windows phone 点击无高光 -->
        <meta name="msapplication-tap-highlight" content="no">
    
##### 网页相关    
    
    申明编码：
        <meta charset='utf-8' />
    优先使用 IE 最新版本和 Chrome：
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <!-- 关于X-UA-Compatible -->
        <meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->
        <meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 使用IE7 -->
        <meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->
    浏览器内核控制：
        国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。
        而添加meta标签的网站可以控制浏览器选择何种内核渲染。
        <meta name="renderer" content="webkit|ie-comp|ie-stand">
    国内双核浏览器默认内核模式如下：
        1. 搜狗高速浏览器、QQ浏览器：IE内核（兼容模式）
        2. 360极速浏览器、遨游浏览器：Webkit内核（极速模式）
    
    禁止浏览器从本地计算机的缓存中访问页面内容：这样设定，访问者将无法脱机浏览。
        <meta http-equiv="Pragma" content="no-cache">
    Windows 8
        <meta name="msapplication-TileColor" content="#000"/> <!-- Windows 8 磁贴颜色 -->
        <meta name="msapplication-TileImage" content="icon.png"/> <!-- Windows 8 磁贴图标 -->
    站点适配：主要用于PC-手机页的对应关系。
        <meta name="mobile-agent"content="format=[wml|xhtml|html5]; url=url">
        <!--
        [wml|xhtml|html5]根据手机页的协议语言，选择其中一种；
        url="url" 后者代表当前PC页所对应的手机页URL，两者必须是一一对应关系。
        -->
    转码申明：用百度打开网页可能会对其进行转码（比如贴广告），避免转码可添加如下meta
        <meta http-equiv="Cache-Control" content="no-siteapp" />