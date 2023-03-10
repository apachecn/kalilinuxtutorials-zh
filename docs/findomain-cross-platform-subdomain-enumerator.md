# Findomain:最快的跨平台子域枚举器

> 原文：<https://kalilinuxtutorials.com/findomain-cross-platform-subdomain-enumerator/>

[![Findomain : Fastest & Cross-Platform Subdomain Enumerator](img/198d91387689a329b340f2a54f3a5383.png "Findomain : Fastest & Cross-Platform Subdomain Enumerator")](https://1.bp.blogspot.com/-v9EY7ZfZqPM/XVPCZgONgDI/AAAAAAAAB7g/2CdaSxDutkYoGx6jVV4zWMfDbIzkqNkDACLcBGAs/s1600/findomain%2B%25281%2529.png)

**find domain**是一个最快的跨平台子域枚举器。它的比较给你一个想法，为什么你应该使用 findomain 而不是其他工具。测试使用的域是以下 [BlackArch](https://blackarch.org/) 虚拟机中的【microsoft.com】T2:

**主机:** KVM/QEMU(标准 PC (i440FX + PIIX，1996) pc-i440fx-3.1)
**内核:**5 . 2 . 6-ARCH 1-1-ARCH
**CPU:**Intel(sky lake，IBRS) (4) @ 2.904GHz
**内存:** 139MiB / 3943MiB

用于计算时间的工具是 Linux 中的`time`命令。你可以在 [it link](https://github.com/Edu4rdSHL/findomain/blob/master/comparision_log.md) 中看到测试的所有细节。

| 枚举工具 | 搜索时间 | 找到的子域总数 | CPU 使用率 | RAM 使用 |
| --- | --- | --- | --- | --- |
| find domain | 真正的 0m38.701s | Five thousand six hundred and twenty-two | 极低 | 极低 |
| 资产查找器 | 真正的 6m1.117s | Four thousand six hundred and thirty | 极低 | 极低 |
| Subl1st3r | 真正的 7m14.996s | Nine hundred and ninety-six | 低的 | 低的 |
| 积累* | 真正的 29m20.301s | Three hundred and thirty-two | 非常高 | 非常高 |

*   我迫不及待地想完成大量的测试，看起来它永远不会结束，而且资源的使用率非常高。

**注意:**基准是在 2019 年 10 月 8 日制定的，因为它指出其他工具可以改善事情，你会得到不同的结果。

**又读-[AbsoluteZero:Python APT 后门](https://kalilinuxtutorials.com/absolutezero-python-apt-backdoor/)**

**特色**

*   发现子域没有蛮力，它的工具使用证书透明度日志。
*   根据用户参数发现有或没有 IP 地址的子域。
*   从用户参数(-t)中读取目标。
*   从文件中读取一个目标列表，发现它们有或没有 IP 的子域，如果用户指定，还可以递归地写入每个域的输出文件。
*   将输出写入 TXT 文件。
*   将输出写入 CSV 文件。
*   将输出写入 JSON 文件。
*   跨平台支持:任何平台。
*   可选的多 API 支持。
*   代理支持。

**注意**:代理支持只是代理 API 请求，发现子域 IP 地址的实际实现不支持代理，如果您使用-p 选项，它仍然使用主机网络。

**它是如何工作的？**

It 工具不使用子(域)发现的常见方法，该工具使用证书透明性日志来查找子域，这种方法使 it 工具最快速、最可靠。该工具利用多个公共可用的 API 来执行搜索。如果你想知道更多关于证书透明度日志的信息，请阅读[https://www.certificate-transparency.org/](https://www.certificate-transparency.org/)

我们目前正在使用的 API:

*   Certspotter:  [https://api.certspotter.com/](https://api.certspotter.com/)
*   Crt.sh : [https://crt.sh](https://crt.sh/)
*   病毒总量:[https://www.virustotal.com/ui/domains/](https://www.virustotal.com/ui/domains/)
*   https://api.sublist3r.com/
*   脸书:[https://developers . Facebook . com/docs/certificate-transparency](https://developers.facebook.com/docs/certificate-transparency)

如果您知道其他应该添加的内容，请打开一个问题。

**我们的二进制版本中支持的平台**

我们给出的二进制文件中所有支持的平台都是 64 位的，我们没有计划添加对 32 位二进制版本的支持，如果你想支持 32 位，请遵循[文档](https://github.com/Edu4rdSHL/findomain#build-for-32-bits-or-another-platform)。

*   [Linux](https://github.com/Edu4rdSHL/findomain#installation-in-linux-using-compiled-artifacts)
*   [窗户](https://github.com/Edu4rdSHL/findomain#installation-windows)
*   [苹果电脑](https://github.com/Edu4rdSHL/findomain#installation-macos)
*   [手臂](https://github.com/Edu4rdSHL/findomain#installation-arm)
*   [Aarch64(树莓派)](https://github.com/Edu4rdSHL/findomain#installation-aarch64-raspberry-pi)

**打造 32 位或另一个平台**

如果您想为 32 位系统或另一个平台构建工具，请按照以下步骤操作:

**注意:**你需要先在你的系统中安装 [rust](https://rust-lang.org/) 、 [make](http://www.gnu.org/software/make) 和 [perl](https://www.perl.org/) 。

使用[机箱](https://crates.io/crates/findomain):

*   `**cargo install findomain**`
*   从`**$HOME/.cargo/bin**`开始执行刀具**。参见**[](https://doc.rust-lang.org/cargo/commands/cargo-install.html)****。****

 **使用 Github 源代码:

*   克隆[库](https://github.com/Edu4rdSHL/findomain)或者下载[发布源代码](https://github.com/Edu4rdSHL/findomain/releases)。
*   提取发布源代码(只有下载了压缩文件时才需要)。
*   转到源代码所在的文件夹。
*   执行`**cargo build --release**`
*   现在您的二进制文件在`**target/release/findomain**`中，您可以使用它了。

**Android 安装(term)**

安装 [Termux](https://termux.com/) 包，打开它并按照命令操作:

**$ pkg 安装 rust make perl
$ cargo 安装 find domain
$ CD $ HOME/。货物/箱子
$。/find domain**

**使用源代码在 Linux 上安装**

如果您想安装它，您可以手动编译源代码或使用预编译的二进制文件。

**手动:**你需要先在你的电脑上安装 [Rust](https://www.rust-lang.org/) 。

**$ git 克隆 https://github.com/Edu4rdSHL/findomain.git
$ CD find domain
$ cargo build–release
$ sudo CP target/release/find domain/usr/bin/
$ find domain**

**在 Linux 中安装使用编译好的工件**

**$ wget https://github . com/edu 4 rdshl/find domain/releases/latest/download/find domain-Linux
$ chmod+x find domain-Linux
$。/find domain-Linux**

**如果你使用的是 [BlackArch Linux](https://blackarch.org/) 发行版，你只需要使用:**

**$ sudo pacman-S find domain**

**安装臂**

**$ wget https://github . com/edu 4 rdshl/find omain/releases/latest/download/find omain-arm
$ chmod+x find omain-arm
$。/find domain-arm**

**安装 aarch 64**

**$ wget https://github . com/edu 4 rdshl/find domain/releases/latest/download/find domain-AAR ch 64
$ chmod+x find domain-AAR ch 64
$。/find domain-AAR ch 64**

**安装窗口**

从[https://github . com/edu 4 rdshl/find domain/releases/latest/download/find domain-windows . exe](https://github.com/Edu4rdSHL/findomain/releases/latest/download/findomain-windows.exe)下载二进制文件

打开一个 CMD shell 并转到下载 findomain-windows.exe 的目录。

在 CMD shell 中。

**安装 MacOS**

**$ wget https://github . com/edu 4 rdshl/find domain/releases/latest/download/find domain-OSX
$ chmod+x find domain-OSX . DMS
$。/find domain-OS x . DMS**

**用法**

您可以以两种方式使用该工具，仅发现域名或发现域+IP 地址。

一个使用证书透明日志来查找子域的工具。

**用法:** find domain【标志】【选项】

**标志:** -a，–all-API 使用所有可用的 API 来执行搜索。这需要更多的时间，但是你会得到更多的结果。
-h，–help 打印帮助信息
-i，–get-ip 如果解析则返回带有 IP 地址的子域列表。
-V，–version 打印版本信息

**选项:**
-f，–file 设置要使用的输入文件。
-o，–以指定的格式输出写数据到输出文件。[可能的值:txt，csv，json]
-p，–proxy 使用代理向 API 发出请求。
-t，–目标目标主机

**例题**

*   对子域进行简单搜索，并在屏幕上打印信息:

**寻找域名-example.com**

*   使用所有 API 对子域进行简单搜索，并在屏幕上打印信息:

**寻找域名-t example.com-a**

*   搜索子域并将数据导出到 CSV 文件:

**寻找域名-t example.com-o CSV**

*   使用所有 API 搜索子域，并将数据导出到 CSV 文件:

**寻找域名-t example.com-a-o CSV**

*   搜索子域并解析子域的 IP 地址(如果可能):

**寻找域-t example.com-I**

*   使用所有 API 搜索子域，并解析子域的 IP 地址(如果可能):

**寻找域名-t example.com-I-a**

*   使用所有 API 搜索子域，并解析子域的 IP 地址(如果可能)，将数据导出到 CSV 文件:

**寻找域名-t example.com-I-a-o CSV**

*   使用代理搜索子域( [http://127.0.0.1:8080](http://127.0.0.1:8080/) 在这种情况下，其余的方法继续以相同的方式工作，您只需要在 before 命令中添加-p 标志):

**find domain-t example.com-p http://127 . 0 . 0 . 1:8080**

[**Download**](https://github.com/Edu4rdSHL/findomain)**