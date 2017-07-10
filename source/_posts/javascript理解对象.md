---
title: javascript理解对象
date: 2017-07-07 22:05:40
tags: [javascript]
categories: 前端
---
EMCAScript中有两种属性：数据属性和访问器属性。
<!-- more -->
#### 1.数据属性
数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4个描述其行为的特性。
①[[Configurable]]:表示能否通过Delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。默认值为true。
②[[Enumerable]]:表示能通过fro-in循环返回属性。默认值为true。
③[[Writable]]:表示能否修改属性的值。默认值为true。
④[[Value]]:包含这个属性的值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。默认值为undefined。
修改属性默认的特性,使用Object.defineProperty()方法。这个方法接收3个参数：属性所在的对象、属性的名字和一个描述符对象。其中，描述符对象的属性必须是：configurable、enumerable、writable和value。
    
    var person = {};
    Object.defineProperty{
        person,
        "name",
        {
            writable:false,
            value: "Tom"
        }
    }
在调用Object.defineProperty()方法时，如果不指定，configurable、enumerable和writable特性的默认值都是false。
注：IE8及以下不建议使用该方法。

#### 2.访问器属性
访问器属性不包含数值：访问器属性有如下4个特性。
①[[Configurable]]:表示能否通过Delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。默认值为true。
②[[Enumerable]]:表示能通过fro-in循环返回属性。默认值为true。
③[[Get]]:在读取属性时调用的函数。默认的是undefined。
④[[Get]]:在写入属性时调用的函数。默认的是undefined。

#### 3.读取属性的特性
使用Object.getOwnPropertyDescriptor()方法，可以取得给定属性的描述符。这个方法接受两个参数：属性所在的对象和要读取其描述符的属性名称。返回一个对象，如果是访问器属性，这个对象的属性有configurable、enumerable、get和set;如果是数据属性，这个对象的属性有configurable、enumerable、writable和value。
