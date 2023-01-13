# Beef:浏览器开发框架项目

> 原文：<https://kalilinuxtutorials.com/beef-browser-exploitation-framework/>

**牛肉**是**浏览器开发框架**的简称。它是一个专注于网络浏览器的渗透测试工具。

随着对针对客户端(包括移动客户端)的网络攻击的担忧日益增加，BeEF 允许专业渗透测试人员通过使用客户端攻击向量来评估目标环境的实际安全状况。

与其他安全框架不同的是，BeEF 越过了加固的网络边界和客户端系统，并在一扇敞开的门:web 浏览器的上下文中检查可利用性。

BeEF 将挂接一个或多个 web 浏览器，并使用它们作为启动定向命令模块的滩头阵地，并从浏览器上下文中对系统进行进一步攻击。

**又读:[滚筒筛:筛选嵌入式设备文件，识别潜在的易受攻击指标](https://kalilinuxtutorials.com/trommel-embedded-vulnerable-indicators/)**

**要求**

*   操作系统:Mac OSX 10.5.0 或更高版本/现代 Linux。注意:不支持 Windows。
*   [Ruby](http://ruby-lang.org) : 2.4 或更新版本
*   [SQLite](http://sqlite.org) : 3.x
*   [Node.js](https://nodejs.org) : 6 或更新版本
*   [宝石文件](https://github.com/beefproject/beef/blob/master/Gemfile)中列出的宝石:
*   OSX 上需要 Selenium: brew 安装 selenium-server-standalone。

**快速启动**

以下是给不耐烦的人看的。

安装脚本安装所需的操作系统包和所有必备的 Ruby gems:

**$。/安装**

有关完整的安装详细信息，请参考 INSTALL.txt。

我们在维基上还有一个安装页面。

成功安装后，请务必阅读 wiki 上的配置页面，了解有关配置和保护 BeEF 的重要详细信息。

**用途**

要开始，只需执行 beef 并按照说明操作:

**$。/牛肉**

[https://www.youtube.com/embed/xdbvU_U42kY?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/xdbvU_U42kY?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/beefproject/beef)