# 0xsp Mongoose:权限提升枚举工具包(64/32)

> 原文：<https://kalilinuxtutorials.com/0xsp-mongoose-privilege-escalation-enumeration/>

[![0xsp Mongoose : Privilege Escalation Enumeration Toolkit (64/32 )](img/9e6494e6644dc81ed3c799544ea656ab.png "0xsp Mongoose : Privilege Escalation Enumeration Toolkit (64/32 )")](https://1.bp.blogspot.com/-jgLVrd21qW4/XWy-lNyiR7I/AAAAAAAACT4/0wbyTkUuEeoTHPEODs6rP7-DxEvVOPpzACLcBGAs/s1600/OXSP%2B%25281%2529.png)

使用**0x sp mongose**您将能够扫描目标操作系统的任何可能的权限提升攻击方式，从收集信息阶段开始，直到通过 0xsp Web 应用程序 API 报告信息。

用户将能够以高性能同时扫描不同的 Linux / windows 操作系统，而无需花费时间在终端或文本文件中查找所找到的内容，mongoose 允许您通过简单的 API 端点将这些信息直接发送到 web 应用程序友好的界面，从而缩短了这种方式。

项目分为两段`**server**` **&** `**agent**` **。**

`**server**`已经用 PHP( `**codeigniter**`)编码。你需要将这个应用程序安装到你的首选环境中，你可以在线或在你的本地主机上使用它。用户可以自由选择。也非常欢迎对增强功能贡献。

`**Agent**` 已被编码为 ELF，其中`**Lazarus Free Pascal**`将被释放(32，64 位)，同时在目标系统上执行`**Agent**` 以及所有需要的参数。用户可以自由决定是否愿意与`**Server App**`通信，以存储结果并方便地浏览它们。或者他也可以在没有 Web Api 连接的情况下运行该工具。

**也可以理解为-[Sudomy:使用 Bash 脚本](https://kalilinuxtutorials.com/sudomy-subdomain-enumeration-tool/)创建的子域枚举工具**

**Linux 代理使用情况**

*   确保给它可执行的权限`**chmod +x agent**`
*   。/agent -h(显示帮助说明)

-k-检查内核中常见的权限提升漏洞。
-u-获取关于用户、群组的信息，相关信息。
-c–检查 cronjobs。
-n-检索网络信息、接口等。
-w–枚举可写文件、目录、SUID、
-I–搜索 Bash、python、Mysql、Vim..etc 历史文件。
-f–搜索可访问的敏感配置文件&私有内容。
-o–连接到 0xsp Web 应用程序。
-p–通过在根目录下运行显示所有进程，检查易受攻击的包。e-内核检测工具，它将有助于在工具数据库中搜索内核漏洞。
-x–授权您与 WebApp API 连接的密钥(默认为 0xsp)。
-a–显示自述文件。

**Windows 代理使用情况**

-s-枚举活动的 Windows 服务、驱动程序..等等。
-u–获取关于用户、组、角色的信息，相关信息。
-c–搜索可访问的敏感配置文件&私有内容。
-n-检索网络信息、接口等。
-w–枚举可写目录、访问权限检查、修改权限。
-I–枚举 Windows 系统信息、会话和相关信息。
-l–通过特定的按键在任何文件中搜索，例如:agent.exe-l c:\ password * . config .
-o–连接 0xsp Mongoose Web 应用程序 API。
-p–枚举已安装的软件、正在运行的进程、任务。
-e–内核检查工具，它将帮助搜索工具数据库以查找 windows 内核漏洞
-x–密钥以授权您与 WebApp 的连接。
-d–将文件直接下载到目标机器。
-t–将文件从目标机器上传到 Mongoose Web 应用程序 API。[agent.exe-t 文件名 API secret key]
-m–一起运行所有已知的扫描类型。

**服务器网络应用**

*   确保至少有`**php 5.6 or above**`
*   需要`**mysql 5.6**`
*   确保在根路径`**/**`上添加文件夹名为`**0xsp**`的 Web 应用程序，如【http://localhost/0xsp/】，`**Agent**`将不会连接到它，如果配置不正确。`**agent**`仅在以下情况下连接:

**。/agent {扫描选项} -o localhost -x secretkey**

**web API 示例**

。/agent -c -o localhost -x 0xsp {枚举 CRON 任务并将结果传输到 Web Api}
。/agent -e -o localhost -x 0xsp {智能漏洞检测器}
。/agent -c -e localhost -x 0sxp {将同时运行两次扫描并直接发送找到的结果}
。/agent -m -o 10.10.13.1 -x 0xsp {一起运行所有扫描并将其导出到 Web API}

**没有 WebApi 的示例**

**。/agent -c -k -p {这将同时运行 3 次扫描，而不会将结果发送到 Web Api }**

**代理功能**

*   高性能、稳定性，执行时无延迟地产生输出结果
*   能够用智能技术执行大部分功能。
*   结果将被发送到快速 Web API
*   异常处理。
*   针对公开披露的漏洞的内置 Json 数据集。
*   像猫鼬一样快

[https://www.youtube.com/embed/lG3HS7a9sVc?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/lG3HS7a9sVc?feature=oembed&enablejsapi=1)

[https://www.youtube.com/embed/YRrnXPDVZlg?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/YRrnXPDVZlg?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/lawrenceamer/0xsp-Mongoose/)