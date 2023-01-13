# Findomain:一个跨平台工具，使用证书透明性日志来查找子域

> 原文：<https://kalilinuxtutorials.com/findomain/>

[![Findomain : A Cross-Platform Tool That Use Certificate Transparency Logs To Find Subdomains](img/dd0ff8eb1a20336698965531b6ecd060.png "Findomain : A Cross-Platform Tool That Use Certificate Transparency Logs To Find Subdomains")](https://1.bp.blogspot.com/-moS8X97lrwI/XSjDU1Z7V1I/AAAAAAAABUY/L5SC03qa0FYRRjqpcspdeUw8at4QJZr7QCLcBGAs/s1600/Findomain%25281%2529.png)

**find domain**是一个跨平台工具，它使用证书透明日志来查找子域。我们目前支持 Linux，Windows 和 MacOS。所有支持的平台都是 64 位。

它是如何工作的？

它的工具不使用子(域)发现的常见方法，该工具使用证书透明日志来查找子域，它的方法使它的工具非常快速和可靠。该工具利用多个公共可用的 API 来执行搜索。

如果你想知道更多关于证书透明度日志的信息，请阅读[https://www.certificate-transparency.org/](https://www.certificate-transparency.org/)

我们目前使用的 API:

*   Certspotter:  [https://api.certspotter.com/](https://api.certspotter.com/)
*   Crt.sh : [https://crt.sh](https://crt.sh/)
*   病毒总量:[https://www.virustotal.com/ui/domains/](https://www.virustotal.com/ui/domains/)
*   https://api.sublist3r.com/
*   脸书:[https://developers . Facebook . com/docs/certificate-transparency](https://developers.facebook.com/docs/certificate-transparency)

如果您知道其他应该添加的内容，请打开一个问题。

**也可阅读-[sneaky exe:将“绕过 UAC”功能嵌入您的自定义有效载荷](https://kalilinuxtutorials.com/sneakyexe-embedding-uac-bypassing/)**

**安装 Linux 使用源代码**

如果您想安装它，您可以手动编译源代码或使用预编译的二进制文件。

**手动:**你需要先在你的电脑上安装 [Rust](https://www.rust-lang.org/) 。

**$ git 克隆 https://github.com/Edu4rdSHL/findomain.git
$ CD find domain
$ cargo build–release
$ sudo CP target/release/find domain/usr/bin/
$ find domain**

**使用编译技巧安装 Linux】**

**$ wget https://github . com/edu 4 rdshl/find domain/releases/latest/download/find domain-Linux
$ chmod+x find domain-Linux
$。/find domain-Linux**

**如果你使用的是 [BlackArch Linux](https://blackarch.org/) 发行版，你只需要使用:**

**$ sudo pacman-S find domain**

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

find domain 0 . 1 . 4
Eduard Tolosa[tolosaeduard@gmail.com](mailto:tolosaeduard@gmail.com)
一种使用证书透明度日志查找子域的工具。

**用法:**
查找域【FLAGS】【OPTIONS】

**FLAGS:**
-a、–all-API 使用所有可用的 API 执行搜索。这需要更多的时间，但是你会得到更多的结果。
-h、–help 打印帮助信息
-i、–get-ip 返回包含 IP 地址的子域列表(如果已解析)。
-V，–版本打印版本信息

**选项:**
-f，–文件设置要使用的输入文件。
-o，–输出将数据以指定的格式写入输出文件。[可能值:txt、csv、json]
-t，–目标主机

**例子**

1.  对子域进行简单搜索，并在屏幕上打印信息:

**寻找域名-example.com**

1.  使用所有 API 对子域进行简单搜索，并在屏幕上打印信息:

**寻找域名-t example.com-a**

1.  搜索子域并将数据导出到 CSV 文件:

**寻找域名-t example.com-o CSV**

1.  使用所有 API 搜索子域，并将数据导出到 CSV 文件:

**寻找域名-t example.com-a-o CSV**

1.  搜索子域并解析子域的 IP 地址(如果可能):

**寻找域-t example.com-I**

1.  使用所有 API 搜索子域，并解析子域的 IP 地址(如果可能):

**寻找域名-t example.com-I-a**

1.  使用所有 API 搜索子域，并解析子域的 IP 地址(如果可能)，将数据导出到 CSV 文件:

**寻找域名-t example.com-I-a-o CSV**

**特色**

*   发现子域没有蛮力，它的工具使用证书透明度日志。
*   根据用户参数发现有或没有 IP 地址的子域。
*   从用户参数(-t)中读取目标。
*   从文件中读取一个目标列表，发现它们有或没有 IP 的子域，如果用户指定，还可以递归地写入每个域的输出文件。
*   将输出写入 TXT 文件。
*   将输出写入 CSV 文件。
*   将输出写入 JSON 文件。
*   跨平台支持:Linux，Windows，MacOS。
*   可选的多 API 支持。

[**Download**](https://github.com/edu4rdshl/findomain)