# joomscan-OWASP Joomla 漏洞扫描器项目

> 原文：<https://kalilinuxtutorials.com/joomscan-owasp/>

OWASP JoomScan 是一个用 perl 编程语言编写的开源项目，用于检测 Joomla CMS 漏洞并进行分析。如果你想在 Joomla CMS 上做渗透测试，OWASP JoomScan 是你最好的选择！这个项目比以往任何时候都更快，并更新了最新的 Joomla 漏洞。

## **安装**

```
git clone https://github.com/rezasp/joomscan.git
cd joomscan
perl joomscan.p
```

**也读作[CuckooDroid——用布谷鸟沙箱](https://kalilinuxtutorials.com/cuckoodroid-android-malware/)** 进行自动化安卓恶意软件分析

## **Joomscan 参数**

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

## **OWASP Joomscan 示例**

**做默认检查**
`**perl joomscan.pl --url www.example.com**`
或
`**perl joomscan.pl -u www.example.com**`

**枚举已安装的组件**
`**perl joomscan.pl --url www.example.com --enumerate-components**`
或
`**perl joomscan.pl -u www.example.com --ec**`

**设置 cookie**
`**perl joomscan.pl --url www.example.com --cookie "test=demo;"**`

**设置用户代理**
`**perl joomscan.pl --url www.example.com --user-agent "Googlebot/2.1 (+http://www.googlebot.com/bot.html)"**`
或
`**perl joomscan.pl -u www.example.com -a "Googlebot/2.1 (+http://www.googlebot.com/bot.html)"**`

**设置随机用户代理**
`**perl joomscan.pl -u www.example.com --random-agent**`
或
`**perl joomscan.pl --url www.example.com -r**`

**更新 Joomscan**
`**perl joomscan.pl --update**`

## **视频**

[https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed](https://www.youtube.com/embed/Ik2CJ9LkuoI?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/rezasp/joomscan)