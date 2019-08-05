---
layout: post
title: "Node.js Express 框架"
date: 2019-08-05
tag: 学习
---



---

Express 是一个为Node.js设计的web开发框架，它基于nodejs平台。



## Express 简介

Express是一个简洁而灵活的node.js Web应用框架, 提供了一系列强大特性帮助你创建各种Web应用，和丰富的HTTP工具。
使用Express可以快速地搭建一个完整功能的网站。



## Express 框架核心特性包括：

* 可以设置中间件来响应HTTP请求。
* 定义了路由表用于执行不同的HTTP请求动作。
* 可以通过向模板传递参数来动态渲染HTML页面。



## 安装 Express

安装Express并将其保存到依赖列表中：

```
$ npm install express --save
```

以上命令会将Express框架安装在当期目录的node_modules目录中， node_modules目录下会自动创建express目录。以下几个重要的模块是需要与express框架一起安装的：

* body-parser - node.js中间件，用于处理JSON, Raw, Text和URL编码的数据。
* cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
* multer - node.js中间件，用于处理enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。



## Express 框架

1. 引入 express 模块

   ```
   var app = require('express')();
   ```

2. 请求和响应

   ```
   app.get('/', function(req, res){}
   Express应用使用回调函数的参数： request和response对象来处理请求和响应的数据。
   ```



**request 和 response 对象的具体介绍：**

Request 对象 - request对象表示HTTP请求，包含了请求查询字符串，参数，内容，HTTP头部等属性。常见属性有：

- req.app：当callback为外部文件时，用req.app访问express的实例
- req.baseUrl：获取路由当前安装的URL路径
- req.body / req.cookies：获得「请求主体」/ Cookies
- req.fresh / req.stale：判断请求是否还「新鲜」
- req.hostname / req.ip：获取主机名和IP地址
- req.originalUrl：获取原始请求URL
- req.params：获取路由的parameters
- req.path：获取请求路径
- req.protocol：获取协议类型
- req.query：获取URL的查询参数串
- req.route：获取当前匹配的路由
- req.subdomains：获取子域名
- req.accpets（）：检查请求的Accept头的请求类型
- req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages
- req.get（）：获取指定的HTTP请求头
- req.is（）：判断请求头Content-Type的MIME类型

Response 对象 - response对象表示HTTP响应，即在接收到请求时向客户端发送的HTTP响应数据。常见属性有：

-  res.app：同req.app一样
- res.append（）：追加指定HTTP头
- res.set（）在res.append（）后将重置之前设置的头
- res.cookie（name，value [，option]）：设置Cookie
- opition: domain / expires / httpOnly / maxAge / path / secure / signed
- res.clearCookie（）：清除Cookie
- res.download（）：传送指定路径的文件
- res.get（）：返回指定的HTTP头
- res.json（）：传送JSON响应
- res.jsonp（）：传送JSONP响应
- res.location（）：只设置响应的Location HTTP头，不设置状态码或者close response
- res.redirect（）：设置响应的Location HTTP头，并且设置状态码302
- res.send（）：传送HTTP响应
- res.sendFile（path [，options] [，fn]）：传送指定路径的文件 -会自动根据文件extension设定Content-Type
- res.set（）：设置HTTP头，传入object可以一次设置多个头
- res.status（）：设置HTTP状态码
- res.type（）：设置Content-Type的MIME类型



### GET 方法

在表单中通过GET方法提交两个参数，我们可以使用server.js文件内的process_get路由器来处理输入


### POST 方法

在表单中通过POST方法提交两个参数，我们可以使用server.js文件内的process_post路由器来处理输入


### 文件上传

创建一个用于上传文件的表单，使用POST方法，表单enctype属性设置为multipart/form-data。


### Cookie 管理

我们可以使用中间件向Node.js服务器发送cookie信息