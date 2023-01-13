# CobaltStrikeParser:用于 CobaltStrike 信标配置的 Python 解析器

> 原文：<https://kalilinuxtutorials.com/cobaltstrikeparser/>

[![](img/5fed08cc0967fcc3a29bb1c7ce7c9a50.png)](https://1.bp.blogspot.com/-mWE_rLyLFXg/YTLr_3v4jTI/AAAAAAAAKsA/R_XknrGoKSk-Mqo-PtLct_yyeu5VD6vVgCLcBGAsYHQ/s1194/CobaltStrike%2B%25281%2529.png)

**CobaltStrikeParser** 是用于 CobaltStrike Beacon 配置的 Python 解析器。

在 metasploit 兼容模式下，将`**parse_beacon_config.py**`用于无阶段信标、内存转储或 C2 URL(默认为 true)。
许多无级信标是 PE，其中信标代码本身存储在`**.data**`部分，并与 4 字节密钥进行异或运算。
脚本尝试启发式地找到 xor 密钥和数据，解密数据并从中解析配置。

这是专门设计的，所以它也可以用作图书馆。

repo 现在还包括一个小型通信模块(comm.py ),可以作为信标帮助与 C2 服务器通信。

**用途**

**用法:parse _ Beacon _ config . py[-h][–JSON][–quiet][–VERSION 版本] beacon
从 PE、内存转储或 URL 解析 CobaltStrike Beacon 的配置。
位置参数:
beacon 这可以是文件路径或 url(如果以 http/s 开头)
可选参数:
-h，–help 显示此帮助消息并退出
–JSON Print as JSON
–quiet 不打印缺失或空的设置
–VERSION Try as specific cobalt VERSION(3 或 4)。如果未指定，则两者都尝试。**

**号外**

要使用通信 poc，请将其复制到主文件夹，并从那里运行。要在 Windows 上安装 M2Crypto 库(poc 的一个要求),最简单的方法是使用在线安装程序，而不是通过 pip。

[**Download**](https://github.com/Sentinel-One/CobaltStrikeParser)