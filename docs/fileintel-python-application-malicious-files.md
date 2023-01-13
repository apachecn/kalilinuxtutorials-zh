# Fileintel:一个模块化的 Python 应用程序，用于获取关于恶意文件的情报

> 原文：<https://kalilinuxtutorials.com/fileintel-python-application-malicious-files/>

[![Fileintel : A Modular Python Application To Pull Intelligence About Malicious Files](img/d835259882dbd940eba4b395efa5f7b0.png "Fileintel : A Modular Python Application To Pull Intelligence About Malicious Files")](https://1.bp.blogspot.com/-XmoIsOQXEHA/XfDQZSc1jbI/AAAAAAAAD5w/mzui1hcQqQ8qXX_xKP74STBUKKbLmPruQCLcBGAsYHQ/s1600/malware.png)

Fileinel 是一个工具，用于收集给定文件的各种情报来源。Fileintel 是以模块化的方式编写的，因此可以很容易地添加新的情报源。

文件由文件哈希(MD5、SHA1、SHA256)识别。输出是 CSV 格式的，并被发送到 STDOUT，这样数据可以被保存或通过管道传输到另一个程序。由于输出是 CSV 格式，Excel 等电子表格或数据库系统将能够轻松地导入数据。

这适用于 Python v2，但也应该适用于 Python v3。如果您发现它不能与 Python v3 一起工作，请发布问题。

这段代码已经在 Windows 7 和 Mac OSX 埃尔卡皮坦上测试过。如果您在任何其他类型的机器上尝试这个，请让我；

**$ python fileintel.py -h
用法:file Intel . py[-h][-a][-v][-n][-o][-t][-r]
配置文件输入文件**

模块化应用查找文件情报信息。将 CSV 输出到
STDOUT。

**位置参数:**
ConfigurationFile 配置文件
InputFile 输入文件，每行一个 hash(MD5，SHA1，SHA256)

**可选参数:**
-h，–help 显示此帮助消息并退出
-a，–All 执行所有查找。
-v，–病毒总量病毒总量查找。
-n，–NSRL NSRL 仅查找 SHA-1 和 MD5 哈希！
-o，–otx OTX 通过 AlienVault 查找。
-t，–threat crowd threat crowd 仅用于 SHA-1 和 MD5 哈希的查找！
-r，–carrier 使用回车在 csv 上换行。

**也可阅读-[CAINE 11–GNU/Linux Live 发行版](https://kalilinuxtutorials.com/caine-gnu-linux-live-distribution/)**

**安装**

首先，确保您的配置文件对于您的计算机/安装是正确的。在配置文件中添加适当的 API 键和用户名。

运行此工具需要 Python 和 Pip。有些模块必须从 GitHub 安装，所以要确保 git 命令可以从命令行使用。Git 易于在任何平台上安装。接下来，安装 python 需求(每次获取这个存储库时运行这个需求):

**$ pip install-r requirements . txt**

Mac OSX 上的股票版 Python 出现了一些问题([http://stack overflow . com/questions/31649390/Python-requests-SSL-handshake-failure](http://stackoverflow.com/questions/31649390/python-requests-ssl-handshake-failure))。您可能需要使用以下命令安装请求库的安全部分:

**$ pip 安装请求【安全】**

**NSRL**

如果您正在使用 NSRL 数据库查找，下载 NSRL“最小”数据集作为一个 zip 文件。将它放在您可以访问的目录中，并将您的配置文件指向该 zip 文件。没有必要解压缩 NSRL 数据。

7Zip

如果您想使用 7Zip(快速)而不是内部 Python zip 库(慢速)来读取大型 NSRL zip 文件，您将需要安装 7Zip。Windows 安装 7Zip 相当简单，但 Mac OX X 或 Linux 将需要安装 p7zip，即命令行工具。对于 Mac OS X，您可以在 Brew 中安装该工具。一旦安装了 7Zip，您需要将您的配置文件指向 7z 可执行文件所在的位置。

**虚拟人**

最后，我是 Python 的 virtualenv 的粉丝。要定制 Python 的本地安装来运行这个工具，我推荐你阅读:
[http://docs.python-guide.org/en/latest/dev/virtualenvs/](http://docs.python-guide.org/en/latest/dev/virtualenvs/)

**运行中**

**$ python file Intel . py my configfile . conf my hashes . txt-a>my output . CSV**

您应该能够将 myoutput.csv 导入到任何数据库或电子表格程序中。

> **请注意，根据您的网络、您的 API 密钥限制以及您正在搜索的数据，该脚本可能会运行很长时间！节约使用每个模块！作为长时间等待的回报，您不必手动提取这些数据。**

**样本数据**

“sample data”目录中有一些示例数据。这些散列是随机选取的，绝不是针对任何组织或个人的。对样本数据运行此工具的方式如下:

**较小列表:**

$ python file Intel . py local/config . conf sampledata/small erlist . txt-a > sampledata/small erlist . CSV
INFO:使用 7Zip from: /usr/local/bin/7z
预处理 NSRL 数据库…请稍候…
******* 处理 275 a 021 bbfb 6489 e 54d 471899 f 7 db 9d 1663 fc 695 EC 2 Fe 2 a 2c 4538 aabf 651 FD 0f*** * ***
* * *处理 001025 c 6d 4974 FB 2 cbea 56 f 710282 ACA 6 c 1353 cc 7120d 5d 4 a 78536888088499 加工 0322 a0ba 58 b 95 db 9 a 2227 F12 d 193 fdde a 74 cf 89*** * ***
*** * ***加工 e 02 ce 6d 73156 a 11 ba 84 a 798 b 26 de 1d 12*** * ***
*** * ***加工 B4 ed 7 aeda CD 28 cbbde 6978 FB 09 c 22 c 75*** * ***

 ****大列表:**

$ python file Intel . py local/config . conf sampledata/larger list . txt-a > sampledata/larger list . CSV
INFO:使用 7Zip from: /usr/local/bin/7z
预处理 NSRL 数据库…请稍等…
***处理 275 a 021 bbfb 6489 e 54d 471899 f 7 db 9d 1663 fc 695 EC 2 Fe 2 a 2c 4538 aabf 651 FD 0 f * * *
* * *处理 001025 c6d 4974 FB 2 cbea 56 f 710282 ACA 6 c 1353 cc 7120d 5d 4 a 7853688084953 a * * *
* * *处理 CEEF161D68AE2B6

**情报来源**

*   VirusTotal(需要公共 API 密钥和网络 I/O，在适当的时候进行节流)
    *   [http://www.virustotal.com](http://www.virustotal.com)
*   NSRL 数据库
    *   [http://www.nsrl.nist.gov/Downloads.htm](http://www.nsrl.nist.gov/Downloads.htm)
*   ThreatCrowd(需要网络 I/O，在适当的时候节流)
    *   [http://www.threatcrowd.org](http://www.threatcrowd.org)
*   AlienVault 的 OTX(需要 API 密钥和网络 I/O)
    *   [https://otx.alienvault.com](https://otx.alienvault.com)
*   威胁专家(需要网络 I/O)
    *   [http://www.threatexpert.com/](http://www.threatexpert.com/)

**资源**

*   VirusTotal Python 库
    *   [https://github.com/blacktop/virustotal-api](https://github.com/blacktop/virustotal-api)
*   NSRL 数据库
    *   [http://www.nsrl.nist.gov/Downloads.htm](http://www.nsrl.nist.gov/Downloads.htm)
    *   [https://blog . Didier Stevens . com/2015/09/01/NSRL-py-using-the-reference-data-set-of-the-national-software-reference-library/](https://blog.didierstevens.com/2015/09/01/nsrl-py-using-the-reference-data-set-of-the-national-software-reference-library/)
*   ThreatCrowd Python 库
    *   [https://github.com/threatcrowd/ApiV2](https://github.com/threatcrowd/ApiV2)
    *   [https://github.com/jheise/threatcrowd_api](https://github.com/jheise/threatcrowd_api)
*   OTX Python 图书馆
    *   [https://github.com/AlienVault-Labs/OTX-Python-SDK](https://github.com/AlienVault-Labs/OTX-Python-SDK)
    *   [https://otx.alienvault.com/api/](https://otx.alienvault.com/api/)
*   威胁专家
    *   使用美丽吸盘的刮刀
        *   [https://www.crummy.com/software/BeautifulSoup/bs4/doc](https://www.crummy.com/software/BeautifulSoup/bs4/doc)
    *   使用请求库的 Web 请求
        *   [http://docs.python-requests.org/en/master/](http://docs.python-requests.org/en/master/)
    *   [http://www.threatexpert.com/](http://www.threatexpert.com/)

[**Download**](https://github.com/keithjjones/fileintel)**