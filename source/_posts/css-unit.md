---
title: vw、vh布局部分手机浏览器弹出软键盘导致的样式问题
date: 2020-01-04 14:57:55
tags:
- css
- unit
---
## 问题描述
最近写了一个移动端H5注册页面，vw、vh 优势在于能够直接获取高度，可以很好的适应不同尺寸大小的屏幕，
但是在真机调试的时候遇到了部分手机浏览器弹出软键盘导致的样式问题。
## 解决方法
监听软键盘弹出前后浏览器的大小，当浏览器大小改变保持body的大小不变
```javascript
var clientHeight = document.documentElement.clientHeight || document.body.clientHeight;
window.onresize = function () {
    var nowClientHeight = document.documentElement.clientHeight || document.body.clientHeight;
    if (clientHeight > nowClientHeight) {
        //键盘弹出的事件处理
    }
    else {
        //键盘收起的事件处理
    }
```
