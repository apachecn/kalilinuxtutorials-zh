# goBox:进入沙箱运行不受信任的代码

> 原文：<https://kalilinuxtutorials.com/gobox/>

[![goBox : GO Sandbox To Run Untrusted Code](img/c863d3c1ee9e2670b5de881cdd550d29.png "goBox : GO Sandbox To Run Untrusted Code")](https://1.bp.blogspot.com/-CZo0jZbCziQ/XqCKs_yJcaI/AAAAAAAAGAo/L5605wLpeZ4Nqs88EsWJlGldhiDHeN3YACLcBGAsYHQ/s1600/Gobox%25282%2529.png)

**goBox** 使用 Ptrace 来挂钩读系统调用，在系统调用执行之前，您可以选择接受或拒绝它们。进入沙箱运行不受信任的代码。

**用途**

的用法。/gobox:

gobox【标志】命令

**标志:**
-h 打印用法。
-n 值
用于自动阻止文件读取的 glob 模式。
-y 值
自动允许文件读取的全局模式。

**亦读-[https://kalilinuxtutorials.com/dnsprobe/](https://kalilinuxtutorials.com/dnsprobe/)**

**用例**

**你想安装什么东西**

**>gobox-n "/etc/password . txt " NPM 安装 sketchy-module**
BLOCKED READ on/etc/password . txt
**>gobox-n "/etc/password . txt " bash<【https://danger.zone/install.sh】**
BLOCKED READ on/etc/password . txt

你对你最喜欢的程序读取什么文件感兴趣。

当然，您可以使用 strace，但是它引用文件描述符，该工具通过打印 fd 的绝对路径使这变得简单得多。

**> gobox ls**
想读/usr/lib/x86 _ 64-Linux-GNU/libselinux . so . 1[y/n]

**注意:**对你所有的敏感数据进行加密绝对是一个更好的主意，只有在不方便或不切实际的时候才使用。

注意:我没有为跨 x 兼容性做任何努力，所以它目前只能在 linux 上工作。我很乐意接受补丁来提高可移植性。

[**Download**](https://github.com/nishitm/goBox)