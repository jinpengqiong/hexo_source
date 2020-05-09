---
title: javascript 中事件冒泡和事件捕获机制
date: 2020-05-09 23:14:33
tags:
---
### 什么是事件？
事件是文档和浏览器窗口中发生的特定的交互瞬间。 事件是javascript应用跳动的心脏，也是把所有东西黏在一起的胶水，当我们与浏览器中web页面进行某些类型的交互时，事件就发生了。

 事件可能是用户在某些内容上的点击，鼠标经过某个特定元素或按下键盘上的某些按键，事件还可能是web浏览器中发生的事情，比如说某个web页面加载完成，或者是用户滚动窗口或改变窗口大小。

 ### 什么是事件流
 事件流描述的是从页面中接受事件的顺序，但有意思的是，微软（IE）和网景（Netscape）开发团队居然提出了两个截然相反的事件流概念，IE的事件流是事件冒泡流(event bubbling)，而Netscape的事件流是事件捕获流(event capturing)。

 - 事件冒泡

IE提出的事件流叫做事件冒泡，即事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点。

- 事件捕获
网景公司提出的事件流叫事件捕获流。

事件捕获流的思想是不太具体的DOM节点应该更早接收到事件，而最具体的节点应该最后接收到事件，针对上面同样的例子，点击按钮，那么此时click事件会按照这样传播：（下面我们就借用addEventListener的第三个参数来模拟事件捕获流）

### DOM事件流
‘DOM2级事件’规定的事件流包含3个阶段，事件捕获阶段、处于目标阶段、事件冒泡阶段。首先发生的事件捕获为截获事件提供机会，然后是实际的目标接收事件，最后一个阶段是事件冒泡阶段，可以在这个阶段对事件做出响应。

在DOM事件流中，事件的目标在捕获阶段不会接收到事件，这意味着在捕获阶段事件从document到<p>就停止了，下个阶段是处于目标阶段，于是事件在<p>上发生，并在事件处理中被看成冒泡阶段的一部分，然后，冒泡阶段发生，事件又传播回document。

![img1](http://image.mzliaoba.com/pic/chatroom/2562048239/20200509/abe04323-b8ba-4eef-8963-ef6691cd590f1174211-20171201225153933-1205737719.png)

### 关于DOM 2级事件处理程序
DOM 2级事件定义了两方法：用于处理添加事件和删除事件的操作： 添加事件 addEventListener()     删除事件  removeEventListener()

所有DOM节点中都包含这两个方法，并且他们都包含3个参数： （1） 要处理的事件方式（例如：click，mouseover,dbclick.....） （2）事件处理的函数，可以为匿名函数，也可以为命名函数（但如果需要删除事件，必须是命名函数） （3）一个布尔值，代表是处于事件冒泡阶段处理还是事件捕获阶段（true：表示在捕获阶段调用事件处理程序；false:表示在冒泡阶段调用事件处理程序）

使用DOM 2级事件处理程序的主要好处是可以添加多个事件处理程序，事件处理会按照他们的顺序触发，通过addEventListener添加的事件只能用removeEventListener来移除，移除时传入的参数与添加时使用的参数必须相同，这也意味着添加的匿名函数将无法移除，（注意：我们默认的第三个参数都是默认false,是指在冒泡阶段添加，大多数情况下，都是将事件处理程序添加到事件的冒泡阶段，这样可以最大限度的兼容各个浏览器）
```bash
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-">
  <title>Document</title>
  <style>
    #outer {
      text-align: center;
      width: px;
      height: px;
      background-color: #ccc;
      margin: auto;
    }

    #middle {
      width: px;
      height: px;
      background-color: purple;
      margin: auto;
    }

    #inner {
      width: px;
      height: px;
      background-color: lightblue;
      margin: auto;
      border-rad
    }
  </style>
</head>

<body>
  <div id='outer'>
    <span>outer</span>
    <div id='middle'>
      <span>middle</span>
      <div id='inner'>
        <span>inner</span>
      </div>
    </div>
  </div>
  <script>
    function $(element) {
      return document.getElementById(element);
    }
    function on(element, event_name, handler, use_capture) {
      if (addEventListener) {
        $(element).addEventListener(event_name, handler, use_capture);
      }
      else {
        $(element).attachEvent('on' + event_name, handler);
      }
    }
    on("outer", "click", o_click_c, true);
    on("outer", "click", o_click_b, false);
    on("middle", "click", m_click_c, true);
    on("middle", "click", m_click_b, false);
    on("inner", "click", i_click_c, true);
    on("inner", "click", i_click_b, false);
    function o_click_c() {
      console.log("outer_捕获");
      alert("outer_捕获");
    }
    function m_click_c() {
      console.log("middle_捕获")
      alert("middle_捕获");
    }
    function i_click_c() {
      console.log("inner_捕获")
      alert("inner_捕获");
    }
    function o_click_b() {
      console.log("outer_冒泡")
      alert("outer_冒泡");
    }
    function m_click_b() {
      console.log("middle_冒泡")
      alert("middle_冒泡");
    }
    function i_click_b() {
      console.log("inner_冒泡")
      alert("inner_冒泡");
    }
  </script>
</body>

</html>
```
