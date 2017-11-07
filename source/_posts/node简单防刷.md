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
3.页面请求把Token带回来

>页面请求带着自定义的Token回传，注意，这个地方可以自己实现一些算法和混淆的东西。我这里提供一个东西。就是通过字符串拆分，把生成的Token放在html中，获取的时候也是随机的。达到每次获取都不一样。
记住标签随机，id值随机生成，在server端输出给html。

```bash
<samp id="_CWXF0" style="display:none;">f</samp>
<i id="_CWXF1" style="display:none;">k</i>
<sub id="_CWXF2" style="display:none;">2</sub>
<tt id="_CWXF3" style="display:none;">d</tt>
<bdo id="_CWXF4" style="display:none;">f</bdo>
<b id="_CWXF5" style="display:none;">d</b>
<cite id="_CWXF6" style="display:none;">7</cite>
<tt id="_CWXF7" style="display:none;">b</tt>
<code id="_CWXF8" style="display:none;">e</code>
<dfn id="_CWXF9" style="display:none;">g</dfn>
<time id="_CWXF10" style="display:none;">3</time>
<code id="_CWXF11" style="display:none;">8</code>
<sub id="_CWXF12" style="display:none;">1</sub>
<code id="_CWXF13" style="display:none;">a</code>
<em id="_CWXF14" style="display:none;">o</em>
<bdo id="_CWXF15" style="display:none;">b</bdo>
<i id="_CWXF16" style="display:none;">d</i>
<i id="_CWXF17" style="display:none;">e</i>
<sup id="_CWXF18" style="display:none;">j</sup>
<small id="_CWXF19" style="display:none;">9</small>
<code id="_CWXF20" style="display:none;">m</code>
<em id="_CWXF21" style="display:none;">4</em>
<small id="_CWXF22" style="display:none;">9</small>
<cite id="_CWXF23" style="display:none;">c</cite>
<abbr id="_CWXF24" style="display:none;">g</abbr>
<tt id="_CWXF25" style="display:none;">5</tt>
<code id="_CWXF26" style="display:none;">h</code>
<sup id="_CWXF27" style="display:none;">6</sup>
<sub id="_CWXF28" style="display:none;">5</sub>
<span id="_CWXF29" style="display:none;">f</span>
<sup id="_CWXF30" style="display:none;">0</sup>
<i id="_CWXF31" style="display:none;">3</i>
<label id="_CWXF32" style="display:none;">7</label>
<span id="_CWXF33" style="display:none;">e</span>
<code id="_CWXF34" style="display:none;">9</code>
<label id="_CWXF35" style="display:none;">6</label>
<bdo id="_CWXF36" style="display:none;">3</bdo>
<code id="_CWXF37" style="display:none;">b</code>
<cite id="_CWXF38" style="display:none;">3</cite>
<acronym id="_CWXF39" style="display:none;">3</acronym>
<sub id="_CWXF40" style="display:none;">m</sub>
<dfn id="_CWXF41" style="display:none;">8</dfn>
<map id="_CWXF42" style="display:none;">o</map>
<strong id="_CWXF43" style="display:none;">9</strong>
<sup id="_CWXF44" style="display:none;">j</sup>
<em id="_CWXF45" style="display:none;">d</em>
<script>
(function(w){
    var r = "";
    function g(id){
        return document.getElementById(id).innerHTML;
    }
    r += g("_CWXF0");r += g("_CWXF1");r += g("_CWXF2");r += g("_CWXF3");
    r += g("_CWXF4");r += g("_CWXF5");r += g("_CWXF6");r += g("_CWXF7");
    r += g("_CWXF8");r += g("_CWXF9");r += g("_CWXF10");r += g("_CWXF11");
    r += g("_CWXF12");r += g("_CWXF13");r += g("_CWXF14");r += g("_CWXF15");
    r += g("_CWXF16");r += g("_CWXF17");r += g("_CWXF18");r += g("_CWXF19");
    r += g("_CWXF20");r += g("_CWXF21");r += g("_CWXF22");r += g("_CWXF23");
    r += g("_CWXF24");r += g("_CWXF25");r += g("_CWXF26");r += g("_CWXF27");
    r += g("_CWXF28");r += g("_CWXF29");r += g("_CWXF30");r += g("_CWXF31");
    r += g("_CWXF32");r += g("_CWXF33");r += g("_CWXF34");r += g("_CWXF35");
    r += g("_CWXF36");r += g("_CWXF37");r += g("_CWXF38");r += g("_CWXF39");
    r += g("_CWXF40");r += g("_CWXF41");r += g("_CWXF42");r += g("_CWXF43");
    r += g("_CWXF44");r += g("_CWXF45");
    w.tokenName=r;
})(window)
</script>
```
4.校验token是否合法

>在路由的地方加入拦截器，达到获取Token的目的，这里为了统一处理前端，建议放在header中，传递，你可以在前端统一封装的ajax处统一处理，以达到不影响业务代码的目的。
```bash
verifyToken(req, res, next) {
    if (req.headers['token_fe']) {
        next();
    } else {
        res.jsonp({
            code: -1,
            ret: false,
            msg: 'access not vaildate'
        });
    }
}
```
这样就实现了最简单的Token防刷,当然重要的是，你可以把token放在内存中，内存中加入过期时间，和有效的规则，比如，一分钟这个Token请求多少次。就不能再次请求等。可以可以注入IP，以IP的模式来校验不能多次请求。