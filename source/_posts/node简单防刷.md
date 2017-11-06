---
title: node简单防刷
date: 2017-11-06 20:51:29
tags:
author:
---
## 简单的安全防范

web时代的今天，我们经常会暴露一些接口给外网，但是很多作为前端工程师，也是需要在互联网的今天做一点攻防。不能直接让人直接访问你的接口，所以，本篇文章主要简单的介绍下。如何的简单的实现防刷。

文章主要采用node.js作为介绍。

首先，我们理解下，一个接口没有任何防刷。你只需要打开浏览器，直接找到对应的接口，直接刷新就可以直接搞定接口。这样我们的风险还是很高的。让刷的难度稍微高一点。

最简单的做法就是，Token验证和访问限制。

1.我们需要server端生成一段随机数。
```bash
injectAccessToken(req, res, next) {
    req._access_token = Math.random().toString(26).slice(2);
    next();
}
```

2.把Token注入到页面中
```nodejs
webInject:function(html,token,callback){
    var htmlEndIndex = html.indexOf('</html>');
    var tokenScript = '<script>window.' + this.config.webTokenVarName + '=' + token + '</script>';
    var prevHtml = html.substring(0, htmlEndIndex);
    var nextHtml = html.substr(htmlEndIndex);
    prevHtml += tokenScript;
    prevHtml += nextHtml;
    callback(null, prevHtml);
}
```
待续....
3.页面请求把Token带回来

4.校验token是否合法

这样就实现了最简单的Token防刷