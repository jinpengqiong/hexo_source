---
title: mouseover和mouseenter的区别
date: 2020-05-09 16:56:36
tags:
---
mouseover：当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡过程。对应的移除事件是mouseout

mouseenter:当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会冒泡，对应的移除事件是mouseleave

mouseover和mouseenter的异同体现在两个方面：

1. 是否支持冒泡

2. 事件的触发时机

先看一张图，对这两件事有一个简单直观的感受。

![img1](http://image.mzliaoba.com/pic/chatroom/2562048239/20200509/a0ec9a3a-56ab-4712-9b74-0ded2a9f60761670358-20190918160838058-597135305.png)

mouseenter事件的情况：

当鼠标从元素的边界之外移入元素的边界之内时，事件被触发。而鼠标本身在元素边界内时，要触发该事件，必须先将鼠标移出元素边界外，再次移入才能触发。

也就是说：mouseover支持事件冒泡，而mouseenter不支持事件冒泡



由于mouseenter不支持事件冒泡，导致在一个元素的子元素上进入或离开的时候会触发其mouseover和mouseout事件，但不会触发mouseenter和mouseleave事件。

如何模拟mouseenter事件



可见mouseover事件因其具有冒泡的性质，在子元素内移动的时候，频繁被触发，如果我们不希望如此，可以使用mouseenter事件代替之，但是早期只有ie浏览器支持该事件，虽然现在大多数高级浏览器都支持了mouseenter事件，但是难免会有些兼容问题，所以如果可以自己手动模拟，那就太好了。