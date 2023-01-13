# IOC Scraper:一个快速可靠的服务，使您能够提取 IOC

> 原文：<https://kalilinuxtutorials.com/ioc-scraper/>

[![](img/eeccf625d58f8d0f448c1386d45c7c5a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjusocuwpw2kKz0-PxbxHzbT552XoqBqhp22b_Gzw4bxekBnz9rlI2AVtzd2TnwmIYqbGNbJwgPkcCe_qOYqa9rhcDROoMeCx9DJVfZ7ayNUHT28iWqJNUMcs5UGYLGmcSqJyJKyvkZW9ywSu5BSbe-Y-PxSLYQ18_1aUyBKOzrS8Tb4dWiKAzOVvW3/s728/image_380x226_61b5ca6ddcd3b.png)

**IOC Scraper** 利用 IOCPARSER 服务从不同供应商的博客、pdf 和 CSV 文件中获取 IOC。解析 IOC 是一个耗时的过程，使用当前脚本可以很容易地自动提取和聚集 IOC。

## 特性

*   缺省 IOC:支持提取和缺省 IOC。
*   白名单 IOC:支持 IOC 的自定义白名单。
*   来源类型:支持各种来源，如博客、pdf、CSV 等等。

## 支持的 IOC 类型

IOC Scraper 支持多种 IOC 类型。

| IOC 类型 | 状态 |
| --- | --- |
| 法国核安全局 | 支持 |
| IPv4, IPv6 | 支持 |
| URL，域 | 支持 |
| 电子邮件 | 支持 |
| MD5，SHA1，SHA256，文件名 | 支持 |
| mac 地址 | 支持 |
| ATT 和 CK 身份证 | 支持 |
| YARA 规则 | 支持 |

## 安装

**git 克隆 https://www.github.com/chaitanyakrishna/iocscraper.git
pip 3 install-f requirements . txt**

**用途**

**python IOC _ scraper . py-h
_ *|*|*/*\/*| _ _*_*_*_*_
| | | | ^ _ ^ _ ^ _ ^ _ ^ _ ^ _ ^/*` | '*\/_ \ ' | | |*| | |**)|(*|*)/_ |*| |
| _ |
用法:IOC _ Scraper . py[-h][-u URL][-uL FILE _ CONTAINING _ URLS][-t time out][-th thread number]-o OUTPUT
IOC _ Scraper v 1.0
可选参数:
-h，–帮助显示此帮助消息并退出
-u URL，–获取 IOCs 的 URL 单个 URL
-uL FILE _ CONTAINING _ URLS，–URL-list FILE _ CONTAINING
-t 超时，–time out 超时 HTTP 请求超时。default=60
-th THREADNUMBER，–thread thread Number 并行 HTTP 请求数。default=100
必需参数:
-o OUTPUT，–OUTPUT 输出文件名。*****

**示例命令行参数**

**python IOC scraper . py-u " http://targeturl . com "-o report
python IOC scraper . py-uL URLs . txt-o report**

**输出**

**python IOC _ scraper . py-uL URL _ list . txt-o report
*_ _
|*_ _*/*\/*|*_ _*_ _*_*_
| | | | | ^ _ _ ^ _ ^ _ ^ '/*` | '*\/_ \ ' | |*| |**)(|)/_ |*| |
| _ |
[日期:20-01-2022][时间:23:03:09][信息]启动 IOC 刮刀…
[*]progress bar:14/14[从:thehackernews.com 获取 IOC][错误:0]…0]…
[日期:20-01-2022][时间:23:03:13][信息]删除重复项…【日期:[日期:20] 从以下域获取 IOC
blog.aquasec.com
nationalcybersecurity.com
cofense.com
thehackernews.com
blog.sucuri.net
threats.amnpardaz.com
www.crowdstrike.com
www.bleepingcomputer.com
forensicitguy . github . io
marcuseddmondson . com
rajhackingarticles . blogspot . com
research . check point . com
www . Reddit . com
www . zero fox . com
日期:20-01 危害统计指标
域:52
URL:26
IP v4:15
IPv6:0
ASN:0
FILE _ HASH _ MD5:24
FILE _ HASH _ SHA1:16
FILE _ HASH _ sha 256:3
MITRE _ ATTACK:4
EMAIL:3
CVE:7
FILE _ NAME:59
YARA _ RULE:0【1***

[**Download**](https://github.com/chaitanyakrishna/iocscraper#output)