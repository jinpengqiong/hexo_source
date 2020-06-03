---
title: toString妙用
date: 2020-06-03 17:15:28
tags:
---
```bash
//实现一个add功能
function add(a) {
    let fn = function(b) {
        a = a + b;
        return fn;
    }

    fn.toString = function() {
        return a;
    }

    return fn;
}

add(1);      // 1
add(1)(2);   // 3
add(1)(2)(3) // 6
add(1)(2)(3)(4) // 10
```

fn是一个function，类型为Object，会默认调用fn的toString方法，这个toString方法不一定返回一个字符串，本例中改写了toString方法，返回了一个数字。