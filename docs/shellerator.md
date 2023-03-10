# Shellerator:用于生成绑定和反向 Shell 的 CLI 工具

> 原文：<https://kalilinuxtutorials.com/shellerator/>

[![Shellerator : CLI Tool For The Generation Of Bind & Reverse Shell](img/ed602b99a748e98a73c5eb2eb0b35e4e.png "Shellerator : CLI Tool For The Generation Of Bind & Reverse Shell")](https://1.bp.blogspot.com/-dxrUGSVOgrQ/XrgX2YZqieI/AAAAAAAAGRA/HAoJmfGMDZsbujnkMoLZzPqubJ6zydzagCLcBGAsYHQ/s1600/CLI.gif)

Shellerator 是一个简单的命令行工具，旨在帮助 pentesters 快速生成多种语言(Bash、Powershell、Java、Python……)的单行反向/绑定 shell。

这个项目的灵感来自于 [Print-My-Shell](https://github.com/sameera-madushan/Print-My-Shell/) 。我只是重写了它，并添加了一些选项和闪光。**反向和绑定外壳的列表还不完善。当我有时间的时候我会在这上面工作。我也很乐意审核拉取请求**。

![Shellerator : CLI Tool For The Generation Of Bind & Reverse Shell](img/ed602b99a748e98a73c5eb2eb0b35e4e.png "Shellerator : CLI Tool For The Generation Of Bind & Reverse Shell")

**安装**

安装非常简单，只需克隆这个 git 并安装需求。

**git 克隆 https://github.com/ShutdownRepo/shellerator
pip 3 安装–用户需求. txt**

**用途**

用法也非常简单。

**用法:**shellerator . py[-h][-b |-r][-t TYPE][-p LPORT][-I LHOST]

**生成绑定/反向 shell**

**可选参数:**
【h】，–help 显示此帮助消息并退出
-l，–list 打印 shellerator 可以生成的所有类型的 shell
-b，–bind-shell 生成一个绑定 shell(你连接到目标)【说明 –Reverse-shell 生成一个反向 shell(目标连接到你)(默认)

**绑定 shell 选项:**
-t TYPE，–TYPE 要生成的 shell 的类型(Bash、Powershell、Java…)
-p LPORT，–Port LPORT 监听器端口

**反向 shell 选项:**
-t TYPE，–TYPE 要生成的 shell 的类型(Bash、Powershell、Java…)
-i LHOST、

**也可阅读-[Authelia:Web 应用的单点登录多因素门户](https://kalilinuxtutorials.com/authelia/)**

不带 CLI 菜单

如果您已经知道想要生成什么类型的 shell，但没有时间在漂亮的 CLI 菜单中选择语言，那么您可以使用适当的`**-t**`(或`**--type**`)选项来设置它。

**python 3 shell erator . py[-r |-b]-t/–type bash-I/–IP 192 . 168 . 56 . 1-p/–port 1337**

![](img/07ca8638921f7440e1c932d070ad8a32.png)

**待办事项列表**

**要添加的东西**

这里有一些我想补充的东西，我会尽快去做的

*   添加 bindshells
*   添加加密的 shells 并与 bind/rev 分开？
*   添加某种选项来帮助用户获得如何改进 shell/tty 的信息(rlwrap，stty，ConPty(参见 PayloadsAllTheThings))

**来源**

贝壳大多来自以下链接

*   [https://github . com/swisskyrepo/payloads all the things/blob/master/Methodology % 20 和% 20 resources/Reverse % 20 shell % 20 cheat sheet . MD](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)
*   [http://pentest monkey . net/cheat-sheet/shell/reverse-shell-cheat-sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
*   [https://www . hacking tutorials . org/networking/hacking-netcat-part-2-bind-reverse-shell/](https://www.hackingtutorials.org/networking/hacking-netcat-part-2-bind-reverse-shells/)
*   [https://ashr . net/bind/and/reverse/shell/cheat sheet/windows/and/Linux . aspx](https://ashr.net/bind/and/reverse/shell/cheatsheet/windows/and/linux.aspx)

[**Download**](https://github.com/ShutdownRepo/shellerator)