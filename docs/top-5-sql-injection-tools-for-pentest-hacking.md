# PenTest 和 Hacking 的五大 SQL 注入工具

> 原文：<https://kalilinuxtutorials.com/top-5-sql-injection-tools-for-pentest-hacking/>

SQL 注入是一种代码注入技术，用于攻击可能破坏数据库的数据驱动应用程序。这里，恶意代码通过网页输入被插入到 SQL 语句中。

SQL 注入是最常见的网络黑客技术之一。让我们看看检测漏洞的五大 SQL 注入工具！

## **sqlcmap**的缩写

Sqlmap 是一个开源的 SQL 注入工具，可以自动检测和利用 SQL 注入漏洞，并接管数据库服务器。

SQLMap 有，

*   强大的检测引擎
*   许多利基功能作为最终渗透测试
*   从数据库指纹识别、从数据库获取数据、访问底层文件系统到通过带外连接在操作系统上执行命令，范围广泛的开关

[![](img/9a268065609fa6e87a933a4185b12fe5.png)](https://github.com/sqlmapproject/sqlmap)

## **jSQL 注射液**

jSQL Injection 是一个轻量级应用程序，用于从远程服务器上查找数据库信息。

sql 注入是，

*   免费、开源，可跨平台运行(Windows、Linux、Mac OS X、Solaris)
*   Kali Linux 官方渗透测试发行版的一部分，包含在 Pentest Box、Parrot Security OS、ArchStrike 或 BlackArch Linux 等其他发行版中。
*   具有“23 种数据库自动注入”的特色，具有正常、错误、盲注和定时注入策略

[![](img/9a268065609fa6e87a933a4185b12fe5.png)](https://github.com/ron190/jsql-injection)

## **白寡妇**

白寡妇是一个开源的自动 SQL 注入工具，它能够运行一个文件列表，或者可以从谷歌搜索潜在的易受攻击的网站。

它允许自动文件格式化，随机用户代理，IP 地址，服务器信息，多 SQL 注入语法，从程序启动 sqlmap 的能力，和一个有趣的环境。

[![](img/9a268065609fa6e87a933a4185b12fe5.png)](https://github.com/WhitewidowScanner/whitewidow)

## **盲 Sql 移位**

blind-Sql-bitshift 通过使用位移位方法计算字符而不是猜测字符来执行盲 Sql 注入。

根据配置，每个字符需要 7/8 个请求。

[![](img/9a268065609fa6e87a933a4185b12fe5.png)](https://github.com/awnumar/blind-sql-bitshifting)

## **布利基**

Blisqy 是一个工具，帮助网络安全研究人员找到基于时间的盲 SQL 注入对 HTTP 头，也利用相同的漏洞。

*   通过 Blisqy 利用该漏洞，可以通过盲 SQL 注入对可打印的 ASCII 字符进行逐位操作，从而从数据库中缓慢虹吸数据(目前仅支持 MySQL/MariaDB)。
*   为了实现与其他 Python 工具的互操作性并支持其他用户，Blisqy 中提供了一些特殊功能，可以将这些模块导入到其他基于 Python 的脚本中。

[![](img/9a268065609fa6e87a933a4185b12fe5.png)](https://github.com/JohnTroony/Blisqy)

尝试所有最好的工具并探索它们！