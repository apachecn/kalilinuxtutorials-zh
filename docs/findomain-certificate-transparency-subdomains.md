# Find domain–使用证书透明度日志来查找子域的工具

> 原文：<https://kalilinuxtutorials.com/findomain-certificate-transparency-subdomains/>

Finddomain 是一个使用证书透明日志来查找子域的工具。

它是如何工作的？

它的工具不使用子(域)发现的常见方法，该工具使用证书透明日志来查找子域，它的方法使它的工具非常快速和可靠。如果您想了解更多关于证书透明度日志的信息，请阅读此

**也可阅读-[如何用自动化转录软件](https://kalilinuxtutorials.com/how-to-save-time-with-automated-transcription-software/)节省时间**

**安装**

如果您想安装它，您可以手动编译源代码或使用预编译的二进制文件。

手动:你需要先在你的电脑上安装 Rust。

**$ git 克隆 https://github.com/Edu4rdSHL/findomain.git
$ CD find domain
$ cargo build–release
$ sudo CP target/release/find domain/usr/bin/
$ find domain**

**使用二进制:**

**$ git 克隆 https://github.com/Edu4rdSHL/findomain.git
$ sudo CP find domain/bin/find domain/usr/bin
$ find domain**

如果您使用的是 BlackArch Linux 发行版，您只需使用:

**$ sudo pacman-S find domain**

**用途**

您可以以两种方式使用该工具，仅发现域名或发现域+IP 地址。

**用法**:
find domain【标志】【选项】

**标志** :
-h，–help 打印帮助信息
-i，–get-ip 返回解析后带有 IP 地址的子域列表。
-V，–version 打印版本信息
**选项** :
-f，–file 设置要使用的输入文件。
-t，–目标目标主机

**演示**

![](img/62fa91af19174e753a6686e999c0a32f.png)

[Click Here For Video](http:// https://asciinema.org/a/k5KdfXZ62db9xgPF9p619FYGa)

[Download](https://github.com/Edu4rdSHL/findomain)