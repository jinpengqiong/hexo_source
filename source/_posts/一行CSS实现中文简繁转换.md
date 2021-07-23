---
title: 一行CSS实现中文简繁转换
date: 2021-07-23 10:47:25
tags:
---

只需一行css设置即可实现此转换：
```
font-variant-east-asian: traditional;
```
由于MAC、iphone等苹果设置的字体本身包含简体和繁体字体，所以该设置加上后立即生效；
而window的默认字体没包含繁体，需要下载一个苹方字体，才可支持；

```
body {
    font-family: 'PingFang SC';
    font-variant-east-asian: traditional;
}
```
