# Shepard:正在开发使用 Windows BITS 的持久下载/上传/执行工具

> 原文：<https://kalilinuxtutorials.com/shepard-in-progress-persistent-download-upload-execution-tool-using-windows-bits/>

[![Shepard : In Progress Persistent Download/Upload/Execution Tool Using Windows BITS](img/8aa51830f3ee15e16dcad0d4833596af.png "Shepard : In Progress Persistent Download/Upload/Execution Tool Using Windows BITS")](https://1.bp.blogspot.com/-Mvsp1i55ZD0/YM34kMnYkUI/AAAAAAAAJk0/jzvUT_5lkrE8gIAbeg5j2BPQ8Yq-EIBLQCLcBGAsYHQ/s728/Shepard%25281%2529.png)

Shepard 是一个正在使用 Windows 后台智能传输服务(BITS)的持久性工具。

*   **功能:**文件下载、文件过滤、文件下载+持久执行
*   **用法:**以管理员身份运行 shepard.exe，命令行参数如下
*   **-d remoteLocation，writePath:** 将常规文件下载到您选择的本地路径
*   **-e remoteLocation，localPath:** 从您选择的本地路径上传常规文件(仅发送到 IIS 服务器，这是 BITS 的限制)
*   **-dr remoteLocation，writePath，[optionalFileArgs]:** 将文件下载到您选择的路径，并将尝试保持持久性。下载的文件将尝试使用 optionalFileArgs 运行，BITS 将每 30 秒检查一次，以确保文件仍在受损系统上运行。

不带参数或参数数量不正确地运行这个可执行文件将导致 shepard 干净地退出。

**BINDSHELL**

服务器(受害者)是用 C#写的。它监听端口 6006。

**用法:**不带参数运行 shepardsbind_serv.exe。

客户端(攻击者)是使用 Python 编写的，并带有一个参数:受害者机器的 IP 地址。用法:使用一个参数运行 shepardsbind _ recv . py:

不带参数运行 shepardsbind_recv.py 将返回错误。提示符将类似于:%SBS%。

**结合使用它们**

受害者电脑上唯一可执行的文件是 shepard.exe。将下载的 bindshell 可执行文件托管到一个可公开访问的位置。Shepard 将下载并运行 bindshell 可执行文件，用户现在可以使用 python 接收器了。如果找到并杀死外壳，它将在 30 秒后重新启动。正在进行的最后步骤:找出如何在 shell 可执行文件被删除的情况下重新运行 shepard.exe 来重新下载。很可能会使用服务。

[**Download**](https://github.com/d3adzo/shepard)