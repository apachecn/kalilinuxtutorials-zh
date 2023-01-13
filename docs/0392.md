# Bincat:集成了 IDA 的二进制代码静态分析器

> 原文：<https://kalilinuxtutorials.com/bincat-binary-code-static-analyser/>

**BinCAT** 是一个*静态*二进制代码分析工具包，旨在帮助逆向工程师，直接从 IDA 或使用 Python 进行自动化。

它的特点是:

*   价值分析(寄存器和存储器)
*   污点分析
*   类型重建和传播
*   向前和向后分析
*   免后使用和双免检测

**也读:**[lol bas——靠土地为生的二进制和脚本](https://kalilinuxtutorials.com/lolbas/)

**快速常见问题解答**

**支持的主机平台:**

*   IDA 插件:all，版本 **7.0 或更高版本** (BinCAT 使用 PyQt，而不是 PySide)
*   分析器(本地或远程):Linux、Windows、macOS(可能)

**支持分析的 CPU(目前):**

*   x86-32
*   x86-64
*   ARMv7
*   ARMv8
*   （IBM 和 Apple 公司联合生产的）个人台式机…

**安装**

**仅支持 IDA v7 或更高版本**

v6.9 可能行得通，但我们不会支持。

**【二进制分发安装(推荐)】**

[二进制发行版](https://github.com/airbus-seclab/bincat/releases)包含了所有需要的东西:

*   分析仪
*   IDA 插件

安装步骤:

*   提取 BinCAT 的[二进制发行版](https://github.com/airbus-seclab/bincat/releases)(不是 git repo)
*   在 IDA 中，点击“文件->脚本文件…”菜单(或键入 ALT-F7)
*   选择`install_plugin.py`
*   BinCAT 现在安装在您的 IDA 用户目录中
*   重启 IDA

**手动安装**

**分析**

分析器可以在本地使用，也可以通过 Web 服务使用。

**在 Linux 上:**

*   使用 Docker: [Docker 安装说明](https://github.com/airbus-seclab/bincat/blob/master/doc/install_docker.md)
*   手动:[建造和安装说明](https://github.com/airbus-seclab/bincat/blob/master/doc/install_manual.md)

**在 Windows 上:**

*   [构建指令](https://github.com/airbus-seclab/bincat/blob/master/doc/windows_build.md)

**IDA 插件**

*   [Windows 手动安装](https://github.com/airbus-seclab/bincat/blob/master/doc/plugin_manual_win.md)。
*   [Linux 手动安装](https://github.com/airbus-seclab/bincat/blob/master/doc/install_plugin.md)

安装 pip 后，BinCAT 应与 IDA 合作开发葡萄酒:

*   下载[https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)(验证不错😉
*   `~/.wine/drive_c/Python27/python.exe get-pip.py`

**使用 BinCAT**

**快速启动**

*   通过使用`Ctrl-Shift-B`快捷方式或使用`Edit -> Plugins -> BinCAT`菜单加载插件
*   转到您想要开始分析的指令
*   选择`BinCAT Configuration`窗格，点击`<-- Current`定义起始地址
*   开始分析

**配置**

可以通过`Edit/BinCAT/Options`菜单配置全局选项。

默认配置和选项存储在`$IDAUSR/idabincat/conf`中。

**选项**

*   “使用远程 bincat”:如果您在 docker 容器中运行 Docker，请选择此项
*   “远程 URL”:[http://localhost:5000](http://localhost:5000/)(或远程 BinCAT 服务器的 URL)
*   “自动启动”:IDA 启动时自动加载 BinCAT
*   “保存到 IDB”:`save to idb`复选框的默认状态

[**Download**](https://github.com/airbus-seclab/bincat)