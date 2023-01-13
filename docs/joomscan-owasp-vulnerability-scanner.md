# joomscan-OWASP Joomla 漏洞扫描器项目

> 原文：<https://kalilinuxtutorials.com/joomscan-owasp-vulnerability-scanner/>

OWASP Joomla！漏洞扫描器或 JoomScan 是一个开源项目，旨在自动执行 Joomla CMS 部署中的漏洞检测和可靠性保证任务。

这个工具是用 Perl 实现的，能够无缝、轻松地扫描 Joomla 安装，同时以其轻量级和模块化的架构留下最小的足迹。它不仅能够检测已知的攻击性漏洞，还能够检测许多错误配置和管理员级别的缺陷，这些缺陷可能会被对手利用来危害系统。

此外，它提供了一个用户友好的界面，并以文本和 HTML 格式编制最终报告，以方便使用和最大限度地减少报告开销。它包含在 Kali Linux 发行版中。

**也读** [**从公共 WiFi 上网有多安全？**](https://kalilinuxtutorials.com/how-to-use-public-wifi/)

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

## **JOOMSCAN 用法示例**

做默认检查…
`**perl joomscan.pl --url www.example.com**`
或
**`perl joomscan.pl -u www.example.com`**

列举已安装的组件…
`**perl joomscan.pl --url www.example.com --enumerate-components**`
或
`**perl joomscan.pl -u www.example.com --ec**`

设置 cookie
`**perl joomscan.pl --url www.example.com --cookie "test=demo;"**`

设置用户代理
`**perl joomscan.pl --url www.example.com --user-agent "Googlebot/2.1 (+http://www.googlebot.com/bot.html)"**`
或
**`perl joomscan.pl -u www.example.com -a "Googlebot/2.1 (+http://www.googlebot.com/bot.html)"`**

设置随机用户代理
**`perl joomscan.pl -u www.example.com --random-agent`**
或
`**perl joomscan.pl --url www.example.com -r**`

设置代理
**`perl joomscan.pl --url www.example.com --proxy http://127.0.0.1:8080`**
或
`**perl joomscan.pl -u www.example.com --proxy https://127.0.0.1:443**`

更新 Joomscan…
`**perl joomscan.pl --update**`

## **视频**

[https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed](https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/rezasp/joomscan)