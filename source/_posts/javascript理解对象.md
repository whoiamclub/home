---
title: javascript理解对象
date: 2017-07-07 22:05:40
tags: [javascript]
categories: 前端
---
EMCAScript中有两种属性：数据属性和访问器属性。
#### 1.数据属性
数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4个描述其行为的特性。
①[[Configurable]]:表示能否通过Delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。默认值为true。
②[[Enumerable]]:表示能通过fro-in循环返回属性。默认值为true。
③[[Writable]]:表示能否修改属性的值。默认值为true。
④[[Value]]:包含这个属性的值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。默认值为undefined。
修改属性默认的特性,使用Object.defineProperty()方法。这个方法接收3个参数