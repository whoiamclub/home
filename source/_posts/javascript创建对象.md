---
title: javascript创建对象
date: 2017-07-10 09:34:07
tags: [javascript]
categories: 前端
---

Object构造函数或对象字面量都可以用来创造单个对象，但这些方式有个明显的缺点：使用同一个接口创建很多对象，会产生大量重复代码。

#### 1.工厂模式
<!-- more -->

    function createPerson(name,age,job){
        var o = new Object();
        o.name = name;
        o.age = age;
        o.job = job;
        o.sayName = function(){
            alert(this.name)
        }
        return o;
    }
    
    var person1 = createPerson("tom",11,"student")
#### 2.构造函数模式
    
    function Person(name,age,job){
        this.name = name;
        this.age = age;
        this.job = job;
        this.sayName = function(){
            alert(this.name)
        }
    }
    var person1 =new Person("tom",11,"student")
    //或者
    var person2 = new Object();
    Person.call(person2,"Sam",11,"student")
#### 3.原型模式
    
    function Person(){
        
    } 
    Person.prototype.name = "hello";
    Person.prototype.sayName = function(){
        alert(this.name);
    }
    
    var person1 = new Person(）;
    person1.age = 11;
Person.prototype.constructor = Person;
person1.constructor = Person;
person1._proto_ = Person.prototype;
Person.prototype.isPrototype(person1); //true
Object.getPrototypeOf(person1) == Person.prototype; // true
person1.hasOwnProperty("name"); //false
"name" in person1; //true
Object.keys(Person.prototype); //["name","sayName"]
Object.keys(person1); //["age"]
Object.getOwnPropertyNames(Person.prototype); //["constructor","name","sayName"]
person1 instanceof Person; //true
//重写原型对象切断了现有原型与任何之前已经存在的对象实例之间的联系。他们引用的仍然是最初的原型。
#### 4.组合使用构造函数模式和原型模式
    
    function Person(){
        this.name = name;
        this.friends = ["tom","sam"]
    }
    Person.prototype = {
        constructor:Person,
        sayName:function(){
            alert(this.name)
        }
    }
#### 5.动态原型模式

        function Person(){
            this.name = name;
            if(typeof this.sayName != "function"){
                Person.prototype.sayName = function(){
                    alert(this.name)
                }
            }
        }
#### 6.寄生构造函数模式

    function SpecialArray(){
        var val = new Array();
        val.push.apply(val,arguments)
        val.toPipedString = function () {
            return this.join('|');
        }
        return val
    }

    

        

