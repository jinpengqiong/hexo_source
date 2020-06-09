---
title: '循环语法比较以及使用场景(for, forEach, for...in, for...of)'
date: 2020-06-09 23:04:47
tags:
---

- for 按顺序遍历，遍历的对象有 length 属性
```bash
var arr = [233, 666, 2333]

for(var index = 0; index < arr.length; index++) {
    console.log(arr[index])
}
```

- forEach: for循环的缺陷在于写法比较麻烦，因此数组提供了内置的 forEach 方法
```bash
arr.forEach((val, index) => {
    console.log(index,val)
})

0 233
1 666
2 2333
```
> forEach循环的缺陷是无法中途跳出循环，break或return都不能奏效
 - for...in 语句主要是为遍历对象而设计的，可以用来遍历对象的所有属性名，也会遍历出原型链上的成员属性；属性名出现的顺序是不确定的

 实现只遍历自身属性：
 ```bash
for(let prop in obj) {
    if (obj.hasOwnProperty(prop)) {
        //...
    }
}
 ```
for...in 循环缺点：
- 数组的键名是数字，但是 for...in 循环是以字符串作为键名"0", "1", "2"等
- for...in循环不仅遍历数字键名，还会遍历手动添加的其它键，包括原型链上的键
- 某些情况下，for...in循环会以任意顺序遍历键名

> 其实for...in在遍历对象属性时，也并不是以任意顺序遍历的，整体上是数字类型的属性会先输出，升序排序，字符串属性按书写的顺序输出

```bash
var obj = {};
obj[100] = '100'
obj[1] = '1'
obj['B'] = 'B'
obj['A'] = 'A'
obj['C'] = 'C'
obj[5] = '5'
obj[101] = '101'

for(key in obj) {
    console.log(`key=${key}, value=${obj[key]}`)
}

key=1, value=1
key=5, value=5
key=100, value=100
key=101, value=101
key=B, value=B
key=A, value=A
key=C, value=C
```

- for...of
```bash
  ES6引入了for...of循环，作为遍历所有数据结构的统一的方法；

  一个数据结构部署了 Symbol.iterator 属性，就被视为具有 iterator 接口，就可以用 for...of 循环遍历成员

  for...of 循环适用范围：数组、Set和Map结构、类数组对象、字符串等;

```
for...of 特点：
```bash
var arr = [3,5,7]
arr.bar = "hello, world"

for(let i in arr) {
    console.log(typeof i) // '0' '1' '2' 'bar'
}

for(let i of arr) {
    console.log(i) // 3 5 7
}
```

```bash
var arr = [3,5,7]
arr.bar = "hello, world"

for(let i in arr) {
    console.log(typeof i) // '0' '1' '2' 'bar'
}

for(let i of arr) {
    console.log(i) // 3 5 7
}
```


