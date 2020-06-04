---
title: event loop
date: 2020-06-04 18:01:11
tags:
---
- 微任务 promise  process.nextTick
- 宏任务 setTimeout  setInterval  I/O  script
- 同一次事件循环中  微任务永远在宏任务之前执行
 ``` bash
console.log(1)
setTimeout(function() {
  console.log(2)
}, 0);
const intervalId = setInterval(function() {
  console.log(3)
}, 0)
setTimeout(function() {
  console.log(10)
  new Promise(function(resolve) {
    console.log(11)
    resolve()
  })
  .then(function() {
    console.log(12)
  })
  .then(function() {
    console.log(13)
    clearInterval(intervalId)
  })
}, 0);

Promise.resolve()
  .then(function() {
    console.log(7)
  })
  .then(function() {
    console.log(8)
  })
console.log(9)
 ```

1. 第一轮事件循环流程：
- 整体script作为第一个宏任务进入主线程，遇到console.log,输出1
- 遇到setTimeout, 其回调函数被分发到宏任务Event Queue中，记为setTimeout1，
- 遇到setIntrval，其回调函数被分发到宏任务Event Queue中，记为setInterval1，
- 遇到setTimeout，其回调函数被分发到宏任务Event Queue中，记为setTimeout2，
- 遇到Promise.resolve，then被分发到微任务Event Queue中，记为then1
- 遇到console.log，输出9

此时的Event Queue：

宏任务 | 微任务
---|:---:
setTimeout1 | then1
setInterval1 |
setTimeout2 |

- 上表是第一轮事件循环宏任务结束时各Event Queue的情况，此时已经输出了1和9
继续执行微任务，执行then1，输出7，8




> 第一轮事件循环正式结束，输出结果是1，9，7，8



2. 第二轮事件循环从setTimeout1开始,首先输出2，此时没有微任务，继续执行下一个宏任务


3. 第三轮事件循环从setInterval1开始, 输出3，此时没有微任务，继续执行下一个宏任务



> 前三轮输出结果为1，9，7，8，2，3



4. 第四轮事件循环从setTimeout2开始

- 首先输出10，遇到了promise，首先输出 11
- then被分发到微任务Event Queue中，记为then2




任务类型 | 任务名称
---|:---
微任务 | then2

- 继续执行微任务then2，输出12，13，setInterval被清除




> 最终输出结果为1，9，7，8，2，3，10，11，12，13