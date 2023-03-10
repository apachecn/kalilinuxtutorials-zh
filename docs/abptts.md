# ABPTTS:用于 Web 应用服务器的基于 HTTP/HTTPS 的 TCP 隧道

> 原文：<https://kalilinuxtutorials.com/abptts/>

[![ABPTTS : TCP Tunneling Over HTTP/HTTPS For Web Application Servers](img/6d781d075ba75da021208ea6976a85a0.png "ABPTTS : TCP Tunneling Over HTTP/HTTPS For Web Application Servers")](https://1.bp.blogspot.com/-VhvOBm9lXiI/YLTmHYwxfSI/AAAAAAAAJRI/XoOKKBysLEgPpO7bBEA3VDt9N1LGUoTYwCLcBGAsYHQ/s728/ABPTTS%25281%2529.png)

ABPTTS 使用 Python 客户端脚本和 web 应用服务器页面/包[1]通过 HTTP/HTTPS 连接将 TCP 流量隧道传输到 web 应用服务器。换句话说，在任何可以部署 web shell 的地方，现在都应该能够建立完整的 TCP 隧道。这允许通过 web 应用服务器建立 RDP、交互式 SSH、Meterpreter 和其他连接。

这种通信被设计成完全符合 HTTP 标准，这意味着除了通过目标 web 应用服务器在中建立隧道*之外，它还可以用于通过数据包检测防火墙建立*出站*连接。*

许多新颖的特征被用于使其流量检测具有挑战性。除了对授权渗透测试人员有用之外，它还旨在为 IDS/WPS/WAF 开发人员提供一个安全、真实的恶意流量示例，该示例避开了过于简单的基于正则表达式模式的签名模型。

PDF 格式的内容丰富的手册将引导用户完成各种部署场景。

这个工具是在 GPL 版本 2 下发布的。

[1]目前包含 JSP/WAR 和 ASP.NET 服务器端组件。

比较和对比:

*   雷乔治([https://github.com/sensepost/reGeorg](https://github.com/sensepost/reGeorg))
*   Node.js 的 HTTP 隧道([https://github.com/johncant/node-http-tunnel](https://github.com/johncant/node-http-tunnel))

以冬虫夏草/冬虫夏草的斜指命名，例如:[http://www.insectimages.org/browse/detail.cfm?imgnum=0014287](http://www.insectimages.org/browse/detail.cfm?imgnum=0014287)

[**Download**](https://github.com/nccgroup/ABPTTS)