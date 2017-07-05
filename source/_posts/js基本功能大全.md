---
title: js基本功能大全
date: 2017-07-05 21:54:04
tags: [javascript]
categories: 前端
---

基本类型与引用类型的区别
1.基本类型： string,number,boolean,null,undefined;操作和保存在变量的实际的值。
2.引用类型： Function,Array,Object;值保存在内存中，js不允许直接访问内存，在操作的时候，操作的是对象的引用。

<!--more-->
#### 1.javascript的数组API

    //定义数组 
    var arr = new Array();  
    
    //数组长度 
    pageIds.length; 
    
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

#### 2.dom最常用API

    //document方法： 
    getElementById(id) Node 返回指定节点的引用 
    getElementsByTagName(name) NodeList 返回文档中所有匹配的元素的集合 
    createElement(name) Node 创建一个元素节点
    createTextNode(text) 创建一个纯文本结点 
    ownerDocument Document 指向这个节点所属的文档 
    documentElement Node 返回html节点 
    document.body Node 返回body节点 
    
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

#### 3.创建一个map对象:

    function HashMap() { 
        /** Map 大小 **/ 
        var size = 0; 
        /** 对象 **/ 
        var entry = new Object(); 
        /** 存 **/ 
        this.put = function (key , value) { 
            if(!this.containsKey(key)) { 
                size ++ ; 
            } 
            entry[key] = value; 
        } 
        /** 取 **/ 
        this.get = function (key) { 
            return this.containsKey(key) ? entry[key] : null; 
        } 
        /** 删除 **/ 
        this.remove = function ( key ) { 
            if( this.containsKey(key) && ( delete entry[key] ) ) { 
                size --; 
            } 
        } 
        /** 是否包含 Key **/ 
        this.containsKey = function ( key ) { 
            return (key in entry); 
        } 
        /** 是否包含 Value **/ 
        this.containsValue = function ( value )     { 
            for(var prop in entry)  { 
                if(entry[prop] == value)    { 
                    return true; 
                } 
            } 
            return false; 
        } 
        /** 所有 Value **/ 
        this.values = function () { 
            var values = new Array(); 
            for(var prop in entry) { 
                values.push(entry[prop]); 
            } 
            return values; 
        } 
        /** 所有 Key **/ 
        this.keys = function () { 
            var keys = new Array(); 
            for(var prop in entry) { 
                keys.push(prop); 
            } 
            return keys;   
        } 
        /** Map Size **/ 
        this.size = function () { 
            return size; 
        } 
        /* 清空 */ 
        this.clear = function () { 
            size = 0; 
            entry = new Object(); 
        } 
    } 
    var map = new HashMap(); 
    /* 
        map.put("A","1"); 
        map.put("B","2"); 
        map.put("A","5"); 
    */ 
    /* 
        alert(map.containsKey("XX")); 
        alert(map.size()); 
        alert(map.get("A")); 
        alert(map.get("XX")); 
        map.remove("A"); 
        alert(map.size()); 
        alert(map.get("A")); 
    */ 
    /** 同时也可以把对象作为 Key **/ 
    /* 
        var arrayKey = new Array("1","2","3","4"); 
        var arrayValue = new Array("A","B","C","D"); 
        map.put(arrayKey,arrayValue); 
        var value = map.get(arrayKey); 
        for(var i = 0 ; i < value.length ; i++) { 
            //alert(value[i]); 
        } 
    */ 
    /** 把对象做为Key时，自动调用了该对象的toString()方法其实最终还是以String对象为Key**/ 
    /** 如果是自定义对象 那自己得重写 toString() 方法 否则就是下面的结果 **/ 
    function MyObject(name){ 
        this.name = name; 
    } 
    /** 
    function MyObject(name) { 
        this.name = name; 
        this.toString = function () { 
            return this.name; 
        } 
    } 
    **/ 
    var object1 = new MyObject("小张"); 
    var object2 = new MyObject("小名"); 
    map.put(object1,"小张"); 
    map.put(object2,"小名"); 
    alert(map.get(object1)); 
    alert(map.get(object2)); 
    map.remove("xxxxx"); 
    alert(map.size()); 
    /** 运行结果 小名 小名 size = 1 **/ 
    /** 如果改成复写toString()方法的对象 , 效果就完全不一样了 **/ 

#### 4.常用的数字函数:

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

#### 5.js堆栈:

    function stack(){ 
        if(this.top==undefined){ 
            //初始化堆栈的顶部指针和数据存放域 
            this.top=0; 
            this.unit=new Array(); 
        } 
        this.push=function(pushvalue){ 
            //定义压入堆栈的方法 
            this.unit[this.top]=pushvalue; 
            this.top+=1; 
        } 
        this.readAllElements=function(){ 
            //定义读取所有数据的方法 
            if(this.top==0){ 
                alert("当前栈空，无法读取数据"); 
                return(""); 
            } 
            var count=0; 
            var outStr=""; 
            for(count=0;count<this.top;count++){ 
                outStr+=this.unit[count]+","; 
            } 
            return(outStr); 
        } 
        this.pop=function(){ 
            //定义弹出堆栈的方法 
            if(this.top==0){ 
                alert("当前栈空，无法弹出数据"); 
                return(""); 
            } 
            var popTo=this.unit[this.top-1]; 
            this.top--; 
            return(popTo); 
        /* 从堆栈弹出数据，顶部指针减一，不过这里没有做到资源的释放，也 
        就是说数据仍然存在于this.unit的数组中，只不过无法访问罢了。目前 
        我也没想到好的办法解决。*/ 
        } 
    } 

#### 6.JavaScript日期函数:

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

#### 7.最常用字符串函数API:

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
    
#### 8.数学函数:

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

#### 9.浏览器特征函数:

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

#### 10.JavaScript面向对象的方法实现继承:call方法

    // 动物类 animal 
    function animal(bSex){ 
        this.sex = bSex 
        this.getSex = function(){ 
            return this.sex 
        } 
    } 
    // 类静态变量 (如果你不修改它的话～～) 
    animal.SEX_G = new Object(); // 雌性 
    animal.SEX_B = new Object(); // 雄性 
    // 动物子类 鸟 
    function bird(bSex){ 
        animal.call(this, bSex); 
        this.fly = function(iSpeed){ 
            alert("飞行时速高达 " + iSpeed); 
        } 
    } 
    // 动物子类 鱼 
    function fish(bSex){ 
        animal.call(this, bSex); 
        this.swim = function(iSpeed){ 
            alert("游动时速高达 " + iSpeed) 
        } 
    } 
    // 鱼 鸟 杂交品种。。。 
    function crossBF(bSex){ 
        bird.call(this, bSex); 
        fish.call(this, bSex); 
    } 
    var oPet = new crossBF(animal.SEX_G); // 雌性 鱼鸟 
    alert(oPet.getSex() == animal.SEX_G ? "雌性" : "雄性"); 
    oPet.fly(124) 
    oPet.swim(254) 

#### 11.用面向对象的编程方式写JavaScript:

    MyTool = new function(){ 
        /** 
        * 返回非空字符串,如果有默认值就返回默认字符串. 
        */ 
        this.notNull = function(str,defaultStr){ 
            if(typeof(str)=="undefined"||str==null||str==''){ 
                if(defaultStr) {
                    return defaultStr; 
                } else {
                    return ''; 
                }
            } else{ 
                return str; 
            } 
        } 
    } 
    rootId = MyTool.notNull(rootId,'001000'); 

#### 12.常用的js方法,包括表单校验的一些方法,下拉菜单常用的方法等等:

    /** 
    * 对JSON对象转换为字符串. 
    * @param {json对象} json 
    * @return {json字符串} 
    */ 
    function jsonObj2Str(json) { 
        var str = "{"; 
        for (prop in json) { 
            str += prop + ":" + json[prop] + ","; 
        } 
        str = str.substr(0, str.length - 1); 
        str += "}"; 
        return str; 
    } 
    /** 
    * 将json字符串转换为json对象. 
    * @param {json字符串} jsonstr 
    * @return {json对象} 
    */ 
    function jsonStr2Obj(jsonstr) { 
        return eval("("+jsonstr+")"); 
    } 
    /** 
    * 得到一个元素的left坐标值. 
    * @param {dom对象} obj 
    * @return {位置值} 
    */ 
    function getLeft(obj){ 
        var offset=e.offsetLeft; 
        if(e.offsetParent!=null){
            offset+=getLeft(e.offsetParent); 
        } 
        return offset; 
    } 
    /** 
    * 得到一个元素的绝对位置的top坐标值. 
    * @param {dom对象} obj 
    * @return {位置值} 
    */ 
    function getTop(obj){ 
        var offset=e.offsetTop; 
        if(e.offsetParent!=null) {
            offset+=getTop(e.offsetParent); 
        }
        return offset; 
    } 
    /** 
    * 删除一个字符串的左右空格. 
    * @param {原始字符串} str 
    * @return {删除空格之后的字符串} 
    */ 
    function trim(str) { 
        return str.replace(/(^\s*)|(\s*$)/g,""); 
    } 
    /** 
    * 根据id取出一个元素. 
    * @param {元素id值} str 
    * @return {dom对象} 
    */ 
    function $(str) { 
        return document.getElementById(str); 
    } 
    /** 
    * 按name获取一个对象. 
    * @param {元素name值} str 
    * @return {根据name返回的第一个对象} 
    */ 
    function $byName(str) { 
        var arr = document.getElementsByName(str); 
        if (arr) {
            return arr[0]; 
        }else {
            return null; 
        } 
    } 
    /***************以下方法和表单验证相关*************************************************/ 
    /** 
    * 返回非空字符串,如果有默认值就返回默认字符串. 
    * @param {要进行转换的原字符串} str 
    * @param {默认值} defaultStr 
    * @return {返回结果} 
    */ 
    function notNull(str, defaultStr) { 
        if (typeof(str) == "undefined" || str == null || str == '') { 
            if (defaultStr) {
                return defaultStr; 
            }else{ 
                return '';
            } 
        } else { 
            return str; 
        } 
    } 
    /** 
    * 比较两个日期大小. 
    * @param {较小日期的文本框id} smallDate 
    * @param {较大日期的文本框id} bigDate 
    * @param {出错的提示信息} msg 
    */ 
    function compareTwoDate(smallDate, bigDate, msg) { 
        var v1 = $(smallDate).value; 
        var v2 = $(bigDate).value; 
        if (v1 >= v2) { 
            alert(msg); 
            v2.focus(); 
            return false; 
        } 
        return true; 
    } 
    /** 
    * 比较两个金额大小的方法. 
    * @param {较小的金额} smallNum 
    * @param {较大的金额} bigNum 
    * @param {出错提示信息} msg 
    * @return {Boolean} 
    */ 
    function compareTwoNum(smallNum, bigNum, msg) { 
        var v1 = $(smallNum).value; 
        var v2 = $(bigNum).value; 
        if (parseFloat(v1) >= parseFloat(v2)) { 
            alert(msg); 
            v2.focus(); 
            return false; 
        } 
        return true; 
    } 
    /** 
    * 检查文本框的长度是否超出指定长度. 
    * @param {文本id} textId 
    * @param {文本框的最大长度} len 
    * @param {文本框描述内容} msg 
    * @return {有错就返回false,否则返回true} 
    */ 
    function checkLength(textId, len, msg) { 
        obj = $(textId); 
        str = obj.value; 
        str = str.replace(/[^\x00-\xff]/g, "**"); 
        realLen = str.length; 
        if (realLen > len) { 
            alert("[" + msg + "]" + "长度最大为" + len + "位," + "请重新输入！\n注意：一个汉字占2位。"); 
            obj.focus(); 
            return false; 
        } else {
            return true;
        }
    } 
    /** 
    * 判断某个文本框不可以为空. 
    * @param {文本框id} textId 
    * @param {文本框描述内容} msg 
    * @return {有错就返回false,否则返回true} 
    */ 
    function checkIfEmpty(textId, msg) { 
        var textObj = $(textId); 
        var textValue = textObj.value; 
        if (trim(textValue) == '') { 
            alert('[' + msg + ']不得为空！'); 
            textObj.focus(); 
            return false; 
        } else { 
            return true; 
        } 
    } 
    /** 
    * 判断指定文本框内容必须为邮件. 
    * @param {文本框id} textId 
    * @param {文本框描述} msg 
    * @return {如果是邮件内容就返回true否则返回false} 
    */ 
    function checkIsMail(textId, msg) { 
        var obj = $(textId); 
        if (!_isEmail(obj.value)) { 
            alert('[' + msg + ']不是合法的邮件地址！'); 
            obj.focus(); 
            return false;   
        } else 
        return true; 
    } 
    /** 
    * 验证是不是邮件. 
    * @param {要验证的字符串} strEmail 
    * @return {Boolean} 
    */ 
    function _isEmail(strEmail) { 
        //接下来的验证是否有两个以上的‘.'号，有的话就是错的！ 
        var first = strEmail.indexOf('.'); 
        if (strEmail.indexOf('@')== -1) { 
            return false; 
        } 
        var tempStr = strEmail.substring(first + 1); 
        if (tempStr.indexOf('.') != -1) { 
            return false; 
        } 
        if (strEmail 
        .search(/^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/) != -1) { 
            return true; 
        } else {
            return false;        
        }
    } 
    /** 
    * 判断某个文本框是否数字. 
    * @param {文本框id} textId 
    * @param {文本框描述内容} msg 
    * @return {Boolean} 
    */ 
    function checkIsNum(textId, msg) { 
        obj = $(textId); 
        if (isNaN(obj.value)) { 
            alert('[' + msg + ']必须为数字。'); 
            obj.focus(); 
            return false; 
        } else {
            return true;        
        }
    } 
    /** 
    * 判断某个文本框是否含有非法字符. 
    * @param {文本框的id} textId 
    * @param {文本框描述内容} msg 
    * @return {有错就返回false否则返回true} 
    */ 
    function checkIsValid(textId, msg) { 
        obj = $(textId); 
        if (!_isValidString(obj.value, '[' + msg + ']不得含有非法字符。')) { 
            obj.focus(); 
            return false; 
        } 
        return true; 
    } 
    /** 
    * 判断是不是合法字符串. 
    * @param {要进行判断的字符串} szStr 
    * @param {文本描述} errMsg 
    * @return {合法则返回true否则返回false} 
    */ 
    function _isValidString(szStr,errMsg) { 
        voidChar = "'\"><`~!@#$%^&\(\)（）！￥……？?“”‘'*"; 
        for (var i = 0; i < voidChar.length; i++) { 
            aChar = voidChar.substring(i, i + 1); 
            if (szStr.indexOf(aChar) > -1){ 
                alert(errMsg) 
                return false; 
            } 
        } 
        return true; 
    } 
    /*************** 以下方法和下拉菜单相关*************************************************/ 
    /** 
    * 控制下拉菜单不可以为-1(未选择情况value=-1) 
    * @param {下拉菜单id} selectId 
    * @param {下拉菜单描述内容} msg 
    * @param {下拉菜单的空值对应的value,默认为-1} nullValue 
    * @return {Boolean} 
    */ 
    function checkChooseSelect(selectId, msg ,nullValue) { 
        var obj = $(selectId); 
        if (obj.value == notNull(nullValue,'-1')) { 
            alert('[' + msg + ']必选!'); 
            obj.focus(); 
            return false; 
        }
        return true; 
    } 
    /** 
    * 得到下拉菜单的显示的文字. 
    * @param {下拉菜单dom对象} selectObj 
    * @return {返回下拉菜单的显示的"文本"} 
    */ 
    function getSelectText(selectObj) { 
        return selectObj.options[selectObj.selectedIndex].text; 
    } 
    /** 
    * 得到下拉菜单的显示的值. 
    * @param {下拉菜单dom对象} selectObj 
    * @return {得到下拉菜单的显示的"值"} 
    */ 
    function getSelectValue(selectObj) { 
        return selectObj.options[selectObj.selectedIndex].value; 
    } 
    /** 
    * 设置下拉菜单的选择状态到指定的值. 
    * @param {下拉菜单对象} obj 
    * @param {要选择的值} value 
    */ 
    function setSelectValue(obj, value) { 
        /*
        for (i = obj.options.length - 1; i >= 0; i--) { 
            if (obj.options[i].value == value) { 
                obj.options[i].selected = true; 
                return; 
            } 
        } 
        */ 
        obj.value= value; 
    } 
    /** 
    * 根据键值串的内容进行下拉菜单的动态组装 
    * @param {要进行下拉菜单组装的dom对象} obj 
    * @param {键值对用,和;分割,例如'1,男;2,女;3,未知'} valAndText 
    */ 
    function setSelectContent(obj,valAndText){ 
        if(trim(valAndText)==''){ 
            alert('没有要进行组装下拉菜单的数据!'); 
            return false; 
        } 
        clearSelect(obj); 
        var keyandvalues = valAndText.split(';'); 
        for(var i=0;i<keyandvalues.length;i++){ 
            var arr = keyandvalues[i].split(','); 
            if(arr){ 
                var value =arr[0]; 
                var text =arr[1]; 
                var objOption = new Option(text,value); 
                obj.add(objOption); 
            } 
        } 
    } 
    /** 
    * 清空下拉菜单里面的内容. 
    * @param {下拉菜单对象} obj 
    */ 
    function clearSelect(obj) { 
        for (var i=obj.options.length; i >0; i--) { 
            obj.remove(0); 
        } 
    } 
    /*************** 以下方法和多选框相关*************************************************/ 
    /** 
    * 返回选中的checks的id组成的字符串,逗号隔开. 
    * @param {checks数组} checks 
    * @return 选择的id组成的字符串 
    */ 
    function getCheckedIds(checks){ 
        var selectedValue = ''; 
        var len = checks.length; 
        for(var index=0; index<len; index++) { 
            if(checks[index].checked==true) { 
                selectedValue += checks[index].value+","; 
            } 
        } 
        if(selectedValue.length>0) {
            return selectedValue.substring(0,selectedValue.length-1); 
        }
        return selectedValue; 
    } 

    //下面的代码放到html标签里，并在head里调用上面的js
    <HEAD>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <!--<<<<<<<<<<<调用上面的js>>>>>>>>>-->
        <SCRIPT LANGUAGE="JavaScript"> 
            <!-- 
                /** 
                * 表单验证的示例js方法. 
                */ 
                function check(){ 
                    if(checkIfEmpty('a','非空校验') 
                    &&checkIsMail('b','邮箱校验') 
                    &&checkIsNum('c','数字校验') 
                    &&checkIsValid('d','合法性校验') 
                    &&compareTwoDate('e','f','小日期与大日期关系错误!') 
                    &&checkLength('g',5,'长度校验') 
                    &&checkChooseSelect('h','下拉菜单非空','-1') 
                    &&compareTwoNum('k','l','大小数目关系不正确!')){ 
                        alert('校验通过!'); 
                        return true; 
                    }else{ 
                        return false; 
                    } 
                } 
                /** 
                * 取下拉菜单的值和文本的示例js方法. 
                */ 
                function getSelect(){ 
                    var sss = $('h'); 
                    alert('下拉菜单选择的文本是:'+getSelectText(sss)+'\n' 
                    +'下拉菜单选择的值是:'+getSelectValue(sss)); 
                } 
                /** 
                * 根据键值字符串设置下拉菜单的显示内容. 
                */ 
                function setSelect(){ 
                    var sss = $('i').value; 
                    setSelectContent($('h'),sss); 
                } 
                /** 
                * 返回多选框数组选择状态的id的字符串,结果以逗号隔开. 
                */ 
                function getMulti(){ 
                    alert('多选选择的id是:'+getCheckedIds(document.getElementsByName('j'))); 
                } 
            //--> 
        </SCRIPT>
    </HEAD>
    <BODY>
        <table>
          <tr>
            <td> 非空:
              <input id='a'></td>
            <td> checkIfEmpty('a','非空校验') </td>
          </tr>
          <tr>
            <td> 邮箱:
              <input id='b' value='323232@2323.com'></td>
            <td> checkIsMail('b','邮箱校验') </td>
          </tr>
          <tr>
            <td> 数字:
              <input id='c' value='aaaa'></td>
            <td> checkIsNum('c','数字校验') </td>
          </tr>
          <tr>
            <td> 合法字符:
              <input id='d' value='@$@$#$#!%%#'></td>
            <td> checkIsValid('d','合法性校验') </td>
          </tr>
          <tr>
            <td> 小的日期:
              <input id='e' value='2010-1-1'>
              大的日期:
              <input id='f' value='2011-1-1'></td>
            <td> compareTwoDate('e','f','小日期与大日期关系错误!') </td>
          </tr>
          <tr>
            <td> 小的数:
              <input id='k' value='12.3'>
              大的数:
              <input id='l' value='4564'></td>
            <td> compareTwoNum('k','l','大小数目关系不正确!') </td>
          </tr>
          <tr>
            <td> 字符长度校验(<5):
              <input id='g'></td>
            <td> checkLength('g',5,'长度校验') </td>
          </tr>
          <tr>
            <td> 下拉菜单非空校验:
              <select id='h'>
                <option value='-1'> 请选择 </option>
                <option value='1'> 立项 </option>
                <option value='2'> 可研 </option>
              </select></td>
            <td> checkChooseSelect('h','下拉菜单非空','-1') </td>
          </tr>
          <tr>
            <td colspan='2'><button onclick='check()'> 测试表单校验方法 </button></td>
          </tr>
          <tr>
            <td><button onclick='getSelect()'> 得到下拉菜单的值 </button></td>
            <td> getSelectText(sss)和getSelectValue(sss) </td>
          </tr>
          <tr>
            <td> 输入下拉菜单的键值字符串(如右所示)
              <input id='i' value='1,男;2,女;3,未知'>
              <button onclick='setSelect()'> 设置下拉菜单的值 </button></td>
            <td> setSelectContent($('h'),sss) </td>
          </tr>
          <tr>
            <td><input type='checkbox' name='j' value='aaa1'>
              <input type='checkbox' name='j' value='aaa2'>
              <input type='checkbox' name='j' value='aaa3'>
              <input type='checkbox' name='j' value='aaa4'>
              <button onclick='getMulti()'> 得到多选选择的id </button></td>
            <td> getCheckedIds(document.getElementsByName('j')) </td>
          </tr>
        </table>    
    </BODY>