# Tor-Rootkit:使用 Tor 的 Python 3 独立 Windows 10 / Linux Rootkit

> 原文：<https://kalilinuxtutorials.com/tor-rootkit/>

[![](img/93ea66a0ae21e802e7bdb887b3402c83.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg1qpS510FeY095KImUn-o9fd6VpE2onyq6K2zYCt4w-EHT-nN75Iq2TdFhJ-O9XHo14S1_17KZQ_Hh6ca5uss3bsOqok2Qk4eq1d3sxRJTfqs1zo6DcI3ZZa5OFNciZaMf3iJbF3100m-YilAxNeY_AORESiwPW_w-GXZ7EW79M4evA-z5cWAnwa6K=s728)

**Tor-Rootkit** 是一个 Python 3 独立的 Windows 10 / Linux Rootkit。网络通信通过 tor 网络建立。

**如何使用**

*   克隆存储库并更改目录:

**git 克隆 https://github . com/emcruise/torookit . git
光盘。/tor-rootkit**

构建 docker 容器:

docker build -t 监听器。

运行 docker 容器:

**docker run-v $(pwd)/executables:/executables/-it 监听器**

部署可执行文件:当监听器启动并运行时，它会生成一个“可执行文件”目录，其中包含不同平台的不同有效负载。

**TorRootkit/
│ …
└可执行文件/**

注意:客户端可能需要一些时间来连接，因为 PyInstaller 可执行文件有点慢，并且需要启动 tor。

**特色**

*   适用于 Windows 和 Linux 的独立可执行文件，包括 python 解释器和 tor
*   整个通信工作在 tor 隐藏服务之上，这保证了一定程度的匿名性
*   侦听器可以处理多个客户端
*   侦听器在启动时为不同的平台生成有效负载

**监听器外壳命令**

| 命令 | 说明 |
| --- | --- |
| `help` | 显示帮助菜单 |
| `^C`或`exit` | 退出外壳 |
| `list` | 列出所有连接的客户端及其相应的索引 |
| `select <index>` | 用客户端启动 shell |

**客户端外壳命令**

| 命令 | 说明 |
| --- | --- |
| `help` | 显示帮助菜单 |
| `^C`或`exit` | 退出客户端外壳并返回监听器外壳 |
| `os <command>` | 在客户端外壳中执行命令并返回输出 |
| `background` | 保持与客户端的连接并返回给侦听器 |

[**Download**](https://github.com/emcruise/tor-rootkit)