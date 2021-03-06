---
layout:     post
title:      JavaScript知识点
subtitle:   H.T. Blog 知识点整理持续更新...
date:       2019-08-18
author:     haotian
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - JavaScript知识点
---

## 文章目录
1. JavaScript知识点

### 1. 对象转原始类型是根据什么流程运行的？
对象转原始类型，会调用内置的[ToPrimitive]函数，对于该函数而言，其逻辑如下：

1、如果Symbol.toPrimitive()方法，优先调用再返回 

2、调用valueOf()，如果转换为原始类型，则返回

3、调用toString()，如果转换为原始类型，则返回

4、如果都没有返回原始类型，会报错
```js
var obj = {
    value: 3,
    toString() {
        return '4'
    },
    valueOf() {
        return 5;
    },
    [Symbol.toPrimitive]() {
        return 6
    }
}
console.log(obj + 1); // 输出7
```
### 2. 如何让if(a == 1 && a == 2)条件成立？
其实就是上一个问题的应用。
```js
var a = {
  value: 0,
  valueOf: function() {
    this.value++;
    return this.value;
  }
};
console.log(a == 1 && a == 2);//true
```