---
title: 关于Array操作的一些性能测试
date: 2016-03-30 11:26:21
tags:
- Node.js
- javascript
categories: 
- javascript
---

## 前言

在日常开发中，同一种结果使用js可以有多种实现方式，不同的实现方式影响着的性能上的差异。在做极致优化的过程中，某些影响性能的方法尽量避免，这里先对Array的一些操作测试。

## 环境

Node.js版本为`node -v v5.6.0`
Mac air 

## 为数组添加元素

两个例子：
```javascript
var array1 = [];
var array2 = [];

console.time('array push');

for (var i = 0; i < 1000000; i++) {
  array1.push('a'+i);
}

console.timeEnd('array push');


console.time('array push2');

for (var i = 0; i < 1000000; i++) {
  array2[i] = 'a'+i;
}

console.timeEnd('array push2');
```

结果：
```
array push: 352.841ms
array push2: 258.473ms
```
<!--more-->

## 为合并两个数组

例1：
```javascript
console.time('array concat');

var array1 = array1.concat(array2);

console.timeEnd('array concat');
console.log('length:' + array1.length);
```

结果：
```
array concat: 28.534ms
length:2000000
```

例2：
```javascript
console.time('array concat2');

array2.forEach(function(v){
  array1.push(v);
});

console.timeEnd('array concat2');
console.log('length:' + array1.length);
```

结果：
```
array concat2: 117.288ms
length:2000000
```

例3：
```javascript
console.time('array concat3');

for (var i = 0; i < array2.length; i++) {
  array1.push(array2[i]);
}

console.timeEnd('array concat3');
console.log('length:' + array1.length);
```

结果：
```
array concat2: 61.036ms
length:2000000
```

## 待续。。。
