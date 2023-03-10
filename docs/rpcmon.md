# RPCMon:基于 Windows 事件跟踪的 RPC 监视器工具

> 原文：<https://kalilinuxtutorials.com/rpcmon/>

[![](img/64b0d69678b36ffaa42c6b2b15053809.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgFukGwvyjhdK9zQ-VGkAVX4_LZcDgTNtaoBc5VlMGhcxgDzoPvY3Qt1UVulcNwnBR4pZfhpuRm4XAM2fESsK8mG31Zc6uN3ImomBeMzLCKiK9b3T6mgbI_M8A6iEuQpdrRaOmS5r3SjWJRnqt6tTbWyOZizMuRFbWU3sqN2Uq4PsZfMP4hst7vaf5/s728/download%20(5)%20(2).png)

RPCMon 可以帮助研究人员获得进程间 RPC 通信的高级视图。它像 Procmon 一样易于使用，并使用詹姆斯福肖。用于 RPC 的. NET 库。RPCMon 可以向您显示被调用的 RPC 函数、调用它们的进程以及其他相关信息。
RPCMon 使用硬编码的 RPC 字典进行快速 RPC 信息处理，其中包含 RPC 模块的信息。它也有一个选项来建立一个 RPC 数据库，以便在硬编码的 RPC 字典中缺少一些细节的情况下，可以从您的计算机中更新它。

## 用法

双击 EXE 二进制文件，你将得到 GUI 窗口。
RPCMon 需要一个数据库来获得 RPC 函数的细节，没有数据库你将会丢失信息。
要加载数据库，按下`**DB -> Load DB...**`并选择您的数据库。您可以将我们添加到这个项目中的一个 DB:`**/DB/RPC_UUID_Map_Windows10_1909_18363.1977.rpcdb.json**`。

## 特性

*   RPC 函数活动的详细概述。
*   构建一个 RPC 数据库来解析 RPC 模块或使用硬编码的数据库。
*   基于单元格筛选\突出显示行。
*   加粗特定行。

[**Download**](https://github.com/cyberark/RPCMon)