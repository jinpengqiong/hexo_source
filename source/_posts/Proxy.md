---
title: Proxy
date: 2020-06-05 18:35:53
tags:
---
#### Proxy用于修改某些操作的默认行为，可以理解为，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截.

> Vue3.0中采用Proxy代替Vue2.0中的Object.defineProperty进行数据劫持

```bash
var obj = new Proxy({}, {
    get: function(target, property) {
        if (property in target) {
            return target[property];
        } else {
            throw new ReferenceError(`Property ${property} doesn't exist!`)
        }
    },
    set: function(obj, prop, value) {
        if (prop === 'age') {
            if (!Number.isInteger(value)) {
                throw new TypeError('not an integer')
            }
            if (value > 200){
                throw new RangeError('invalid input')
            }
            obj[prop] = value;
        }
        obj[prop] = value; // 挂载其它属性
    }
})

obj.age = 100;
obj.name = 'alice'
for(let key in obj) {
    if (obj.hasOwnProperty(key)) {
        console.log(key,'=',obj[key])
    }
}

age = 100
name = alice
```