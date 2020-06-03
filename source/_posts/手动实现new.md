---
title: 手动实现new
date: 2020-06-03 11:44:18
tags:
---
### new 一个构造函数，相当于实例化一个对象，总共分四步：

1. 创建一个全新的对象，即：var o = {}
2. 新对象被执行原型连接，将 o 对象的 proto 指向构造函数 Person 的原型对象(Person.prototype)
3. 将新对象绑定到构造函数调用的 this，即将 o 作为 this 调用构造函数 Person，从而设置 o 的属性和方法并初始化
4. 返回构造函数中的返回值，如果没有，则返回新对象

```bash
function _new() {
    let o = {};
    let _self = Array.from(arguments).slice(0, 1)[0];
    let _args = Array.from(arguments).slice(1);
    o.__proto__ = _self.prototype;
    _self.apply(o, _args);
    return o;
}

function Person(name, age){
    this.name = name;
    this.age = age;
}

Person.prototype.sayhi = function(){
    console.log('hi', this.name)
}

var p = _new(Person, 'lucy', 12);
p.sayhi(); // hi, lucy

```