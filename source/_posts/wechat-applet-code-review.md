---
title: 代码发布审核未通过,请你完善内容审核机制
date: 2020-01-09 19:51:55
tags:
- wechat
- 小程序
- 审核
---
## 问题描述
小程序代码发布审核未通过，原因如下：
1:小程序内容不符合规则:
(1):为避免您的小程序被滥用，请你完善内容审核机制，如调用小程序内容安全API，或使用其他技术、人工审核手段，过滤色情、违法等有害信息，保障发布内容的安全。
请根据上述原因对小程序进行修改，并重新提交代码审核。
## 解决过程
针对不符合的内容进行了改善，引入了小程序内容安全API msgSecCheck。
为了调用这个API，在小程序中加入了云开发，创建了两个云函数。
一个用来获得 **access_token**,代码如下：
```javascript
const cloud = require('wx-server-sdk')
const request = require('request')

cloud.init()

var appid = '你的appid'
var appsecret = '你的appsecret'
let token_url = 'https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=' + appid + '&secret=' + appsecret
// 云函数入口函数
exports.main = async (event, context) => {
  const rp = options =>
    new Promise((resolve, reject) => {
      request(options, (error, response, body) => {
        if (error) {
          reject(error);
        }
        resolve(response);
      });
    });
  const result = await rp({
    url: token_url,
    method: 'GET'
  });
  return (typeof result.body === 'object') ? result.body : JSON.parse(result.body);
}
```
一个用来调用**msgSecCheck**,代码如下：
```javascript
// 云函数入口文件
const cloud = require('wx-server-sdk')
const request = require('request')

cloud.init()

let checkUrl = 'https://api.weixin.qq.com/wxa/msg_sec_check' 
// 云函数入口函数
exports.main = async (event, context) => {
  const rp = options =>
    new Promise((resolve, reject) => {
      request(options, (error, response, body) => {
        if (error) {
          reject(error);
        }
        resolve(response);
      });
    });
  const resultTwo = await rp({
    url: checkUrl + '?access_token=' + event.access_token,
    method: 'POST',
    body: JSON.stringify({content: event.text})
  })
  return (typeof resultTwo.body === 'object') ? resultTwo.body : JSON.parse(resultTwo.body);
}
```
有个坑点就是access_token是拼接在请求路径上的，需要注意一下。

