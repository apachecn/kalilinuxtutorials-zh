# Webtech:识别网站上使用的技术

> 原文：<https://kalilinuxtutorials.com/webtech/>

我们非常自豪地将 WebTech 作为开源软件发布。WebTech 是一个 Python 软件，它可以通过访问给定的网站、解析单个响应文件或重放文本文件中描述的请求来识别 web 技术。

这样你就可以得到可重复的结果，并最大限度地减少对目标网站的请求。

**也读作-[DNSDmpstr:DnsDumpster&黑客目标](https://kalilinuxtutorials.com/dnsdmpstr-dnsdumpster-hackertarget/)的非官方 API &客户端**

CLI 安装

网络技术可在 pip 上获得:

**pip 安装 webtech**

也可以通过 setup.py 安装:

**python setup . py install–用户**

**打嗝整合**

下载 Jython 2.7.0 standalone 并安装到 Burp 中。

在“扩展器”>“选项”>“Python 环境”中:

*   选择 Jython jar 位置

最后，在“扩展器”>“扩展”中:

*   点击“添加”
*   选择“py”或“Python”作为扩展格式
*   选择该文件夹中的 Burp-WebTech.py 文件

**用途**

**扫描网站:**

**$ web tech-u https://example.com/
目标网址:https://example.com
……
$ web tech-u file://response . txt
目标网址:
……**

**完全使用:**

**$ webtech -h
用法:web tech[选项]
选项:
-h，–帮助显示此帮助消息并退出
-u urlS，–URLS =要扫描的 URL URL
–ul = URLS _ FILE，–URLS-FILE = URLS _ FILE
要扫描的 URL 列表文件
–ua = USER _ AGENT，–USER-AGENT = USER _ AGENT
使用此用户代理
–rua，–random-random**

**数据库匹配资源**

*   [HTTP 头信息](http://netinfo.link/http/headers.html)
*   [饼干名称](https://webcookies.org/top-cookie-names)

[**Download**](https://github.com/ShielderSec/webtech)