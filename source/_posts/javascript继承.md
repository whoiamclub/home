---
title: javascript继承
date: 2017-07-10 13:33:15
tags: [javascript]
categories: 前端
---
许多OO语言都支持两种继承方式：接口继承和实现继承。EMCAScript只支持实现继承，其实现继承主要是依靠原型链来实现的。
<!-- more -->
#### 1.组合继承
    
    function SuperType(name){
        this.name = name;
        this.colors = ["red"];
    }
    SuperType.prototype.sayName = function(){
        alert(this.name)
    }
    function SubType(name,age){
        SuperType.call(this.name)
        this.age = age;
    }
    SubType.prototype = new SuperType();
    SubType.prototype.constructor = SubType;
    SubType.prototype.sayAge = function(){
        alert(this.age)
    }
    //创建原型对象
    //增强对象，添加constructor属性
    //指定原型，使用新创建的原型对象
#### 2.原型式继承
Object.create()规范化原型继承。这个方法接受两个参数：一个是用作新对象原型的对象，一个是为新对象定义额外属性的对象。

#### 3.深度克隆
浅度克隆：原始类型为值传递，对象类型仍为引用传递。
深度克隆：所有元素或属性均完全复制，与原对象完全脱离，也就是说所有对于新对象的修改都不会反映到原对象中。
    
    //深度克隆
    Object.prototype.clone=function(){
        //原型指向保持一致
        var newobj=Object.create(Object.getPrototypeOf(this));
        //自身属性保持一样
        var propNames=Object.getOwnPropertyNames(this);
        propNames.forEach(function(item){
           //保持每个属性的特性也一样
           var des=Object.getOwnPropertyDescriptor(this,item);
           Object.defineProperty(newobj,item,des);
        },this);
        return newobj;
    }
    注解：
    Object.getPrototypeOf(this)
    //返回值：给定对象的原型。如果没有继承属性，则返回 null 。
    //在 ES5 中，如果参数不是一个对象类型，将抛出一个  TypeError 异常。在 ES6 /ES2015中，参数被强制转换为一个 Object。
    
    Object.create(proto);
    //proto：新创建的对象的原型
    //返回值：使用指定的原型对象和其属性创建了一个新的对象。
    
    Object.getOwnPropertyNames(this);
    //返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名。
    
    Object.getOwnPropertyDescriptor(obj, prop)
    //obj：想要查看属性的对象；prop：将返回对应属性描述符的属性名称
    //返回对象指定的属性配置。
    
     Object.defineProperty(newobj,item,des);
     //obj：要在其上定义属性的对象。prop：要定义或修改的属性的名称。descriptor：将被定义或修改的属性的描述符。
     //会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。
     
     //IE兼容forEach方法
     //https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/forEach  
        if (!Array.prototype.forEach) {  
           Array.prototype.forEach = function(callback, thisArg) {  
               var T, k;  
               if (this == null) {  
                   throw new TypeError(" this is null or not defined");  
               }  
               var O = Object(this);  
               var len = O.length >>> 0; // Hack to convert O.length to a UInt32  
               if ({}.toString.call(callback) != "[object Function]") {  
                   throw new TypeError(callback + " is not a function");  
               }  
               if (thisArg) {  
                   T = thisArg;  
               }  
               k = 0;  
               while (k < len) {  
                   var kValue;  
                   if (k in O) {  
                       kValue = O[k];  
                       callback.call(T, kValue, k, O);  
                   }  
                   k++;  
               }  
           };  
        } 