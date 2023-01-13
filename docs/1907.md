# SharpWebServer : HTTP 和 WebDAV 服务器，具有网络 NTLM 散列捕获功能

> 原文：<https://kalilinuxtutorials.com/sharpwebserver/>

[![SharpWebServer : HTTP And WebDAV Server With Net-NTLM Hashes Capture Functionality](img/ab888dee3669730adf1526d3453c4320.png "SharpWebServer : HTTP And WebDAV Server With Net-NTLM Hashes Capture Functionality")](https://1.bp.blogspot.com/-b_Mqz0e4_O4/YM4Cp0HFnoI/AAAAAAAAJm4/gFnRqc8qDxYJLLj2umEbQsAegZP4Q-9IgCLcBGAsYHQ/s728/SharpWebServer%25281%2529.png)

SharpWebServer 是一个面向红队的简单的 **HTTP & WebDAV** 服务器，用 C#编写，具有捕获网络 NTLM 散列的功能。用于为受损机器上的有效负载提供横向移动服务。

需要。NET Framework 4.5 和*System.Net*和*系统。Net.Sockets* 引用。

**用途**

**:: SharpWebServer ::
一个面向红队的 C#简单 HTTP 服务器，具有 Net-NTLMv1/2 哈希捕获功能
作者:
–Can güney aksa kalli(github.com/aksakalli)–原始实现
–Harry Patrick 442(github.com/harrypatrick442)–aksa kalli 的 fork &更改
–Dominic Chell(@ DOM Chell)来自 MDSec–Net-NTLM v2 哈希捕获从 Farmer 借来的代码
–Mariusz b ./mge eky，–合并所有建筑
在 NTLM 认证中增加了连接保持活动
用法:
SharpWebServer.exe[dir = path][verbose = true][NTLM = true][log file = path]
选项:
Port–监听的 TCP 端口号(1-65535)
dir–包含要托管的文件的目录。
详细–打开详细模式。
秒–指定服务器应该运行多长时间。默认:无限期
ntlm–在提供文件之前要求 NTLM 身份验证。用于收集 NetNTLMv2 哈希
(MDSec 的农民风格)
日志文件-输出日志文件的路径。**

**例子**

同时提供文件服务和捕获网络 NTLM 哈希的示例用例:

**服务器**

**C:>SharpWebServer.exe port = 8888 dir = C:\ Windows \ Temp verbose = true NTLM = true
::SharpWebServer::
一个面向红队的 C#简单 HTTP & WebDAV 服务器，具有 Net-NTLM 哈希捕获功能
。]服务 HTTP 服务器的端口:8888
[。]会运行这么长:60 秒
。]详细模式已打开。
【。] NTLM 模式开启。
【。]从目录中提供文件:C:\ Windows \ Temp
sharp webserver[29 . 03 . 21，17:55:14] NTLM:由于缺少授权头，发送 401 未经授权。
SharpWebServer [29.03.21，17:55:14]::1-" GET/test . txt "-len:0(401)
sharp webserver[29 . 03 . 21，17:55:14] NTLM:用 NTLM 挑战响应发送 401 未授权。
SharpWebServer [29.03.21，17:55:14]::1-" GET/test . txt "-len:0(401)
[+]sharp webserver:Net-NTLM 哈希捕获:
TestUser:::1122334455667788:66303 ee 2 df 9417 e 2 Fe 07 E1 b 7 FD 663205:010000000000**

**客户端**

**C:>curl-sD-HTTP://localhost:8888/test . txt–NTLM–negotiate-u TestUser:test password
HTTP/1.1 401 未授权
传输-编码:chunked
WWW-Authenticate:NTLM
日期:2021 年 3 月 29 日星期一 15:55:14 GMT
HTTP/1.1 401 未授权
传输-编码:chunked
WWW-Authenticate:NTLM TL**

**WebDAV 客户端**

**C:>dir \ localhost @ 8888 \ test
drive \ localhost @ 8888 \ test 中的卷没有标签。
卷序号为 0000-0000
目录\ localhost @ 8888 \ test
30 . 03 . 2021 05:12。2021 年 3 月 30 日 05 时 12 分..30 . 03 . 2021 04:27 11 test2 . txt
30 . 03 . 2021 05:12 12 test3 . txt
30 . 03 . 2021 05:12 test4
2 个文件 23 个字节
3 个目录 225 268 776 960 个可用字节
C:>type \ localhost @ 8888 \ 888
C:>copy \ localhost @ 8888 \ test \ test 4 \ test 5 . txt。
复制了 1 个文件。**

[**Download**](https://github.com/mgeeky/SharpWebServer)