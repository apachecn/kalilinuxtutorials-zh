# SneakyEXE:将“绕过 UAC”功能嵌入到您的自定义有效负载中

> 原文：<https://kalilinuxtutorials.com/sneakyexe-embedding-uac-bypassing/>

[![SneakyEXE : Embedding “UAC-Bypassing” Function Into Your Custom Payload](img/4bb66ab2d5ee4a7c19cd92b551a495c2.png "SneakyEXE : Embedding “UAC-Bypassing” Function Into Your Custom Payload")](https://1.bp.blogspot.com/-M9CTTGP49Ws/XSL51l3yjXI/AAAAAAAABRc/a7scvpaLkhwcbX0ago2nRDCiutQVSZS3QCLcBGAs/s1600/SneakyEXE.png)

SneakyEXE 是一个工具，它可以帮助你将 UAC 旁路功能嵌入到你的自定义 Win32 负载中(特别是 x86_64 架构)

*   在 Windows 7、8、10(64 位)上测试
*   免费和开源，发布全部源代码

**要求**

* * *

|  | Linux 操作系统 | Windows 操作系统 |
| --- | --- | --- |
| 体系结构 | 可选择的 | x86_64 |
| Python 3.x > | 是 | `NO` |
| 组件 | 术语颜色 | `NO` |
| 发行版 | 任何的 | Windows 操作系统 |
| 版本 | 任何的 | Windows 7、8、10 |

**也读作——[Slackor:一个使用 Slackor 作为命令的 Golang 植入&控制服务器](https://kalilinuxtutorials.com/slackor-golang-implant-control-server/)**

**用途**

**【Linux】:**

> 这个工具确实需要一个名为`termcolor`的 python 模块。当你运行这个脚本时，如果你还没有安装它，它会自动安装，但是如果你想让这个工具运行得更快，我建议你在继续之前手动安装

**$ pip3 安装术语颜色#安装术语颜色**

**$ #仅临时使用，安装低于
$ git 克隆 https://github.com/Zenix-Blurryface/SneakyEXE.git
$ CD sneaky exe/Linux $ chmod+x sneaky exe . py
$。/sneakyexe <选项> = <有效负载路径/代码> out= <您要保存>** 的位置】

**【视窗】:**

*   参观[https://github.com/Zenix-Blurryface/SneakyEXE](https://github.com/Zenix-Blurryface/SneakyEXE)
*   下载存储库，“克隆或下载”->“下载 ZIP”
*   将其解压缩到您的可选目录中
*   将目录更改为\SneakyEXE\Win32\
*   执行 sneakyexe.exe(或 sys\sneakyexe.exe 以提高启动速度)
*   (可选:您可以将 sneakyexe.exe 复制到您想要的任何目录，并删除解压缩的目录)

**–注意—**只有拥有管理员权限的用户才能成功执行有效载荷。令牌有限的用户不会成功。

**安装**

**【Linux】:**

git 克隆 https://github . com/zenix-blurryface/sneakyexe . git
$ CD sneakyexe
$ chmod+x install . sh
$ sudo。/install.sh

**【视窗】:**

*   `UNAVAILABLE`
*   (如果很多人要求，很快就会)

**建造**

*   基于 Opensuse Leap 15.0 构建
*   使用`Python 3.6.5`开发
*   使用`gcc (MinGW.org GCC-8.2.0-3) 8.2.0`开发，用于有效载荷编译

###### [有效载荷嵌入]

*   为了从源代码构建电梯，您将需要`gcc gcc 8.2.0` ( `c11`)和一台安装了 Windows 10(7/8) 64 位的 AMD64 机器。

**# Windows 10/7/8 (AMD64)
#打开 cmd.exe/powershell.exe
>>gcc-mwindows-o<输出>。exe /source/main.c**

###### [图形用户界面版本]

*   为了从源代码中构建 GUI 版本，您将需要带有`Pyinstaller`、`Pillow`等模块的`Python 3.5.6`(或更高版本)，以及安装了 Windows 10 (7/8) 64 位的 AMD64 机器。

**#假设我们已经预装了 Python
#打开 cmd.exe/powershell.exe
>>pip 安装 pillow #安装 Pillow
> > pip 安装 pyinstaller #安装 Pyinstaller
> > mkdir 编译#可选目录名
> > cd 编译
>>py installer–windowed–one file–icon = ico . ico/source/Win32/GUI . py
#对于 sysematic 版本(/sys)，remove–one file**

**免责声明**

*   该工具仅用于学术目的或道德案例。如果你参与任何黑帽活动，我不会对你的行为承担任何责任
*   在你的软件中随意使用这个项目，就`don't reclaim the ownership`。

[**Download**](https://github.com/Zenix-Blurryface/SneakyEXE)