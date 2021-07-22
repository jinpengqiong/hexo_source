---
title: module.exports与exports区别
date: 2021-07-22 15:18:34
tags:
---

> 用一句话来说明就是，require方能看到的只有module.exports这个对象，它是看不到exports对象的，而我们在编写模块时用到的exports对象实际上只是对module.exports的引用。

```bash
var module = {
    exports:{
        name:"我是module的exports属性"
    }
};
var exports = module.exports;  //exports是对module.exports的引用，也就是exports现在指向的内存地址和module.exports指向的内存地址是一样的

console.log(module.exports);    //  { name: '我是module的exports属性' }
console.log(exports);   //  { name: '我是module的exports属性' }


exports.name = "我想改一下名字";


console.log(module.exports);    //  { name: '我想改一下名字' }
console.log(exports);   //  { name: '我想改一下名字' }
//看到没，引用的结果就是a和b都操作同一内存地址下的数据


//这个时候我在某个文件定义了一个想导出的模块
var Circle = {
    name:"我是一个圆",
    func:function(x){
        return x*x*3.14;
    }
};

exports = Circle;  //   看清楚了，Circle这个Object在内存中指向了新的地址，所以exports也指向了这个新的地址，和原来的地址没有半毛钱关系了

console.log(module.exports);    //  { name: '我想改一下名字' }
console.log(exports);   // { name: '我是一个圆', func: [Function] }
```

回到nodejs中，module.exports初始的时候置为{}, exports也指向这个空对象。
```bash
// 这样写没问题，在同一片内存中处理同一个对象
exports.name = ()=> {
  console.log('name')
}
module.exports.age = () => {
  console.log('age')
}
// 以下写法不行，因为exports的引用变为新的内存引用
exports = {
  a : 1,
  b: 2
}
//下面的写法是可以导出去的。说句题外话，module.exports除了导出对象，函数，还可以导出所有的类型，比如字符串、数值等。
module.exports.name = {
  console.log('name')
}
```


