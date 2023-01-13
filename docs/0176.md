# joomscan-OWASP Joomla 漏洞扫描器项目

> 原文：<https://kalilinuxtutorials.com/owasp-joomla-vulnerability-scanner/>

JoomScan 或 OWASP Joomla 漏洞扫描器是一个开源项目，旨在自动执行 Joomla CMS 部署中的漏洞检测和可靠性保证任务。这个工具是用 Perl 实现的，能够无缝、轻松地扫描 Joomla 安装，同时以其轻量级和模块化的架构留下最小的足迹。它不仅能够检测已知的攻击性漏洞，还能够检测许多错误配置和管理员级别的缺陷，这些缺陷可能会被对手利用来危害系统。此外，OWASP Joomla 漏洞扫描程序提供了一个用户友好的界面，并以文本和 HTML 格式编写最终报告，以便于使用和最大限度地减少报告开销。

OWASP Joomla 漏洞扫描程序包含在 Kali Linux 发行版中。

**也读[WarChild——为分析](https://kalilinuxtutorials.com/warchild-denial-service-testing/)** 而制作的拒绝服务测试套件

## 为什么是 OWASP JOOMSCAN？

*   版本枚举器
*   漏洞枚举器(基于版本)
*   组件枚举器(默认情况下 1209 最常用)
*   组件漏洞枚举器(基于版本)(+1030 漏洞)
*   防火墙检测器
*   报告到文本和 HTML 输出
*   查找公共日志文件
*   查找常用备份文件

## **安装**

```
git clone https://github.com/rezasp/joomscan.git
cd joomscan
perl joomscan.pl
```

## **自变量**

```
Usage:	joomscan.pl [options]

--url | -u <URL>                |   The Joomla URL/domain to scan.
--enumerate-components | -ec    |   Try to enumerate components.

--cookie <String>               |   Set cookie.
--user-agent | -a <user-agent>  |   Use the specified User-Agent.
--random-agent | -r             |   Use a random User-Agent.
--timeout <time-out>            |   set timeout.
--about                         |   About Author
--update                        |   Update to the latest version.
--help | -h                     |   This help screen.
--version                       |   Output the current version and exit.
```

## **OWASP Joomla 漏洞扫描器使用示例** 

**进行默认检查。**..
`**perl joomscan.pl --url www.example.com**`
或
`**perl joomscan.pl -u www.example.com**`
**枚举已安装的组件……**
`**perl joomscan.pl --url www.example.com --enumerate-components**`
或
`**perl joomscan.pl -u www.example.com --ec**`
**设置 cookie**
`**perl joomscan.pl --url www.example.com --cookie "test=demo;"**`
**设置用户代理**
`**perl joomscan.pl --url www.example.com --user-agent "Googlebot/2.1** **(+http://www.googlebot.com/bot.html)"**`
或
`**perl joomscan.pl -u www.example.com -a "Googlebot/2.1 (+http://www.googlebot.com/bot.html)"**`
**设置随机用户代理**`**perl joomscan.pl -u www.example.com --random-agent**`
或
`**perl joomscan.pl --url www.example.com -r**`

 **## **OWASP Joomla 漏洞扫描器简介**

[https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed](https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/rezasp/joomscan)**