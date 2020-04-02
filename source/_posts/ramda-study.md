---
title: 几个ramda方法
date: 2020-04-02 11:01:39
tags:
---

## compose

从右往左执行函数组合（右侧函数的输出作为左侧函数的输入）。最后一个函数可以是任意元函数（参数个数不限），其余函数必须是一元函数。

```javascript
    R.compose(Math.abs, R.add(1), R.multiply(2))(-4) //=> 7
```

## prop

取出对象中指定属性的值。如果不存在，则返回 undefined。

```javascript
R.prop('x', {x: 100}); //=> 100
R.prop('x', {}); //=> undefined
R.prop(0, [100]); //=> 100
R.compose(R.inc, R.prop('x'))({ x: 3 }) //=> 4
```
