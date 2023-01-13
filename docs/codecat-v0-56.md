# Codecat v0.56:一个帮助你发现/跟踪用户输入接收器和安全漏洞的开源工具

> 原文：<https://kalilinuxtutorials.com/codecat-v0-56/>

[![](img/0a8fe4756019c7d1929a81cafa82a115.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjzEcDAcpUVpdT5ZUQHawgpr8SC9Gmn1NJxvPgHWStzN0NRlLD_fJ3Qi4kIPSzPp8fNvs5HAvdCq-CsmLhAE_wOhZ_L9ZNDS9FySosDbCFIVbv2eIUdqd5lS-S5wRHq6igVxA4C7IIis8CYKle4kxPYEgND7b664mNmaPIt_8EggQOxkKFY6XS4M8_S/s728/Top-5-Open-Source-Source-and-Free-Static-Code-Analysis-Tools-in-2020.png)

CodeCat 是一个开源工具，使用静态代码分析来帮助你发现/跟踪用户输入接收器和安全漏洞。这些点遵循正则表达式规则。C，C++，GO，Python，javascript，Swift，PHP，Ruby，ASP，Kotlin，Dart，Java 的现行规则。(您可以创建自己的规则)。

## 如何一步一步安装

转到 CodeCat 目录，安装后端和前端库:

**$ apt 安装 python 3-venv python 3-dev libffi-dev rustc libssl-dev
$ python 3-m venv。venv
$。。venv/bin/activate
$ pip 安装轮
$ pip 安装-r 前端/requirements.txt
$ pip 安装-r 后端/requirements.txt**

运行后端和前端

**$ cd Codecat
$ cd 前端；python 3 wsgi . py&$ CD..
$ cd 后端；python 3 wsgi . py&**

下一步，您需要保存您的用户以登录:

**$ curl-I-X POST-H " Content-Type:application/JSON "-d ' { " email ":" admin 2 @ test . com "，" username":"admin "，" password ":" rubrik 123 "} ' https://127 . 0 . 0 . 1:50001/API/users-k**

这些端点/API/用户在第一次部署中只运行一次。如果您尝试再次发送请求以插入用户，端点返回 404 是安全的，以阻止可能的攻击的资源。

转到下面的“https://127 . 0 . 0 . 1:50093/front/auth/”。现在你可以进入这个系统-auth，使用登录名“admin”，通过“rubrik123”。

*关于 TLS 的注意:*您可以在“wsgi.py”中配置并加载您的 TLS 证书。

# 生产

假设你需要在生产中运行。所以我推荐另一种方式。

**$ guni corn-b 127 . 0 . 0 . 1:50001 wsgi:app**

如果您愿意，可以将 TLS 与证书资源一起使用:

**$ guni corn–cert file = server . CRT–keyfile = server . key-b 127 . 0 . 0 . 1:50001 wsgi:app**

相同的命令发送到前端，但是您需要使用端口 50093。

[**Download**](https://github.com/CoolerVoid/codecat)