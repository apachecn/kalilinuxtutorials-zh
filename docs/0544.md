# Raptor WAF:使用 DFA Beta 的 Web 应用防火墙

> 原文：<https://kalilinuxtutorials.com/raptor-waf/>

Raptor 是一个用 C 语言编写的 Web 应用程序防火墙，使用 DFA 来阻止 SQL 注入、跨站脚本和路径遍历。

**运行**

**$ git 克隆 https://github.com/CoolerVoid/raptor_waf
$ CD 猛禽 _ waf 制造；宾/猛禽**

注意:不要用“cd bin。/raptor“使用完整路径”bin/raptor“look detail[https://github.com/CoolerVoid/raptor_waf/issues/4](https://github.com/CoolerVoid/raptor_waf/issues/4)

需要 lib pcre 来编译。

**也可阅读-[silk etw:抽象出 ETW](https://kalilinuxtutorials.com/silketw-abstract-complexities-etw/) 复杂性的工具 **

**例子**

一些 HTTPd 服务器在端口 80 上用其端口 8883 重定向

**$ bin/Raptor-h localhost-p 80-r 8883-w 4-o loglog . txt**

将易受攻击的 PHP 代码复制到您的 web 服务器目录

**$ CP doc/test _ DFA/test . PHP/var/www/html**

现在您可以在[http://localhost:8883/test . PHP](http://localhost:8883/test.php)测试 xss 攻击

要运行的其他选项(现在使用 regex，查看文件 config/regex_rules.txt 以编辑规则):

**$ bin/Raptor-h 127 . 0 . 0 . 1-p 80-r 8883-w 0-o result waf-m pcre**

[**Download**](https://github.com/CoolerVoid/raptor_waf)