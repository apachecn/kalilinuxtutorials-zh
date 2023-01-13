# 0d1n:在 HTTP/S 上进行 Fuzzing 的 Web 安全工具

> 原文：<https://kalilinuxtutorials.com/0d1n-web-security-tool/>

0d1n 是一个针对 web 应用程序的自动化定制攻击的工具。让我们看看 Web 安全工具支持的特性。

*   授权表单中的暴力登录和密码
*   目录泄露(使用路径列表破解，并找到 HTTP 状态代码)
*   测试以查找 SQL 注入和 XSS 漏洞
*   每个请求加载反 CSRF 令牌的选项
*   每个请求使用随机代理的选项
*   其他功能…

**也可阅读-[QRLJacking:一种新的社会工程攻击载体](https://kalilinuxtutorials.com/qrljacking-a-attack-vector/)**

**旧版本**

你可以点击这里下载旧版本的网络安全工具。

**安装&使用**

*   需要 libcurl-dev 或 libcurl-devel(基于 rpm linux)

**$ git 克隆 https://github.com/CoolerVoid/0d1n/**

*   需要 libcurl 来运行

**$ sudo apt-get install libcurl-dev**

*   if rpm 发行版

**$ sudo yum install libcurl-devel
$ make
$。/0d1n**

*   阅读文件

[**Download**](https://github.com/CoolerVoid/0d1n)