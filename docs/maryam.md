# Maryam:开源智能(OSINT)框架

> 原文：<https://kalilinuxtutorials.com/maryam/>

[![Maryam : Open-source Intelligence(OSINT) Framework](img/19f62b21d91e01740e0058bd66a311fe.png "Maryam : Open-source Intelligence(OSINT) Framework")](https://1.bp.blogspot.com/-mSX9KxSPi3o/XncScuPtVZI/AAAAAAAAFnA/EMukiLYM630-HFa7526hb0unFN9sTq0GwCLcBGAsYHQ/s1600/Maryam%25281%2529.png)

OWASP Maryam 是一个开源智能(OSINT)和基于 Web 的足迹模块/工具框架，基于 Recon-ng，用 Python 编写。如果你有 Metasploit 或 Recon-ng 方面的技能，你可以很容易地使用它，没有先决条件。

[![](img/7b6c97f62ae3488847444ec395aee2ef.png)](https://asciinema.org/a/310985)

**也可阅读-[懒人码头工人:管理一切的懒惰方式码头工人](https://kalilinuxtutorials.com/lazydocker/)**

有什么办法？

**如果你想的话**

*   从搜索引擎中提取电子邮件、文档、子域名、社交网络
*   从网络资源中提取链接，CSS 和 JS 文件，CDN 链接，电子邮件，关键词
*   找到并蛮力 DNS，TLD 和重要的指示
*   抓取网页并搜索您的正则表达式
*   识别 WebApps、WAF、有趣和重要的文件
*   并得到几种格式报告

**安装**

**git 克隆 https://github.com/saeeddhqan/Maryam.git
CD 玛利亚姆
pip install -r 需求
chmod +x 玛利亚姆
。/玛丽亚姆**

**快速指南**

**获取帮助选项**

*   写**或`?`或**
*   或者写`**help <command-name>**`请求帮助你的命令

**显示模块**

*   写`**show modules**`

**使用模块**

*   写**或`load <module-name>`或**

**用于显示设置选项**

*   写`**show options**`

**用于设置一个选项**

*   写 **`set <option-name> <value>`**
*   例如 **`set VERBOSITY 2`**

**用于运行选定的模块**

*   写`**run**`

**用于添加一个变量**

*   写 **`var <$name> <value>`**
*   例如`**var $hunter_key XXXXXXXXXXXXXXXX**`
*   为使用它写 **`set HUNTER_KEY $hunter_key`**
*   为显示所有变量，编写`**var list**`命令
*   对于删除变量写 **`var delete <var-name>`**

**用于从模块输出中获取报告**

*   将“输出”选项设置为真:`**set output True**`
*   或者使用'–输出开关':`**wapps -d domain.com --output**`
*   接下来，使用`**report**`命令: **`report <format> <file-name-for-output> <module-name>`**
*   例如 **`report <format> pdf_docs osint/docs_search localhost`**

**显示历史命令**

*   写 **`history all`**

**进行模块搜索**

*   写 **`search <string>`**

**为记录命令**

*   写 **`record start <file-name>`**
*   **`record stop`**

**用于存储所有输出**

*   写 **`spool start <file-name>`**
*   为停止它`**spool stop**`

**用于文件**中的运行命令

*   写`**resource <commands-file-name>**`

**用于运行 shell 命令**

*   写`**shell <command>**`或`**! <command>**`或`**<command>**`

**用于重新加载所有模块**

*   写`**reload**`

**用于配置连接**

*   见选项:`**show options**`
*   并设置选项:`**set TIMEOUT 2.5**`

**为使用随机用户代理**

*   写 **`set RAND_AGENT true`**

[**Download**](https://github.com/saeeddhqan/Maryam)