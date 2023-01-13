# Hostintel:为恶意主机收集情报的模块化 Python 应用程序

> 原文：<https://kalilinuxtutorials.com/hostintel-collect-malicious-hosts/>

Hostintel 用于为主机收集各种情报来源。Hostintel 以模块化方式编写，因此可以轻松添加新的情报源。

主机由 FQDN 主机名、域或 IP 地址来标识。这个工具目前只支持 IPv4。输出是 CSV 格式的，并被发送到 STDOUT，这样数据可以被保存或通过管道传输到另一个程序。

由于输出是 CSV 格式，Excel 等电子表格或数据库系统将能够轻松地导入数据。

**也念:[反向壳小抄 2019](https://kalilinuxtutorials.com/reverse-shell-cheat-sheet/)**

[https://www.youtube.com/embed/aYK0gILDA6w?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/aYK0gILDA6w?feature=oembed&enablejsapi=1)

**short introduction for this tool**

这适用于 Python v2，但也应该适用于 Python v3。如果您发现它不能与 Python v3 一起工作，请发布问题。

**帮助屏幕:**

$ python hostintel.py -h
用法:host Intel . py[-h][-a][-d][-v][-p][-s][-c][-t][-o][-I][-r]
配置文件输入文件
查找主机智能信息的模块化应用程序。将 CSV 输出到 STDOUT。该应用程序在完成所有输入之前不会输出信息。
位置参数:
ConfigurationFile 配置文件
InputFile 输入文件，每行一个主机(IP，域，或 FQDN
主机名)
可选参数:
-h，–help 显示此帮助消息并退出
-a，–All 执行所有查找。
-d，–DNS DNS 查找。
-v，–病毒总量病毒总量查找。
-p，–passive total passive total 查找。
-s，–shod an shod an 查找。
-c，–Censys Censys 查找。
-t，–威胁人群威胁人群查找。
-o，–otx OTX 通过 AlienVault 查找。
-i，–isc 互联网风暴中心 DShield 查找。
-r，–carrier 使用回车在 csv 上换行。

**安装**:

首先，确保您的配置文件对于您的计算机/安装是正确的。在配置文件中添加适当的 API 键和用户名。

运行此工具需要 Python 和 Pip。有些模块必须从 GitHub 安装，所以要确保 git 命令可以从命令行使用。

Git 易于在任何平台上安装。接下来，安装 python 需求(每次获取这个存储库时运行这个需求):

$ pip 安装-r 要求. txt

Mac OSX 上的 Python 股票版出现了一些问题(http://stack overflow . com/questions/31649390/Python-requests-SSL-handshake-failure)。您可能需要使用以下命令安装请求库的安全部分:

$ pip 安装请求[安全性]

**运行:**

$ python hostintel.py myconfigfile.conf myhosts.txt -a > myoutput.csv

您应该能够将 myoutput.csv 导入到任何数据库或电子表格程序中。

```
Note that depending on your network, your API key limits, and the data you are searching for, this script can run for a very long time! Use each module sparingly! In return for the long wait, you save yourself from having to pull this data manually.
```

**样本数据:**

“sample data”目录中有一些示例数据。IP、域名和主机是随机挑选的，绝不是针对任何组织或个人。对样本数据运行此工具的方式如下:

**小主机列表:**

$ python host Intel . py local/config . conf sampledata/small list . txt-a > sampledata/small list . CSV
***处理 8.8.8.8 * * *
* * *处理 8.8.4.4 * * *
* * *处理 192.168.1.1 ***
***处理 10.0.0.1 ***
***处理 google.com * * *
* * *处理 212.227.247.242 * * *
* * *写输出* * *

**大型主机列表:**

$ python host Intel . py local/config . conf sampledata/larger list . txt-a > sampledata/larger list . CSV
* * *处理 114.34.84.13 * * *
* * *处理 116.102.34.212 * * *
* * *处理 118.75.180.168 * * *
* * *处理 123.195.184.13 * * *
* * *处理 14.110.216.236 * * *
* * *处理 14.173.147.69 * * *
* * *处理 14.181.192.151 * * *
* * *处理 146.120.11.66 * * *
* * *处理 163 . 172 . 149 . 131 * * *
…
* * *处理 54.233

[**Download**](https://github.com/keithjjones/hostintel)