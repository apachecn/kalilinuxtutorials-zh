# Adapt:一个为 WebApps 执行自动化渗透测试的工具

> 原文：<https://kalilinuxtutorials.com/adapt-automated-penetration-testing/>

ADAPT 是一个为 web 应用程序执行自动化动态应用程序渗透测试的工具。它旨在提高渗透测试工作的准确性、速度和信心。

自动调整对多个行业标准 OWASP 十大漏洞的测试，并根据这些潜在漏洞输出分类结果。

ADAPT 还使用 OWASP ZAP 的功能来执行自动主动和被动扫描以及自动蜘蛛搜索。由于 ADAPT 工具的灵活性，所有这些特性和测试都可以在配置文件中启用或禁用。

**又读:** [Killcast:操控你网络中的 Chromecast 设备](https://kalilinuxtutorials.com/killcast-chromecast-network/)

**安装**

*   点击[此处](https://github.com/secdec/ADAPT/releases)下载最新版本的 ADAPT。
*   通过终端提取适配器

**阿.塔尔-xvfz adapt.tar.gz**

*   打开一个新的终端(ctrl+alt+t)
*   导航到新解压缩的适配文件夹
*   a.确保您的环境可以访问网络
*   执行安装脚本(install.sh)
*   a.'类型'。/install.sh '
*   b.出现提示时，输入您的管理员密码
*   适配器现在应该可以进行配置了

它是如何工作的？

ADAPT 使用 Python 创建了一个自动化框架，以使用行业标准工具(如 OWASP ZAP 和 Nmap)来执行可重复的、设计良好的程序，并获得预期的结果，从而创建一个易于理解的报告，列出在 web 应用程序中检测到的漏洞。

**自动化测试:**

*   OTG-IDENT-004-帐户枚举
*   OTG-AUTHN-001-测试通过加密通道传输的凭证
*   OTG-AUTHN-002-默认凭据
*   OTG-AUTHN-003-弱锁定机制测试
*   OTG-AUTHZ-001-目录遍历
*   OTG-配置-002-测试应用平台配置
*   OTG-配置-006-测试 HTTP 方法
*   OTG-CRYPST-001–测试弱 SSL/TLS 密码，传输层保护不足
*   OTG-CRYPST-002–填充甲骨文的测试
*   OTG-ERR-001-错误代码测试
*   OTG-ERR-002–测试堆栈跟踪
*   OTG 信息 002–网络服务器指纹识别
*   OTG-InP val-001–测试反射式跨站点脚本
*   OTG-因帕尔-002–测试存储的跨站点脚本
*   OTG-in pval-003–HTTP 动词篡改
*   OTG-SESS-001-会话管理模式测试
*   OTG-SESS-002-Cookie 属性

[**Download**](https://github.com/secdec/adapt)