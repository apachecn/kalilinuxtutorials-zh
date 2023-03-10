# DOMDig:用于单页应用的 DOM XSS 扫描仪

> 原文：<https://kalilinuxtutorials.com/domdig/>

[![](img/920affa00eabdbd00bc3a25779d238d9.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg45zod210fKCGVcegNdjNwyngidYK1G5j4UQHwEcwuBtXBEukcM9EiU_nYxzA1uBPaOJFS8EKC0RE9JT_U9myva2Y-JMua5hFD2ST1fD-a1ri5pJWIuoZGoopWjPgD_k6zcKVUwdQua7wwg0QWxUqMy-HZ2PK1Hh3CXXqeE9ariUgPS9YlvwVufexU/s728/Cross-Site-Scripting-XSS-Attacks%20(1).png)

DOMDig 是一个运行在 Chromium 浏览器内部的 DOM XSS 扫描器，它可以递归扫描单页应用程序(SPA)。
与其他扫描器不同，DOMDig 可以通过跟踪 DOM 修改和 XHR/fetch/websocket 请求来抓取任何 web 应用程序(包括 gmail ),并且可以通过触发事件来模拟真实的用户交互。在这个过程中，XSS 有效负载被放入输入字段，它们的执行被跟踪，以便找到注入点和相关的 URL 修改。
它基于 htcrawl，这是一个足够强大的节点库，可以轻松抓取 gmail 帐户。

## 主要特点

*   在真正的浏览器中运行(Chromium)
*   递归 DOM 爬行引擎
*   处理 XHR、获取、JSONP 和 websockets 请求
*   支持 cookies，代理，自定义头，http 认证和更多
*   可脚本化的登录序列

## 开始使用

### 安装

**git 克隆 https://github.com/fcavallarin/domdig.git
CD DOM dig&NPM I&CD..
节点 domdig/domdig.js**

**例子**

**node DOM dig . js-c ' foo = bar '-p http:127 . 0 . 0 . 1:8080 https://htcap.org/scanme/domxss.php**

### 登录序列

登录序列(或初始序列)是一个 json 对象，包含扫描开始前要采取的一系列操作。列表中的每个元素都是一个数组，其中第一个元素是要采取的动作的名称，其余元素是这些动作的“参数”。行动包括:

*   写
*   点击
*   点击导航
*   睡眠

#### 举例

**[
["写"、" #用户名"、"演示"]、
["写"、" #密码"、"演示"]、
["点击导航"、" # BTN-登录"]、
]**

### 有效负载文件

有效负载可以作为字符串数组从 json 文件(-P 选项)加载。要构建定制的有效负载，必须使用字符串`**window.___xssSink({0})**`作为要执行的函数(而不是传统的`**alert(1)**`

#### 举例

**【
’；窗户。_ _ _ XSS sink({ 0 })；“、
' ![](img/9a11002d14ee21f54b81445816f527b2.png) '
]**

[**Download**](https://github.com/fcavallarin/domdig)