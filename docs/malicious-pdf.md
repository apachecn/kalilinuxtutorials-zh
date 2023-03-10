# 恶意 Pdf:生成一堆带有呼叫总部功能的恶意 Pdf 文件

> 原文：<https://kalilinuxtutorials.com/malicious-pdf/>

[![](img/0512a98476acf18273156176b1b63b87.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgK7y6nNlCEGj4I882P3yOf74L6uniHLxXVPpsDVDG-RQd3JA9vNDftjh_T8M7PtLsS51zD16CgXaj51kGTZmLH0MSq6-Z96L5v5zYkqcBHsOkn8jvrpXuyTDT-Tytl0iMzmYOxQXoszoUcsoJ3yg16MhXiWFeJn9JF53wTt9th-upeZUOo3RURXy66/s728/12dfde6e-c20c-4b91-b115-ae699f43543e%20(1).png)

**恶意 Pdf** 生成十种不同的具有呼叫总部功能的恶意 Pdf 文件。可与 Burp Collaborator 或 Interact.sh 一起使用

用于渗透测试和/或红队等。我创建这个工具是因为我需要一个第三方工具来生成一堆带有各种链接的 PDF 文件。

## 用法

`**python3 malicious-pdf.py burp-collaborator-url**`

输出将被写成:test1.pdf，test2.pdf，test3.pdf 等在当前目录中。

不要在 url 参数中使用 https:// etc 前缀。

## 目的

*   测试接受 PDF 文件的网页/服务
*   测试安全产品
*   测试 PDF 阅读器
*   测试 PDF 转换器

[**Download**](https://github.com/jonaslejon/malicious-pdf)