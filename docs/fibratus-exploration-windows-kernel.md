# Fibratus:探索和跟踪 Windows 内核的工具

> 原文：<https://kalilinuxtutorials.com/fibratus-exploration-windows-kernel/>

**Fibratus** 是一款能够捕获大部分 Windows 内核活动的工具——进程/线程创建和终止、上下文切换、文件系统 I/O、注册表、网络活动、DLL 加载/卸载等等。

内核事件可以很容易地传输到许多输出接收器，如 **AMQP** 消息代理、**弹性搜索**集群或标准输出流。

您可以使用 **filaments** (轻量级 Python 模块)用您自己的工具库来扩展它，从而利用 Python 生态系统的力量。

**也可阅读: [Crashcast-Exploit:批量播放 YouTube 视频的工具，终止应用&重命名 Chromecast 设备](https://kalilinuxtutorials.com/crashcast-exploit/)**

**安装**

[下载最新版本](https://github.com/rabbitstack/fibratus/releases/download/v0.7.2/fibratus-0.7.2.exe) (Windows installer)。变更日志和旧版本可以在[这里](https://github.com/rabbitstack/fibratus/releases)找到。

或者，您可以从 PyPI 获得它。

*   安装依赖项
    *   [下载](https://www.python.org/ftp/python/3.4.0/python-3.4.0.amd64.msi)，安装 Python 3.4。
    *   安装 Visual Studio 2015(您只需要 Visual C 编译器来构建`**kstreamc**`扩展)。确保导出`**VS100COMNTOOLS**`环境变量，使其指向`**%VS140COMNTOOLS%**`。
    *   得到 **Cython** : `**pip install Cython >=0.23.4**` **。**
*   通过 pip 软件包管理器安装 **fibratus** :

**pip 安装光纤**

[**Download**](https://github.com/rabbitstack/fibratus)