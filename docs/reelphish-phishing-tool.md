# reel phish——一种实时双因素网络钓鱼工具

> 原文：<https://kalilinuxtutorials.com/reelphish-phishing-tool/>

ReelPhish 是一种实时双因素网络钓鱼工具。这个 ReelPhish 工具已经和 FireEye 博客一起发布了。博文可以通过[点击这里](https://www.fireeye.com/blog/threat-research/2018/02/reelphish-real-time-two-factor-phishing-tool.html)找到。

## **卷纸T3 的安装步骤**

*   需要最新版本的 Python 2.7.x。
*   安装 Selenium，这是运行浏览器驱动程序所需的依赖项。
    *   **pip install-r requirements . txt**
*   为您计划使用的所有网络浏览器下载浏览器驱动程序。二进制文件应该放在这个根目录中，命名方案如下。
    *   [**浏览器:**](http://www.seleniumhq.org/download/)
        *   下载 32 位 Windows IE 的 Internet Explorer 驱动程序服务器。解压缩文件，并将二进制文件重命名为:IEDriver.exe。
        *   为了使 Internet Explorer 驱动程序工作，请确保禁用保护模式。在 IE11 (64 位 Windows)上，必须创建注册表项“HKEY _ LOCAL _ MACHINE \ SOFTWARE \ wow 6432 node \ Microsoft \ Internet Explorer \ Main \ FEATURE control \ FEATURE _ BF cache”。在此项中，创建一个名为 iexplore.exe 的 DWORD 值，并将该值设置为 0。
        *   有关 Internet Explorer 要求的更多信息，请访问 www . github . com/selenium HQ/selenium/wiki/Internet Explorer driver
*   [**火狐:**](http://www.github.com/mozilla/geckodriver/releases/)
    *   下载用于 Windows 32 位的 Firefox GeckoDriver 的最新版本。解压缩文件，并将二进制文件重命名为:FFDriver.exe。
        *   在 Linux 系统上，下载 Firefox GeckoDriver 的 Linux 版本，将二进制文件重命名为: **FFDriver.bin** 。Linux 支持是实验性的。
    *   壁虎驱动有特殊要求。将 FFDriver.exe 复制到**geckodriver.exe**，并将其放入路径变量中。此外，将 firefox.exe 的**添加到路径变量中。**
*   [**铬:**](https://chromedriver.storage.googleapis.com/index.html?path=2.35/)
    *   下载用于 Windows 32 位的谷歌 Chrome 驱动程序的最新版本。解压缩文件，并将二进制文件重命名为:ChromeDriver.exe。
        *   在 Linux 系统上，下载 Linux 版本的 Chrome Web 驱动程序，并将二进制文件重命名为:ChromeDriver.bin。Linux 支持是实验性的。

**也可理解为[THC-SSL-DOS–针对安全网络服务器的 DOS 工具，用于测试 SSL 重新协商](http://kalilinuxtutorials.com/thc-ssl-dos/)**

 **ReelPhish 由两部分组成:钓鱼网站处理代码和这个脚本。可以根据需要设计网络钓鱼网站。/examplesitecode 中提供了示例 PHP 代码。示例代码将从 HTTP POST 请求中获取用户名和密码，并将其传输到钓鱼脚本。

网络钓鱼脚本侦听本地端口，并等待凭据包。一旦收到凭据，网络钓鱼脚本将打开一个新的 web 浏览器实例，并导航到所需的 URL(您将在其中输入用户凭据的实际站点)。凭据将由 web 浏览器提交。

处理钓鱼网站和该脚本之间通信的推荐方式是使用反向 SSH 隧道。这就是为什么示例 PHP 钓鱼网站代码向 **localhost:2135** 提交凭证的原因。

 ***   您必须使用–browser 参数指定要使用的浏览器。支持的浏览器包括 Internet Explorer(“–浏览器 IE”)、Firefox(“–浏览器 FF”)和 Chrome(“–浏览器 Chrome”)。Windows 和 Linux 都受支持。Chrome 需要最少的设置步骤。更多详情请参见上述安装说明。
*   您必须指定 URL。该脚本将导航到此 URL 并代表您提交凭据。
*   其他可选参数也是可用的。
    *   将日志记录参数设置为 debug(–logging debug)以记录详细事件
    *   设置提交参数(–submit)来定制被浏览器“点击”的元素
    *   设置覆盖参数(–override)以忽略缺少的表单元素
    *   设置 numpages 参数(–numpages)以增加身份验证页面的数量(请参见下一节)

## **支持多页面认证**

ReelPhish 支持多个身份验证页面。例如，在某些情况下，可能会在第二页上请求双因素认证码。要实现此功能，请确保将–numpages 设置为身份验证页面的数量。还要确保会话 ID 在您的钓鱼网站上被正确跟踪。会话 ID 用于在用户进行身份验证的每个步骤时跟踪用户。

在某些情况下，您可能需要从特定的身份验证页面中抓取特定的内容(如质询代码)。ReelPhish.py 中提供了注释掉的代码示例来执行一个抓取操作。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/fireeye/ReelPhish)****