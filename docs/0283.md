# XXRF 镜头–用于测试 SSRF 漏洞

> 原文：<https://kalilinuxtutorials.com/xxrf-shots-ssrf-vulnerability/>

XXRF 镜头对于测试 SSRF 漏洞很有用。服务器端请求伪造或 SSRF 是一种漏洞类别，攻击者从易受攻击的 web 应用程序发送精心编制的请求，包括对防火墙后的内部资源进行未经授权的访问，这些资源无法从外部网络直接访问。

## **XXRF拍摄安装**

```
git clone [https://github.com/ariya/phantomjs.git](https://github.com/ariya/phantomjs.git)****cd phantomjs**
**chmod +x build.py**
**./build.py
```

**也读作[CLR inject——将 C# EXE 或 DLL 程序集注入到每个 CLR 运行时和另一个进程的 AppDomain](https://kalilinuxtutorials.com/clrinject/)**

## **用途**

```
./xxrf.sh
```

输入带有易受攻击参数的 url，然后按回车键。该脚本旨在执行两个不同的任务。首先，它将在易受攻击的参数旁边注入有效负载，并将请求处理到由@ maaaaz 编写的另一个 python 脚本。python 脚本要求 phantomJS 执行屏幕截图功能。

## **Youtube**

[https://www.youtube.com/embed/z9ct4OoRQ_M?feature=oembed](https://www.youtube.com/embed/z9ct4OoRQ_M?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/samhaxr/XXRF-Shots)