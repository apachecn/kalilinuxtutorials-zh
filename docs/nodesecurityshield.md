# NodeSecurityShield:一个开发者和安全工程师友好的包，用于保护 NodeJS 应用程序

> 原文：<https://kalilinuxtutorials.com/nodesecurityshield/>

[![](img/28ae36e34e7d1a1b23d699b7c7f0f621.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg0OhwGIVq2NJ5gPelHPgArA_SgQcnRDOyIEP9s7HJkQt0co6vT7d3JP3_I_UaTyI5xOvzSmExnLoZvWXuZC2_LP0b1HHkBwWpdZwwDT8IlJqyJ4ajgjRE5idgfzOdWZYmCVHZcwTQk3ns9IRnvvQu_KOditX4yAbqsNnNO7zj5XOmFvjaAhnbe60Zc/s728/NodeSecurityShield%20(1).png)

NodeSecurityShield 是一个开发者和安全工程师友好的包，用于保护 NodeJS 应用。

受 log4J 漏洞(CVE-2021-44228)的启发，该漏洞可以被利用，因为应用程序可以进行任意网络调用。

我们认为有必要让应用程序声明它可以拥有什么特权，这样利用这些漏洞就变得更加困难。

为此， **NSS** ( **节点安全盾**)有**资源访问策略**。

### 资源访问策略(RAP)

**资源访问策略**类似于 **CSP** (内容安全策略)。

它让开发人员/安全工程师声明应用程序应该访问哪些资源。而**节点安全盾**会强制执行。

## 安装

使用 npm 安装*节点安全屏蔽*

**npm 安装节点安全屏蔽**

## 使用

/ **/要求节点安全屏蔽
let nodeSecurityShield = Require(' nodeSecurityShield ')；
//启用攻击监控和/或拦截
nodesecurityshield . enableattackmoning(resourceAccessPolicy，callbackFunction)；**

**样本*资源访问策略***

**const resourceAccessPolicy = {
" outbound request ":{
" blocked domains ":["*. 123 . com "，" stats.abc.com "，" xyz.com']，" allowed domains ":["*. DOM dog . io "]
}
}；**

**样本*回调函数*进行攻击监控**

**var callback function = function(violation event){
console . log(violation event)；
}**

**样本*回调函数*拦截攻击**

**var callback function = function(violation event){
抛出新错误("请求被阻止。它违反了声明的资源访问策略。)
}**

### 与哨兵集成

**示例*资源访问策略与哨兵*集成 **

**const resourceAccessPolicy = {
" reportUriHosts ":[" ingest . sentry . io "]，
" outbound request ":{
" blocked domains ":["*. 123 . com "，" stats.abc.com "，" xyz.com']，" allowedDomains ":["*. DOM dog . io "]
}
}；**

## 特征

*   **攻击监控**
    *   出站网络呼叫
*   **攻击阻断**
    *   出站网络呼叫

[**Download**](https://github.com/DomdogSec/NodeSecurityShield)