# Thc Hydra:从远程系统获得未授权访问的工具

> 原文：<https://kalilinuxtutorials.com/thc-hydra/>

[![Thc Hydra : Tool To Gain Unauthorised Access From Remote To A System](img/56dd4d95cd907fb0d1a514d41c53aa60.png "Thc Hydra : Tool To Gain Unauthorised Access From Remote To A System")](https://4.bp.blogspot.com/-GVfG7LZDMHc/XObWGH0H3mI/AAAAAAAAAdQ/vrCt5ncSBbouU41kb57QDTwX9aMOxmu5QCLcBGAs/s1600/THC-Hydra%25281%2529.png)

每个密码安全研究都显示，最大的安全漏洞之一是密码。Thc Hydra 是一个概念验证代码，让研究人员和安全顾问有可能展示从远程获得对系统的未授权访问是多么容易。

此工具仅用于合法目的！

已经有一些登录黑客工具可用，但是，没有一个支持一个以上的攻击协议或支持并行连接。

经测试，它可以在 Linux、Windows/Cygwin、Solaris、FreeBSD/OpenBSD、QNX (Blackberry 10)和 MacOS 上干净地编译。

目前这个工具支持以下协议:星号，AFP，思科 AAA，思科认证，思科使能，CVS，火鸟，FTP，HTTP-FORM-GET，HTTP-FORM-POST，HTTP-GET，HTTP-HEAD，HTTP-POST，HTTP-Proxy，HTTPS-FORM-GET，HTTPS-FORM-POST，HTTPS-GET，HTTPS-HEAD，HTTPS-POST，HTTP-PROXY，ICQ，IMAP，IRC，LDAP，MEMCACHED，MONGODB，MS-SQL，MYSQL，NCP

如果你对当前的开发状态感兴趣，你总是可以在 hydra 的项目页面上找到 hydra 的最新发布/生产版本，网址是:Github:SVN co【https://github.com/vanhauser-thc/thc-hydra】[或 git clone](https://github.com/vanhauser-thc/thc-hydra)[https://github.com/vanhauser-thc/thc-hydra](https://github.com/vanhauser-thc/thc-hydra)使用开发版本风险自担。它包含新的特性和新的错误。事情可能不会成功！

**又念——[Brutemap:找个人算账](https://kalilinuxtutorials.com/brutemap/)**

**如何编译**

要配置、编译和安装 hydra，只需键入:

**。/configure
make
make install**

如果您想要 ssh 模块，您必须设置 libssh(不是 libssh2！)在您的系统上，从[http://www.libssh.org](http://www.libssh.org/)获取它，对于 ssh v1 支持，您还需要在 cmake 命令行中添加“-DWITH_SSH1=On”选项。

**重要提示:**如果您在 MacOS 上编译，那么您必须这样做——不要通过 brew 安装 libssh！

如果您使用 Ubuntu/Debian，这将安装一些可选模块所需的补充库(注意，有些可能在您的发行版中不可用):

**apt-get install libssl-dev libssh-dev libid n11-dev libpcre 3-dev \
libgtk 2.0-dev libmysql client-dev libpq-dev libsvn-dev \
firebird-dev libmemcached-dev**

这将启用除 Oracle、SAP R/3、NCP 和 apple 归档协议之外的所有可选模块和功能，您需要从供应商的网站下载并安装这些模块和功能。

对于所有其他基于 Linux 和 BSD 的系统，使用系统软件安装程序，并查找类似上面命令中的同名库。在所有其他情况下，您必须下载所有源代码库并手动编译它们。

**支持的平台**

*   所有 UNIX 平台(Linux，*BSD，Solaris 等。)
*   MacOS(基本上是 BSD 的克隆)
*   带有 Cygwin 的 windows(IP v4 和 IPv6)
*   基于 Linux、MacOS 或 QNX 的移动系统(例如 Android、iPhone、Blackberry 10、Zaurus、iPaq)

**如何使用**

如果你只是输入`**hydra**`，你会看到可用的重要选项的简短摘要。键入`**./hydra -h**`查看所有可用的命令行选项。

请注意，不包括登录/密码文件。自己生成它们。但是存在默认密码列表，请使用“dpl4hydra.sh”生成一个列表。

对于 Linux 用户，可以使用 GTK 图形用户界面，试试`**./xhydra**`

对于命令行的用法，语法如下:对于攻击一个目标或一个网络，你可以使用新的"://"样式:hydra[一些命令行选项]协议://TARGET:PORT/MODULE-OPTIONS 旧的模式也可以用于这些，另外如果你想从一个文本文件指定你的目标，你*必须*使用这个:

**hydra【一些命令行选项】[-s PORT]目标协议【模块-选项】**

通过命令行选项，您可以指定尝试哪些登录，哪些密码，是否应该使用 SSL，使用多少并行任务进行攻击，等等。

协议是您要用于攻击的协议，例如 ftp、smtp、http-get 或许多其他可用的协议。目标是您要攻击的目标模块-选项是可选值，每个协议模块都有特定的选项

**首先—**选择你的目标你有三个选项来指定你要攻击的目标:

1.  命令行上的单个目标:只需输入 IP 或 DNS 地址
2.  命令行上的网络范围:CIDR 规范，如“192.168.0.0/24”
3.  文本文件中的主机列表:每个条目一行(见下文)

**其次—**选择您的协议尽量避免 telnet，因为检测正确或错误的登录尝试是不可靠的。使用端口扫描器查看目标上启用了哪些协议。

**第三-**检查模块是否有可选参数 hydra -U 协议，例如 hydra -U smtp

**第四-**目的港这是可选的！如果没有提供端口，则使用协议的默认公共端口。如果指定使用 SSL("-S "选项)，则默认情况下使用 SSL 公共端口。

如果使用“://”符号，如果要提供 IPv6 地址或 CIDR(“192 . 168 . 0 . 0/24”)符号来攻击，就必须使用“" " "]”括号:hydra[一些命令行选项]FTP://[192 . 168 . 0 . 0/24]/hydra[一些命令行选项] -6 smtps://[2001:db8::1]/NTLM

请注意，hydra 所做的一切都是 IPv4 而已！如果要攻击 IPv6 地址，必须添加“-6”命令行选项。所有的攻击都只针对 IPv6！

如果要通过文本文件提供目标，可以不使用://符号，而是使用旧的样式，只提供协议(和模块选项):hydra[一些命令行选项] -M targets.txt ftp 您还可以通过在文件中的目标条目后添加“:”来提供每个目标条目的端口，例如:

**foo.bar.com
target.com:21
unusual.port.com:2121
default.used.here.com
127 . 0 . 0 . 1** 

注意，如果您想要附加 IPv6 目标，您必须提供-6 选项，并且*必须*将 IPv6 地址放在文件(！idspnonenote)的括号中。)像这样:

**foo.bar.com
target.com:21
【fe80::1% eth 0】
【2001::1】
【2001::2】:8080
【2a 01:24a:133:0:00:123:ff:1a】**

**登录和密码**

对于如何使用登录名和密码进行攻击，您有许多选择，其中-l 表示登录名，而-p 表示密码，您告诉 hydra 这是唯一可以尝试的登录名和/或密码。使用-L 表示登录名，使用-P 表示密码，您可以提供包含条目的文本文件。例如:

**hydra-L admin-P password FTP://localhost/
hydra-L default _ logins . txt-P test FTP://localhost/
hydra-L admin-P common _ passwords . txt FTP://localhost/
hydra-L logins . txt-P passwords . txt FTP://localhost/**

此外，您可以通过“-e”选项尝试基于登录的密码。“-e”选项有三个参数:

**s–尝试以密码
登录 n–尝试空密码
r–反向登录并尝试以密码**登录

如果你想，例如，尝试“尝试登录为密码”和“空密码”，你指定“-e sn”在命令行上。

但是，除了-p/-P 之外，还有两种尝试密码的模式:您可以使用文本文件，其中登录名和密码由冒号分隔，例如:

**admin:password
test:test
foo:bar**

这是一个常见的默认帐户样式列表，也是由 hydra 提供的 dpl4hydra.sh 默认帐户文件生成器生成的。您可以将这样的文本文件与-C 选项一起使用-请注意，在此模式下，您不能使用-l/-L/-p/-P 选项(-e nsr)。示例:

**hydra-C default _ accounts . txt FTP://localhost/**

最后，还有一个带有-x 选项的 bruteforce 模式(不能与-p/-P/-C 一起使用):

**-x 最小长度:最大长度:字符集**

字符集的定义是 A 代表小写字母，A 代表大写字母，1 代表数字，对于你提供的任何东西，它都是它们的真实表示。示例:

**-x 1:3:a 生成长度为 1 到 3 的全部小写字母的密码
-x 2:5:/生成长度为 2 到 5 的仅包含斜线的密码
-x 5:8:A1 生成长度为 5 到 8 的全部大写字母和数字的密码**

示例:

**九头蛇-l FTP-x3:3:FTP://localhost/**

通过第三个命令行参数(目标服务可选)或-m 命令行选项，可以将一个选项传递给模块。许多模块使用这个，少数需要它！

要查看模块的特殊选项，请键入:

九头蛇-U

例如

。/hydra -U http-post-form

特殊选项可以通过-m 参数传递，作为第三个命令行选项或以 service://target/option 格式传递。

示例(它们都是平等的):

**。/hydra -l 测试-p 测试-m 平原 127.0.0.1 imap
。/hydra-l test-p test 127 . 0 . 0 . 1 IMAP 平原
。/hydra-l test-p test IMAP://127 . 0 . 0 . 1/PLAIN**

**恢复中止/崩溃的会话**

当 hydra 使用 Control-C 中止、终止或崩溃时，它会留下一个“hydra.restore”文件，该文件包含恢复会话所需的所有信息。

该会话文件每 5 分钟写入一次。注意:不能将 hydra.restore 文件复制到不同的平台(例如从小端到大端，或者从 Solaris 到 AIX)

**如何扫描/破解代理**

环境变量 HYDRA_PROXY_HTTP 定义了 web 代理(这只适用于 HTTP 服务！).以下语法有效:

**HYDRA _ PROXY _ HTTP = " HTTP://123 . 45 . 67 . 89:8080/"
HYDRA_PROXY_HTTP="http://login:password@123.45.67.89:8080/"
HYDRA _ PROXY _ HTTP = " PROXY list . txt "**

最后一个示例是一个包含多达 64 个代理的文本文件(格式定义与其他示例相同)。

对于所有其他服务，使用 HYDRA_PROXY 变量进行扫描/破解。它使用相同的语法。例如:

**HYDRA _ PROXY = connect | socks 4 | socks 5]://[log in:password @]PROXY _ addr:PROXY _ port**

例如:

**HYDRA _ PROXY = connect://PROXY . anonymizer . com:8000
HYDRA _ PROXY = socks 4://auth:pw @ 127 . 0 . 0 . 1:1080
HYDRA _ PROXY = socksproxylist . txt**

**附加提示**

*   按可能性对密码文件进行排序，并使用-u 选项更快地找到密码！
*   uniq 你的字典文件！这可以节省你很多时间🙂cat word . txt | sort | uniq > dictionary . txt
*   如果您知道目标正在使用密码策略(只允许用户选择最小长度为 6 的密码，至少包含一个字母和一个数字，等等。使用 hydra 软件包附带的 pw-inspector 工具来减少密码列表:cat dictionary . txt | pw-inspector-m 6-c 2-n > passlist . txt

**结果输出**

结果和其他信息一起输出到 stdio。通过-o 命令行选项，还可以将结果写入文件。使用-b，可以指定输出的格式。目前，支持这些功能:

*   `text`–纯文本格式
*   `jsonv1`–使用模式 1.x 版本的 JSON 数据(定义如下)。
*   `json`–JSON 数据使用最新版本的模式，目前只有版本 1。

如果使用 JSON 输出，如果在引导 Hydra 时出现严重错误，结果文件可能不是有效的 JSON。

**JSON 模式**

下面是 JSON 输出的一个例子。一些字段的注释:

*   `**errormessages**`**–一个零个或多个字符串的数组，通常在 Hydra 运行结束时打印到 stderr。文本是非常自由的形式。**
*   **`**success**`**–显示 Hydra 是否正确无误地运行(如果检测到密码，则显示**而非**)。该参数是 JSON 值`**true**` 或`**false**` 取决于完成情况。****
*   ****`**quantityfound**`**–发现了多少个用户名+密码组合。******
*   ******`**jsonoutputversion**`**–版本模式，1.00，1.01，1.11，2.00，2.03 等。Hydra 将使版本的第二个元组总是两位数，以使下游处理器更容易处理(相对于 1.1 和 1.10)。次要级别的版本是附加的，因此 1.02 将比 1.00 包含更多的字段，并且是向后兼容的。2.x 版本会破坏 1.x 版本的输出。********

 ******1.00 版示例:

**{
" ERROR messages ":[
"[ERROR]某个东西的错误消息"、
"[ERROR]另一个消息"、
"这些都是很自由的形式"
、
" generator ":{
" build ":" 2019-03-01 14:44:22 "、
" command line ":" Hydra-b JSON v1-o results . JSON……"、
" jsonoutversion ":"
{
"host": "127.0.0.1 "，
"login": "joe@example.com "，
"password": "joe "，
"port": 9999，
" service ":" http-post-form "
}
，
"success": false
}**

**bug&特性**

九头蛇:如果你发现了错误或者你写了一个新的模块，给我或者大卫发邮件。[vh@thc.org](mailto:vh@thc.org)(并将“反垃圾邮件”放在主题行中)

你应该用 PGP 加密发给[vh@thc.org](mailto:vh@thc.org)的电子邮件:

———begin PGP public key block—(VH @ thc . org)版本:GnuPG v 3 . 3 . 3(VH @ thc . org)
T2]mqinfip+7 qbeacjctjohujbqxqqqq7melladvxrteqh8 kqhpor 018 xkel 09 ptkibwfbku 48 XLR 3 et V5 fc1 yet 8 gdowl 5 o 0 qtk1 aflybkflvnjdrs+y2 bpjit

[**Download**](https://github.com/vanhauser-thc/thc-hydra)******