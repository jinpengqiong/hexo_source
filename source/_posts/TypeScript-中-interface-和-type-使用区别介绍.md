---
title: TypeScript 中 interface 和 type 使用区别介绍
date: 2021-09-09 15:01:38
tags:
---

interface 和 type 很像，很多场景，两者都能使用。但也有细微的差别：
- 类型：对象、函数两者都适用，但是 type 可以用于基础类型、联合类型、元祖。
- 同名合并：interface 支持，type 不支持。
- 计算属性：type 支持, interface 不支持。

总的来说，公共的用 interface 实现，不能用 interface 实现的再用 type 实现。是一对互帮互助的好兄弟。
