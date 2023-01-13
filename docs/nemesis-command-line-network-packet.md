# ne mesis——一个命令行网络数据包制作和注入实用程序

> 原文：<https://kalilinuxtutorials.com/nemesis-command-line-network-packet/>

涅墨西斯项目被设计成一个基于命令行的、可移植的人类 IP 栈，用于类 UNIX 和 Windows 系统。该套件根据协议进行分解，应该允许从简单的 shell 脚本中对注入的数据包进行有用的脚本编写。

## **涅墨西斯特性**

*   ARP/RARP、DNS、以太网、ICMP、IGMP、IP、OSPF、RIP、TCP 和 UDP 协议支持
*   类 UNIX 系统上的第 2 层或第 3 层注入
*   Windows 系统上的第 2 层注入(仅限)
*   来自文件的数据包有效负载
*   文件中的 IP 和 TCP 选项
*   在 OpenBSD、Linux、Solaris、Mac OS X 和 Windows 2000 上测试

每个受支持的协议都使用自己的协议“注入器”,并附有解释其功能的手册页。

有关版本的详细信息，请参考变更日志；有关可用功能的详细描述，请参考每个协议注射器的文档。

**也读作 [UploadScanner : HTTP 文件上传扫描代理](https://kalilinuxtutorials.com/uploadscanner-http-file-upload-scanner/)**

## **安装**

复仇女神是围绕 libnet 建立的。Windows 平台构建也需要 libpcap。涅墨西斯<= 1.4 was built around libnet 1.0 and Nemesis > = 1.5 要求 libnet 1.1，或更高版本。

在 Debian 和 Ubuntu 衍生的 GNU/Linux 系统上:

```
sudo apt install libnet1-dev
```

这将 libnet 头文件和库文件安装在一个标准位置，这个位置`**configure**`脚本可以很容易地找到。如果您的 libnet1 安装在非标准位置，您可以提供如下路径:

```
configure LDFLAGS=-L/path/to/lib CPPFLAGS=-I/path/to/header
```

GNU Configure & Build 系统使用`**/usr/local**`作为默认的安装前缀。通常这就足够了，下面的例子改为安装到`**/usr**`:

```
tar xf nemesis-1.5.tar.xz
cd nemesis-1.5/
./configure --prefix=/usr
make -j5
sudo make install-strip
```

#### **在 Windows 上安装**

nemesis.exe 可以安装在 Windows 系统的任何地方。需要注意的是，LibnetNT.dll 必须存在于与 nemesis.exe 相同的目录中，或者存在于 **`%PATH%`** 变量中列出的任何目录中。在 Windows 2000 上，这将是`**%SystemRoot%\System32**`

## **从 GIT 构建**

如果您想做出贡献，或者只是想尝试最新但尚未发布的特性，那么您需要了解一些关于 GNU Configure & Build 系统的事情:

*   `**configure.ac**`和每个目录的`**Makefile.am**`是关键文件
*   **`configure`**`**Makefile.in**`由`**autogen.sh**`生成，不存储在 GIT 中，而是为释放 tarballs 自动生成
*   `**Makefile**`是由 **`configure`** 脚本生成的

要从 GIT 构建，首先需要克隆存储库并运行 **`autogen.sh`** 脚本。这需要在你的系统上安装`**automake**`和`**autoconf**`。

```
git clone https://github.com/troglobit/inadyn.git
cd inadyn/
./autogen.sh
./configure && make
```

GIT 源代码是一个移动的目标，不推荐用于生产系统，除非您知道自己在做什么！

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/troglobit/nemesis) **鸣谢:马克·格里姆斯、杰夫·内森和约阿希姆·尼尔森**