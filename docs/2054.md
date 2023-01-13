# CSIRT-Collect:收集内存和(分类)磁盘取证的 PowerShell 脚本

> 原文：<https://kalilinuxtutorials.com/csirt-collect/>

[![](img/cffb91c8588e9bde5dd468986ba090d2.png)](https://1.bp.blogspot.com/-liQxT_Vh6_E/YSclQkyhZ5I/AAAAAAAAKko/zB-T2m3rHp4MF5eFDaOhPhSH81BKse6VgCLcBGAsYHQ/s728/Disk%2BForensics.png)

**CSIRT-Collect** 是一个 PowerShell 脚本，用于为事件响应调查收集内存和(分类)磁盘取证。

该脚本利用一个网络共享，它将从该共享访问和复制所需的可执行文件，并随后将获取的证据上传到同一个共享后收集。

对所述目录的权限要求将取决于环境的细微差别以及脚本执行所使用的凭证(交互式与自动化)

在演示代码中，可以看到\Synology\Collections 的网络位置。应该对此进行更改，以反映您环境的具体情况。

收藏文件夹需要包括:

*   子目录 KAPE；从现有安装中复制目录
*   子目录内存；7zip 和 winpmem.exe 的 7za.exe 命令行版本

**CSIRT-Collect**

*   映射到现有网络驱动器–
    *   子目录 1:“内存”——Winpmem 和 7zip 可执行文件
    *   子目录 2:“KAPE”——目录(从本地安装复制)
*   在资产上创建本地目录
*   将内存 exe 文件复制到本地目录
*   用 Winpmem 捕获内存
*   完成后，压缩内存映像
*   根据主机名重命名 zip 文件
*   记录操作系统构建信息(无需确定易失性概况)
*   传输完成后，压缩映像被复制到网络目录并从主机中删除
*   用于 KAPE 输出的资产的新临时目录
*   KAPE！SANS_Triage 集合使用 VHDX 作为输出格式[$hostname.vhdx]运行
*   VHDX 传输到网络
*   完成后删除本地 KAPE 目录
*   将“过程完成”文本文件写入网络，以通知调查人员数据已准备好进行分析。

**CSIRT-Collect_USB**

基本上与 CSIRT-Collect.ps1 功能相同，除了它打算从 USB 设备上运行。内存映像和 KAPE 上的额外压缩操作。vhdx 已被删除。USB 版本的文件夹结构略有变化。在 USB 的根目录上:

*   CSIRT-Collect_USB.ps1
*   标题为“收藏”的文件夹(开始时为空)
*   KAPE 和内存文件夹–同上

执行:-以管理员身份打开 PowerShell 导航到 USB 设备-执行。/CSIRT-Collect_USB.ps1

[**Download**](https://github.com/dwmetz/CSIRT-Collect)