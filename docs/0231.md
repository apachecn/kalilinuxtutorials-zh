# Burpsuite 扩展–Burp Suite 扩展的集合

> 原文：<https://kalilinuxtutorials.com/burpsuite-extensions/>

BurpSuite 扩展的集合。

## **Burpsuite Extensions gunziper**

burp suite([https://portswigger.net/burp/](https://portswigger.net/burp/))的插件，使您能够

*   “解包”请求/响应(例如，进行 base64 解码，然后进行 java 反序列化)
    *   反序列化是用 xstream([http://x-stream.github.io/index.html](http://x-stream.github.io/index.html))和 kxml 2([https://sourceforge.net/projects/kxml/files/kxml2/2.3.0/](https://sourceforge.net/projects/kxml/files/kxml2/2.3.0/))完成的
*   从响应中收集例如 CSRF 令牌并自动将其插入任何请求中的可能性(不需要使用 burps 宏功能进行额外的请求)
*   一半自动比较数百/数千个响应的差异
    *   假设您使用 intruder 测试了 10 个带有有效负载的 GET 参数，应用程序只是在响应中的某个地方反映了整个 URL。当然，可能会有 XSS，但是其他漏洞呢，比如 SQL、XXE……对响应大小的排序不会简单地指向相关的请求，所以入侵者比较器开始发挥作用。使用它，您可以定义一个正则表达式，该表达式剥离部分响应(例如，反射的 URL)，然后遍历所有响应，并对上一个响应和当前响应进行比较，如果有一些差异，它将显示一个类似于 burp 的比较器的 diff 窗口。用于 diffing 的库有“Diff Match and Patch”([http://code.google.com/p/google-diff-match-patch](http://code.google.com/p/google-diff-match-patch))和“Java-Diff-utils”([http://code.google.com/p/java-diff-utils/](http://code.google.com/p/java-diff-utils/))。

预构建的 jar 文件可以从[http://coding.f-block.org/](http://coding.f-block.org/)收集

**也可阅读[HUNT–Burp Suite Pro/Free 和 OWASP ZAP Extensions](https://kalilinuxtutorials.com/hunt-burp-suite/)**

## **SAML 请求**

测试 SAML 身份验证请求的 Burpsuite 扩展，在许多 SSO 实现中使用。它支持 SAML 身份验证请求的解码和修改，并根据被操纵的请求测试 IDP。它还与代理、中继器和入侵者集成，以最大限度地利用 Burpsuite 工具来测试 SAML 身份验证请求。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ernw/burpsuite-extensions)