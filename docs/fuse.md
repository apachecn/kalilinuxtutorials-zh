# FUSE:一个用于发现文件上传错误的渗透测试工具

> 原文：<https://kalilinuxtutorials.com/fuse/>

[![](img/7c58b4a9acf0d8e0ced545df49d386b9.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgcLAkbrdHJT4UTqPzWa7EszOFnIhOLmFYH_qyJ-tCrbPgI4vLjqbCXoQMGOHqCKSB2Q-xi7D6YrKXiJkeYza4C5d_nG_A36TQ0HJk06f5_cVQpQ_nys_rvJ7EXcHxHiYprDh9BqIoYD12J6nDU7oVIOXTi9KIHXr3DPoNYVfb9urGpBlymTDS9KNFM=s720)

**FUSE** 是一个渗透测试系统，旨在识别无限制可执行文件上传(UEFU)漏洞。测试策略的细节在我们的论文“FUSE:通过渗透测试发现文件上传错误”中，该论文发表在 NDSS 2020 上。要了解如何配置和执行 FUSE，请参阅以下内容。

**设置**

**安装**

FUSE 目前在 Ubuntu 18.04 和 Python 2.7.15 上工作。

*   安装依赖项

# **apt-get 安装 rabbitmq-server
#apt-get 安装 python-pip
#apt-get 安装 git**

*   克隆和构建 FUSE

**$ git 克隆 https://github.com/WSP-LAB/FUSE
$ CD 熔丝&&pip install-r requirements . txt**

如果您计划使用 selenium 利用无头浏览器验证，请参考 [selenium 文档](https://selenium.dev/selenium/docs/api/py/index.html)安装 Chrome 和 Firefox web 驱动程序。

**用途**

**配置**

*   FUSE 使用用户提供的配置文件来指定目标 PHP 应用程序的参数。在测试目标 Web 应用程序之前，必须填写脚本。您可以查看自述文件和示例配置文件。
*   文件监视器的配置(可选)

**$ vim File MONITOR . py
…
10 MONITOR _ PATH = '/var/www/html/'<-目标应用程序的 Web 根
11 MONITOR_PORT=20174 < -文件监视器的默认端口
12 EVENT _ LIST _ LIMITATION = 8000<-EVENT _ LIST 中的最大元素数
…**

**执行**

*   融合

**$ python framework . py[配置文件的路径]**

文件监视器

**$ python filemonitor.py**

*   结果
    *   当 FUSE 完成渗透测试时，会创建一个[HOST]目录和一个[HOST_report.txt]文件。
    *   [主机]文件夹存储已尝试上传的文件。
    *   [HOST_report.txt]文件包含与触发 U(E)FU 的文件相关的测试结果和信息。

**简历**

如果你发现了 UFU 和 UEFU 的 bug 并通过运行 FUSE 得到 CVEs，请发一个 PR 给 README.md

| 应用 | 简历(cv) |
| --- | --- |
| Elgg | CVE-2018-19172 |
| ECCube3 | CVE-2018-18637 |
| CMSMadeSimple | CVE-2018-19419，CVE-2018-18574 |
| CMSimple | CVE-2018-19062 |
| 混凝土 5 | CVE-2018-19146 |
| GetSimpleCMS | CVE-2018-19420，CVE-2018-19421 |
| 子离子 | CVE-2018-19422 |
| OsCommerce2 | CVE 2018-18572，CVE 2018-18964，CVE 2018-18965，CVE 2018-18966 |
| 巨大的 | CVE 2018-6383，CVE 2018-18694 |
| 元素氙的符号 | XEVE-2019-001 |

[**Download**](https://github.com/WSP-LAB/FUSE)