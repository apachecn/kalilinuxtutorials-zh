# Jsleak:通过正则表达式模式检测 JS 文件中漏洞的 Go 代码

> 原文：<https://kalilinuxtutorials.com/jsleak/>

[![](img/569a74e695b468c60723c3926eb59b12.png)](https://1.bp.blogspot.com/-rDGJzlB-5cI/YScoiDyKNlI/AAAAAAAAKk4/XhiPTNIlLTYtw54dwSZU-0tWO6Y8Cot8gCLcBGAsYHQ/s728/images%2B%25281%2529.png)

**jsleak** 是一个通过 regex 模式识别 JS 文件中敏感数据的工具。尽管它是为此而构建的，但是只要有正则表达式模式，就可以用它来识别任何东西。

**如何安装**

直接:

{你的软件包管理员}安装 pkg-config libpcre ++ dev
去找 github.com/0xTeles/jsleak/v2/jsleak

**如何使用**

**-json 字符串
[+] Json 输出文件
-模式字符串
[+]文件包含要测试的模式
-timeout int
[+]请求超时秒数(默认为 5)
-verbose
[+]详细模式**

**演示**

**cat URLs . txt | js leak-Pattern regex . txt
[+]Url:http://localhost/index . js
[+]Pattern:p([a-z]+)ch
[+]Match:peach**

[**Download**](https://github.com/0xTeles/jsleak)