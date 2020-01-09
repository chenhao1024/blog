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
## 问题原因
苹果手机软键盘是叠在可视窗口上面的，也就是不影响可视窗口的大小。但是在安卓，软键盘是在窗口中，即占用窗口的面积。
## 解决方法1
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
## 解决方法2
在csdn看到一个更好的解决方法。
给viewport设置height值，可用window.innerHeight赋值。
```javascript
 <meta name="viewport" id="viewportMeta">
```
```javascript
var initViewport = function(height){
	var metaEl = document.querySelector("#viewportMeta");
	var content = "height=" + height + ",width=device-width,initial-scale=1.0,user-scalable=no";
	metaEl.setAttribute('name', 'viewport');
	metaEl.setAttribute('content', content);
}
var realHeight = window.innerWidth > window.innerHeight ? window.innerWidth : window.innerHeight
initViewport(realHeight);

```
