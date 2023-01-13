# MEC:大规模并行开发

> 原文：<https://kalilinuxtutorials.com/mec-massexploitconsole/>

massExploitConsole 一组黑客工具，带有 CLI 和 UI，用于并发利用。以下是 MEC 的特色:

*   易于使用的 cli 用户界面
*   利用进程级并发执行任何适当的利用
*   一些内置漏洞(自动化)
*   使用 proxychains4 和 ss-proxy 隐藏您的 ip 地址(内置)
*   zoomeye 主机扫描(10 个线程)
*   一个简单的百度爬虫(多线程)
*   censys 主机扫描

**还看:[2018 年最受欢迎的黑客工具](https://kalilinuxtutorials.com/most-popular-hacking-tools-in-2018/)**

### **MEC 入门**

**git 克隆 https://github . com/JM 33-m0/massxpconsole . git&&CD massxpconsole&&。/install.py**

*   当安装 pypi deps 时，可能需要`**apt-get install libncurses5-dev**`(对于基于 Debian 的发行版)
*   现在您应该可以开始了(如果没有，请在此处报告丢失的 deps
*   键入`**proxy**`命令在后台运行预先配置的 [Shadowsocks](https://github.com/shadowsocks/shadowsocks-go) socks5 代理，`**vim ./data/ss.json**`编辑代理配置。并且，`**ss-proxy**`用`**mec.py**`退出

### **要求**

*   GNU/Linux，WSL，MacOS(未测试)，在 [Arch Linux](https://www.archlinux.org) ， [Kali Linux (Rolling，2018)](https://www.kali.org) ，Ubuntu Linux (16.04 LTS)和 Fedora 25 下全面测试(只要你处理了所有 dep，它也可以在其他发行版上工作)
*   Python 3.5 或更高版本(否则可能会出错，[https://github . com/jm33-m0/massExpConsole/issues/7 # issue comment-305962655](https://github.com/jm33-m0/massExpConsole/issues/7#issuecomment-305962655))
*   开发者使用的`**proxychains4**`(在`**$PATH**`中)，需要一个有效的 socks5 代理(你可以在`**mec.py**`中修改它的配置)
*   使用 Java 反序列化漏洞时需要 Java，如果您还没有安装的话，您可能需要安装`**openjdk-8-jre**`。

**注意:**你必须安装所有的 dep 或者工具。

### **用途**

*   只要运行`**mec.py**`，如果它抱怨缺少模块，安装它们
*   如果您想添加自己的漏洞脚本(或二进制文件，无论什么):
    *   `**cd exploits**` **，** `**mkdir <your_exploit_dir>**`
    *   您的漏洞应该以传递给它的最后一个参数为目标，深入研究`**mec.py**`以了解更多信息
    *   `**chmod +x <exploit>**`确保当前用户可以执行
    *   使用`**attack**`命令，然后使用`m`来选择您的自定义漏洞
*   在控制台中键入`help`以查看所有可用的功能
*   `zoomeye`需要有效的用户帐户配置文件`zoomeye.conf`

### **免责声明**

*   请仅在**授权系统**上使用该工具，我不对忽视我的警告的用户造成的任何损害负责。

[**Download**](https://github.com/jm33-m0/mec)