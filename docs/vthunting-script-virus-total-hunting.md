# VTHunting:一个用于生成病毒总搜索报告的小脚本

> 原文：<https://kalilinuxtutorials.com/vthunting-script-virus-total-hunting/>

[![VTHunting : A Tiny Script Used to Generate Report About Virus Total Hunting](img/201c433873acf1f9e85a133cfd739d1d.png "VTHunting : A Tiny Script Used to Generate Report About Virus Total Hunting")](https://1.bp.blogspot.com/-lRNS_Bhb4nI/XPiEUdjvRYI/AAAAAAAAAqQ/BjPnDs8CVi4FYpqKJwhgzpwHQ2uW-0rCwCLcBGAs/s1600/VirusTotal%2BHunting%25282%2529.png)

VTHunting 是一个基于 VT api 版本 3 的小型工具，可以运行关于恶意软件狩猎的每日、每周或每月报告。报告可以通过电子邮件、空闲频道或电报发送。

该工具还可以在 cli 中使用，以便随时获取报告。默认的结果数是 10，但是可以在配置部分增加或减少。该工具仅适用于病毒总体智能 API。

**也可阅读-[聚敛:深入的 DNS 枚举和网络映射](https://kalilinuxtutorials.com/amass-dns-enumeration-network-mapping/)**

**报表示例**

以下摘录是生成报告的示例。

**McAfee ATR | Thomas Roccia | @ fr0 gger _
从 VirusTotal** 获取最新狩猎通知
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
2018-12-24 10:20:30.158831
**规则名称:**fancy bear _ ComputraceAgent
**比赛日期:**2018-12-24 17:33 apt 28]
———————————————
—**规则名称:**哈特曼 _ 编译 _python:哈特曼
**比赛日期:**2018-12-24 00:28:21
**sha 256:**14 c64 fc 93 AE 68 f 01989 db 992 BF 8 ee 4 e 4

**入门**

只需下载脚本:

**git 克隆 https://github.com/fr0gger/vthunting**

然后用 API 键和信息配置配置部分:

# **病毒总 API**
vt API = " "
number _ of _ result = " " # 10 默认设置

# **邮件配置**#
SMTP _ serv = " "
SMTP _ port = " "
Gmail _ log in = " "
Gmail _ pass = " " # pass from APP
Gmail _ dest = " "

**# Slack Bot config**
Slack _ Bot _ TOKEN = " "。

配置就绪后，您可以使用以下命令运行该文件:

**python vt hunting . py–help**

**用法:vthunting.py [OPTION]
-h，–帮助打印此帮助
-r，–report 打印 vthunting 报告
-s，–slack _ report 将报告发送到 Slack 通道
-e，–email _ report 通过 email 发送报告
-t，–Telegram _ report 将报告发送到 Telegram**

**先决条件**

**要求**

您首先需要安装需求:

*   要求
*   slackclient

**pip install-r requirements . txt**

**VT API**

从病毒总数中获取您的 API 密钥。[https://developers.virustotal.com/v3.0/reference](https://developers.virustotal.com/v3.0/reference)

**电子邮件配置(gmail)**

要创建一个应用程序，你可以在这里找到文档:[https://support.google.com/accounts/answer/185833](https://support.google.com/accounts/answer/185833)

**Slack Bot 配置**

要生成令牌，您需要转到这里并按照步骤:[https://api.slack.com/custom-integrations/legacy-tokens](https://api.slack.com/custom-integrations/legacy-tokens)

**电报机器人配置**

要获得令牌，您需要通过与@BotFather 对话来创建一个电报机器人，它将帮助您配置您的机器人并获得令牌。获得令牌后，请访问[https://api.telegram.org/bot](https://api.telegram.org/bot)<YOUR _ TOKEN>/get updates 获取频道 id。

**在您的系统中安装**

如果您想在任何地方访问该脚本，您可以将它复制到以下位置，而不需要扩展名:

**CP vt hunting . py/usr/local/bin/vt hunting**

**用 crontab** 配置任务调度器

您可以使用 crontab 运行脚本并定期接收报告。

**crontab -e**

[**Download**](https://github.com/fr0gger/vthunting)