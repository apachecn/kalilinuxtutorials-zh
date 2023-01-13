# ScriptHunter:在网站上查找 JavaScript 文件的工具

> 原文：<https://kalilinuxtutorials.com/scripthunter/>

[![ScriptHunter : Tool To Find JavaScript Files On Websites](img/8e1df18d518e38ba5db5747330cb9a9b.png "ScriptHunter : Tool To Find JavaScript Files On Websites")](https://1.bp.blogspot.com/-3e1-wIOXoxE/X7Lsp4LZcBI/AAAAAAAAIAI/a6qZxS35gaQrVIA8fJPjc3Ay8IS9GltEQCLcBGAsYHQ/s728/scripthunter-1%25281%2529.png)

**Scripthunter** 是一款为给定网站查找 javascript 文件的工具。要扫描谷歌，只需运行`**./scripthunter.sh https://google.com**`。请注意，这可能需要一段时间，这就是为什么 scripthunter 还实现了一个通知机制，通过 Telegram API 通知您扫描何时完成。[博文](https://blog.r0b.re/hacking/pentesting/bugbounty/recon/web/js/2020/06/30/scripthunter-automated-js-discovery.html)

**设置**

要安装 scripthunter，请克隆此存储库。Scripthunter 需要安装一些工具，所以请确保您已经安装了这些工具:

*   [高](https://github.com/lc/gau)
*   [ffuf](https://github.com/ffuf/ffuf)
*   [哈科勒](https://github.com/hakluke/hakrawler)
*   [httpx](https://github.com/projectdiscovery/httpx)
*   [展开](https://github.com/tomnomnom/unfurl)

请确保这些工具大部分都是用 Go 编写的，你已经正确安装和配置了 Go。请确保当您在终端中键入上述任何命令时，它们能够被识别并正常工作。

此外，scripthunter 使用 Telegram 在扫描完成后向您发送通知。要启用此功能，您需要创建一个电报 Bot，并将 Bot API 密钥和 chatid 粘贴到 scripthunter 脚本中。您可以按照[本](https://blog.r0b.re/automation/bash/2020/06/30/setup-telegram-notifications-for-your-shell.html)指南获取这些值。

![](img/f28865caa9c35a93187b41217b452c00.png)

**特性**

*   使用 Gau 和 Hakrawler 从网站提取公共 javascript 文件
*   从找到的公共文件中解析包含 js 文件的目录
*   使用 ffuf 和自定义单词表扫描 js 目录中隐藏的 js 文件
*   检查所有找到的文件的连通性
*   扫描完成后通知用户
*   将所有看到的 js 文件名聚合到一个全局单词列表中

[**Download**](https://github.com/robre/scripthunter)