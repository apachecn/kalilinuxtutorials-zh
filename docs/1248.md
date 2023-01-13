# HTTPS-无处不在:一个加密你的通信的浏览器扩展

> 原文：<https://kalilinuxtutorials.com/https-everywhere/>

[![HTTPS-Everywhere : A Browser Extension That Encrypts Your Communications](img/c560690d212beb4cf7ad93818f6d99cc.png "HTTPS-Everywhere : A Browser Extension That Encrypts Your Communications")](https://1.bp.blogspot.com/-xzwL44vSpCc/XnzNmt8ogSI/AAAAAAAAFo4/Hzc61LePmoYWYi0Wbz7OOEUyXhxvuiVqACLcBGAsYHQ/s1600/https-everywhere%25281%2529.png)

**HTTPS-无处不在**是一个浏览器扩展，可以加密你与许多提供 HTTPS 但仍允许未加密连接的网站的通信。

获取您需要的包，并安装一个 git 挂钩，以便在推送之前运行测试:

**bash install-dev-dependencies . sh**

运行规则集验证和浏览器测试:

**bash test.sh**

在独立的 Firefox 配置文件中运行最新的代码和规则集:

**bash test/Firefox . sh–just run**

在独立配置文件中为特定版本的 Firefox 运行最新的代码和规则集:

**FIREFOX =/path/to/FIREFOX bash test/FIREFOX . sh–just run**

**也读作-[令牌反向器:字表生成器破解安全令牌](https://kalilinuxtutorials.com/token-reverser/)**

在独立的 Chromium 配置文件中运行最新的代码和规则集:

**bash test/chromium . sh–just run**

在独立的 Tor 浏览器配置文件中运行最新的代码和规则集:

**bash test/tor-browser . sh path _ to _ tor _ browser . tar . xz**

构建 Firefox(。xpi) &铬(。crx)扩展:

**bash make.sh**

这两个构建命令都将其输出存储在 pkg/下。

**预交付测试**

通过启用预提交挂钩，可以自动运行可用的测试套件，该挂钩提供有:

**ln -s../../hooks/预提交。git/hooks/预提交**

**源树**

这是 Firefox 和 Chrome 的 HTTPS Everywhere 的源代码树。

你可能想知道的重要目录

chromium/ WebExtension 源代码(针对 Firefox & Chromium/chrome)
Chromium/External 外部依赖关系
chromium/test 单元测试

规则/符号链接到 src/chrome/content/rules

src/chrome/content/rules 规则集文件 live here

test/ Travis 单元测试源代码 live here

utils/各种实用程序(包括一些 Travis 测试源代码)

[**Download**](https://github.com/EFForg/https-everywhere)