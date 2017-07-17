---
title: 前端三剑客-js基础大全
date: 2017-06-29 12:31:55
tags: [javascript,初级]
categories: 前端面试圣经初级
---

Javascript包括EMCAScript、DOM和BOM。本文总结了javascript基本数据类型里String和number的常用API,数组、Math、Date函数API,常用DOMAPI以及浏览器特征函数。
<!-- more -->
#### 0.基本类型与引用类型
1.基本类型： string,number,boolean,null,undefined;操作和保存在变量的实际的值。
2.引用类型： Function,Array,Object;值保存在内存中，js不允许直接访问内存，在操作的时候，操作的是对象的引用。

#### 1.字符串API:

    //字符串(String) 
    //1.声明 
    var myString = new String("Every good boy does fine."); 
    var myString = "Every good boy does fine."; 
    
    //2.字符串连接 
    var myString = "Every " + "good boy " + "does fine."; 
    var myString = "Every "; myString += "good boy does fine."; 
    
    //3.截取字符串 
    var myString = "Every good boy does fine."; 
    //截取第 6 位开始的字符 
    var section = myString.substring(6); //结果: "good boy does fine." 
    //截取第 0 位开始至第 10 位为止的字符 
    var section = myString.substring(0,10); //结果: "Every good" 
    //截取从第 11 位到倒数第 6 位为止的字符 
    var section = myString.slice(11,-6); //结果: "boy does" 
    //从第 6 位开始截取长度为 4 的字符 
    var section = myString.substr(6,4); //结果: "good" 
    
    //4.转换大小写 
    var myString = "Hello"; 
    var lcString = myString.toLowerCase(); //结果: "hello" 
    var ucString = myString.toUpperCase(); //结果: "HELLO" 
    
    //5.字符串比较 
    var aString = "Hello!"; 
    var bString = new String("Hello!"); 
    if( aString == "Hello!" ){ } //结果: true 
    if( aString == bString ){ } //结果: true 
    if( aString === bString ){ } //结果: false (两个对象不同,尽管它们的值相同) 
    
    //6.检索字符串 
    var myString = "hello everybody."; 
    // 如果检索不到会返回-1,检索到的话返回在该串中的起始位置 
    if( myString.indexOf("every") > -1 ){ } //结果: true 
    
    ////7.查找替换字符串 
    var myString = "I is your father."; 
    var result = myString.replace("is","am"); //结果: "I am your father." 
    
    //8.特殊字符: 
    //\b : 后退符 \t : 水平制表符 
    //\n : 换行符 \v : 垂直制表符 
    //\f : 分页符 \r : 回车符 
    //\" : 双引号 \' : 单引号 
    //\\ : 反斜杆 
    
    //9.将字符转换成Unicode编码 
    var myString = "hello"; 
    var code = myString.charCodeAt(3); //返回"l"的Unicode编码(整型) 
    var char = String.fromCharCode(66); //返回Unicode为66的字符 
    
    //10.将字符串转换成URL编码 
    var myString = "hello all"; 
    var code = encodeURI(myString); //结果: "hello%20all" 
    var str = decodeURI(code); //结果: "hello all" 
    //相应的还有: encodeURIComponent() decodeURIComponent() 
    
#### 2.数字函数:

    //数字型(Number) 
    //1.声明 
    var i = 1; 
    var i = new Number(1); 
    
    //2.字符串与数字间的转换 
    var i = 1; 
    var str = i.toString(); //结果: "1" 
    var str = new String(i); //结果: "1" 
    i = parseInt(str); //结果: 1 
    i = parseFloat(str); //结果: 1.0 
    //注意: parseInt,parseFloat会把一个类似于"32G"的字符串,强制转换成32 
    
    //3.判断是否为有效的数字 
    var i = 123; var str = "string"; 
    if( typeof i == "number" ){ } //true 
    //某些方法(如:parseInt,parseFloat)会返回一个特殊的值NaN(Not a Number) 
    //请注意第2点中的[注意],此方法不完全适合判断一个字符串是否是数字型!! 
    i = parseInt(str); 
    if( isNaN(i) ){ } 
    
    //4.数字型比较 
    //此知识与[字符串比较]相同 
    
    ///5.小数转整数 
    var f = 1.5; 
    var i = Math.round(f); //结果:2 (四舍五入) 
    var i = Math.ceil(f); //结果:2 (返回大于f的最小整数) 
    var i = Math.floor(f); //结果:1 (返回小于f的最大整数) 
    
    //6.格式化显示数字 
    var i = 3.14159; 
    //格式化为两位小数的浮点数 
    var str = i.toFixed(2); //结果: "3.14" 
    //格式化为五位数字的浮点数(从左到右五位数字,不够补零) 
    var str = i.toPrecision(5); //结果: "3.1415" 
    
    //7.X进制数字的转换 
    var i = parseInt("0x1f",16); 
    var i = parseInt(i,10); 
    var i = parseInt("11010011",2); 
    
    //8.随机数 
    //返回0-1之间的任意小数 
    var rnd = Math.random(); 
    //返回0-n之间的任意整数(不包括n) 
    var rnd = Math.floor(Math.random() * n) 

  
#### 3.数组API

    //定义数组 
    var arr = new Array();  
    
    //数组长度 
    arr.length; 
    
    //shift：删除原数组第一项，并返回删除元素的值；如果数组为空则返回undefined 
    var a = [1,2,3,4,5]; 
    var b = a.shift(); //a：[2,3,4,5] b：1 
    
    //unshift：将参数添加到原数组开头，并返回数组的长度 
    //注：在IE6.0下测试返回值总为undefined，FF2.0下测试返回值为7，
    //所以这个方法的返回值不可靠，需要用返回值时可用splice代替本方法来使用。
    var a = [1,2,3,4,5]; 
    var b = a.unshift(-2,-1); //a：[-2,-1,1,2,3,4,5] b：7 
    
    //pop：删除原数组最后一项，并返回删除元素的值；如果数组为空则返回undefined 
    var a = [1,2,3,4,5]; 
    var b = a.pop(); //a：[1,2,3,4] b：5 
    
    //push：将参数添加到原数组末尾，并返回数组的长度 
    var a = [1,2,3,4,5]; 
    var b = a.push(6,7); //a：[1,2,3,4,5,6,7] b：7 
    
    //concat：返回一个新数组，是将参数添加到原数组中构成的 
    var a = [1,2,3,4,5]; 
    var b = a.concat(6,7); //a：[1,2,3,4,5] b：[1,2,3,4,5,6,7] 
    
    //splice(start,deleteCount,val1,val2,)：从start位置开始删除deleteCount项，从该位置起插入val1,val2, 
    var a = [1,2,3,4,5]; 
    var b = a.splice(2,2,7,8,9); //a：[1,2,7,8,9,5] b：[3,4] 
    var b = a.splice(0,1); //同shift 
    a.splice(0,0,-2,-1); var b = a.length; //同unshift 
    var b = a.splice(a.length-1,1); //同pop 
    a.splice(a.length,0,6,7); var b = a.length; //同push 
    
    //reverse：将数组反序 
    var a = [1,2,3,4,5]; 
    var b = a.reverse(); //a：[5,4,3,2,1] b：[5,4,3,2,1] 
    
    //sort(orderfunction)：按指定的参数对数组进行排序 
    var a = [1,2,3,4,5]; 
    var b = a.sort(); //a：[1,2,3,4,5] b：[1,2,3,4,5] 
    
    //slice(start,end)：返回从原数组中指定开始下标到结束下标之间的项组成的新数组 
    var a = [1,2,3,4,5]; 
    var b = a.slice(2,5); //a：[1,2,3,4,5] b：[3,4,5] 
    
    //join(separator)：将数组的元素组起一个字符串，以separator为分隔符，省略的话则用默认用逗号为分隔符 
    var a = [1,2,3,4,5]; 
    var b = a.join("|"); //a：[1,2,3,4,5] b："1|2|3|4|5" 

#### 4.日期函数:

    //日期型(Date) 
    //1.声明 
    var myDate = new Date(); //系统当前时间 
    var myDate = new Date(yyyy, mm, dd, hh, mm, ss); 
    var myDate = new Date(yyyy, mm, dd); 
    var myDate = new Date("monthName dd, yyyy hh:mm:ss"); 
    var myDate = new Date("monthName dd, yyyy"); 
    var myDate = new Date(epochMilliseconds); 
    
    //2.获取时间的某部份 
    var myDate = new Date(); 
    myDate.getYear(); //获取当前年份(2位) 
    myDate.getFullYear(); //获取完整的年份(4位,1970-????) 
    myDate.getMonth(); //获取当前月份(0-11,0代表1月) 
    myDate.getDate(); //获取当前日(1-31) 
    myDate.getDay(); //获取当前星期X(0-6,0代表星期天) 
    myDate.getTime(); //获取当前时间(从1970.1.1开始的毫秒数) 时间戳！！ 
    myDate.getHours(); //获取当前小时数(0-23) 
    myDate.getMinutes(); //获取当前分钟数(0-59) 
    myDate.getSeconds(); //获取当前秒数(0-59) 
    myDate.getMilliseconds(); //获取当前毫秒数(0-999) 
    myDate.toLocaleDateString(); //获取当前日期 
    myDate.toLocaleTimeString(); //获取当前时间 
    myDate.toLocaleString( ); //获取日期与时间 
    
    //3.计算之前或未来的时间 
    var myDate = new Date(); 
    myDate.setDate(myDate.getDate() + 10); //当前时间加10天 
    //类似的方法都基本相同,以set开头,具体参考第2点 
    
    //4.计算两个日期的偏移量 
    var i = daysBetween(beginDate,endDate); //返回天数 
    var i = beginDate.getTimezoneOffset(endDate); //返回分钟数 
    
    //5.检查有效日期 
    //checkDate() 只允许"mm-dd-yyyy"或"mm/dd/yyyy"两种格式的日期 
    if( checkDate("2006-01-01") ){ } 
    //正则表达式(自己写的检查 yyyy-mm-dd, yy-mm-dd, yyyy/mm/dd, yy/mm/dd 四种) 
    var r = /^(\d{2}|\d{4})[\/-]\d{1,2}[\/-]\d{1,2}$/; 
    if( r.test( myString ) ){ } 


#### 5.数学函数:

    //Math对象 
    1. Math.abs(num) : 返回num的绝对值 
    2. Math.acos(num) : 返回num的反余弦值 
    3. Math.asin(num) : 返回num的反正弦值 
    4. Math.atan(num) : 返回num的反正切值 
    5. Math.atan2(y,x) : 返回y除以x的商的反正切值 
    6. Math.ceil(num) : 返回大于num的最小整数 
    7. Math.cos(num) : 返回num的余弦值 
    8. Math.exp(x) : 返回以自然数为底,x次幂的数 
    9. Math.floor(num) : 返回小于num的最大整数 
    10.Math.log(num) : 返回num的自然对数 
    11.Math.max(num1,num2) : 返回num1和num2中较大的一个 
    12.Math.min(num1,num2) : 返回num1和num2中较小的一个 
    13.Math.pow(x,y) : 返回x的y次方的值 
    14.Math.random() : 返回0到1之间的一个随机数 
    15.Math.round(num) : 返回num四舍五入后的值 
    16.Math.sin(num) : 返回num的正弦值 
    17.Math.sqrt(num) : 返回num的平方根 
    18.Math.tan(num) : 返回num的正切值 
    19.Math.E : 自然数(2.718281828459045) 
    20.Math.LN2 : 2的自然对数(0.6931471805599453) 
    21.Math.LN10 : 10的自然对数(2.302585092994046) 
    22.Math.LOG2E : log 2 为底的自然数(1.4426950408889634) 
    23.Math.LOG10E : log 10 为底的自然数(0.4342944819032518) 
    24.Math.PI : π(3.141592653589793) 
    25.Math.SQRT1_2 : 1/2的平方根(0.7071067811865476) 
    26.Math.SQRT2 : 2的平方根(1.4142135623730951) 

#### 6.DOMAPI

    //document方法： 
    getElementById(id) Node 返回指定节点的引用 
    getElementsByTagName(name) NodeList 返回文档中所有匹配的元素的集合 
    createElement(name) Node 创建一个元素节点
    createTextNode(text) 创建一个纯文本结点 
    ownerDocument Document 指向这个节点所属的文档 
    documentElement Node 返回html节点 
    document.body Node 返回body节点 
    document.querySelector()
    document.querySelectorAll()
    
    
    //element方法： 
    getAttribute(attributeName) String 返回指定属性的值 
    setAttribute(attributeName,value) String 给属性赋值 
    removeAttribute(attributeName) String 移除指定属性和它的值 
    
    //node方法： 
    appendChild(child) Node 给指定结点添加一个新的子结点 
    removeChild(child) Node 移除指定结点的子结点 
    replaceChild(newChild,oldChild) Node 替换指定结点的子结点 
    insertBefore(newChild,refChild) Node 在同一层级的结点前面插入新结点 
    hasChildNodes() Boolean 如果结点有子结点则返回true 
    
    //node属性： 
    nodeName String 以字符串的格式存放结点的名称 
    nodeType String 以整型数据格式存放结点的类型 
    nodeValue String 以可用的格式存放结点的值 
    parentNode Node 指向结点的父结点的引用 
    childNodes NodeList 指向子结点的引用的集合 
    firstChild Node 指向子结点结合中的第一个子结点的引用 
    lastChild Node 指向子结点结合中的最后一个子结点的引用 
    previousSibling Node 指向前一个兄弟节点；如果这个节点就是兄弟节点，那么该值为null 
    nextSibling Node 指向后一个兄弟节点；如果这个节点就是兄弟节点，那么该值为null

#### 7.浏览器特征函数:

    //1.浏览器名称 
    //IE : "Microsoft Internet Explorer" 
    //NS : "Netscape" 
    var browserName = navigator.appName; 
    
    //2.浏览器版本 
    var browserVersion = navigator.appVersion; 
    
    //3.客户端操作系统 
    var isWin = ( navigator.userAgent.indexOf("Win") != -1 ); 
    var isMac = ( navigator.userAgent.indexOf("Mac") != -1 ); 
    var isUnix = ( navigator.userAgent.indexOf("X11") != -1 ); 
    
    //4.判断是否支持某对象,方法,属性 
    //当一个对象,方法,属性未定义时会返回undefined或null等,这些特殊值都是false 
    if( document.images ){ } 
    if( document.getElementById ){ } 
    
    //5.检查浏览器当前语言 
    if( navigator.userLanguage ){ var l = navigator.userLanguage.toUpperCase(); } 
    
    //6.检查浏览器是否支持Cookies 
    if( navigator.cookieEnabled ){ } 