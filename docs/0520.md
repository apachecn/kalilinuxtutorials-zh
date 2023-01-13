# ZeebSploit: Web 扫描器利用信息收集

> 原文：<https://kalilinuxtutorials.com/zeebsploit-web-scanner/>

ZeebSploit 是一款黑客工具，用于搜索网页信息和扫描网页漏洞。

**安装&使用**

**apt-get 安装 git
git 克隆 https://github.com/jaxBCD/Zeebsploit.git
CD Zeebsploit
chmod+x 安装
。/install
python 3 zeebsploit . py
为演出模块
键入“help ”,并遵循说明**

**也可阅读-[pocsuite 3:开源远程漏洞测试框架](https://kalilinuxtutorials.com/pocsuite3-open-sourced-remote-vulnerability/)**

**模块**

```
[Main modules]
+----------+-------------------------------+
| Modules  |          Description          |
+----------+-------------------------------+
| Exploit  |      Exploitation Modules     |
| Scanners |        Scanners Modules       |
|  infoga  | information Gathering Modules |
+----------+-------------------------------+

[Exploit Modules]
+---------------------------+--------------------------------------------------+
|          Modules          |                   Description                    |
+---------------------------+--------------------------------------------------+
|    wp content injection   | wordpress content injection version 4.7 or 4.7.1 |
|        wp revslider       |  wordpress plugin revslider remote file upload   |
|        wp learndash       |      wordpress leardash remote file upload       |
|         wp swhobiz        |   wordpress plugin showbiz remote file upload    |
|     joomla com fabrik     |       joomla component fabrik file upload        |
| joomla manager get config |     joomla component manager auto get config     |
|      joomla jdownload     |  joomla component jdownloads remote file upload  |
|          joomla           |  Joomla ads manager component auto shell upload  |
|     apache struts rce     |      CVE: 2017-5638 - Apache Struts2 S2-045      |
|                           |             remote command execution             |
|        drupal8 rce        |    drupal version 8 remote command execution     |
|  dvr cam leak credential  |              TBK DVR4104 / DVR4216               |
|                           |    - Credentials Leak (Get User and password     |
|     webdav file upload    |                     Nothing                      |
|         ---More---        |        Coming Soon the following version         |
+---------------------------+--------------------------------------------------+

[Scanner Module]
+--------------------+----------------------------------------+
|      Modules       |              Description               |
+--------------------+----------------------------------------+
| subdomain scanner  |         Scan Subdomain for Web         |
|    sqli scanner    |    Scan Sql Injection Vulnerability    |
|    xss scanner     |    Scan XSS Injection Vulnerability    |
|    lfi scanner     | Local File Includes Scanner etc/passwd |
| admin login finder |         Scan Admin Login page          |
| directory scanner  |   scan directory on web use dirhunt    |
| subdomain takeover |      scan type subdomain takeover      |
|     ---More---     |   Coming Soon the following version    |
+--------------------+----------------------------------------+

[Information Gathering]

+--------------------+------------------------------------------+
|      Modules       |               Description                |
+--------------------+------------------------------------------+
|    cms detector    |    a tool for detecting cms on a web     |
|    port scanner    |         Scan Open Port use Nmap          |
| information header |       response header information        |
|   ip geolocation   |   detect the location of an ip or host   |
|   email searcher   |         searching email from web         |
|     traceroute     | to show the route the package has passed |
| robot.txt detector |         Scan Robot.txt from Web          |
| header information |         Response Header Checker          |
|    whois lookup    |     looking for registered users or      |
|                    |  recipients of Internet resource rights  |
|     ---More---     |    Coming Soon the following version     |
+--------------------+------------------------------------------+
```

[**Download**](https://github.com/jaxBCD/Zeebsploit)