# RetDec : RetDec 是一个基于 LLVM 的可重定目标的机器代码反编译器

> 原文：<https://kalilinuxtutorials.com/retdec-retargetable-decompiler-llvm/>

[![RetDec : RetDec Is A Retargetable Machine-Code Decompiler Based On LLVM](img/da733ff27b58853c726993b6467d3790.png "RetDec : RetDec Is A Retargetable Machine-Code Decompiler Based On LLVM")](https://1.bp.blogspot.com/-6hnKSDo-dHw/Xe1O2Orf7hI/AAAAAAAAD2A/ITVn9OSDeYEkFO8VDiRiUh9dU0MKGKRkwCLcBGAsYHQ/s1600/OpenSource.png)

RetDec 是一个基于 LLVM 的可重定向机器代码 de 编译器。反编译器不限于任何特定的目标体系结构、操作系统或可执行文件格式:

*   支持的文件格式:ELF、PE、Mach-O、COFF、AR(存档)、Intel HEX 和原始机器代码
*   支持的架构:
    *   32 位:英特尔 x86、ARM、MIPS、PIC32 和 PowerPC
    *   64 位:x86-64、ARM64 (AArch64)

**特性**

*   带有详细信息的可执行文件静态分析。
*   编译器和打包程序检测。
*   加载和指令解码。
*   基于签名的静态链接库代码移除。
*   调试信息的提取和利用(DWARF，PDB)。
*   教学习语的重构。
*   检测和重建 C++类的层次结构(RTTI，vtables)。
*   从 C++二进制文件中分离符号(GCC，MSVC，Borland)。
*   功能、类型和高级结构的重构。
*   集成拆卸器。
*   用两种高级语言输出:C 和一种类似 Python 的语言。
*   生成调用图、控制流图和各种统计数据。

**安装&使用**

目前，我们支持 Windows (7 或更高版本)、Linux、macOS 和(实验性的)FreeBSD。RetDec 的安装版本需要大约 4 GB 的可用磁盘空间。

**窗户**

*   要么下载并解包一个[预建的包](https://github.com/avast/retdec/releases)，要么自己构建并安装反编译程序(流程如下)。
*   安装 [Microsoft Visual C++可再发行版 Visual Studio 2017](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) 。
*   安装以下程序:
    *   [Python](https://www.python.org/) (版本> = 3.4)
    *   [UPX](https://upx.github.io/) (可选:如果你想在预处理阶段使用 UPX 解包器)
    *   [Graphviz](https://graphviz.gitlab.io/_pages/Download/windows/graphviz-2.38.msi) (可选:如果您想要生成调用或控制流图)
*   现在，您已经准备好运行反编译器了。要反编译名为 **`test.exe`的二进制文件，**运行以下命令(确保`**python**`运行 Python 3；或者，您可以尝试使用 **`py -3` ) `python $RETDEC_INSTALL_DIR/bin/retdec-decompiler.py test.exe`** 获取更多信息，使用`--help`运行`**retdec-decompiler.py**`。

**Linux**

*   要么下载并解包一个[预建的包](https://github.com/avast/retdec/releases)，要么自己构建并安装反编译程序(流程如下)。
*   构建完反编译程序后，您需要通过发行版的包管理器安装以下包:
    *   [Python](https://www.python.org/) (版本> = 3.4)
    *   [UPX](https://upx.github.io/) (可选:如果你想在预处理阶段使用 UPX 解包器)
    *   [Graphviz](http://www.graphviz.org/) (可选:如果您想要生成调用或控制流图)
*   现在，您已经准备好运行反编译器了。要反编译名为`**test.exe**`的二进制文件，运行`**$RETDEC_INSTALL_DIR/bin/retdec-decompiler.py test.exe**` 获取更多信息，运行`**retdec-decompiler.py**`和`--help`。

**苹果电脑**

*   要么下载并解包一个[预建的包](https://github.com/avast/retdec/releases)，要么自己构建并安装反编译程序(流程如下)。
*   构建完反编译器后，您需要安装以下软件包:
    *   [Python](https://www.python.org/) (版本> = 3.4)
    *   [UPX](https://upx.github.io/) (可选:如果你想在预处理阶段使用 UPX 解包器)
    *   [Graphviz](http://www.graphviz.org/) (可选:如果您想要生成调用或控制流图)
*   现在，您已经准备好运行反编译器了。要反编译名为`**test.exe**`的二进制文件，运行`**$RETDEC_INSTALL_DIR/bin/retdec-decompiler.py test.exe**` 获取更多信息，运行 **`retdec-decompiler.py`和`--help`** 。

**FreeBSD(实验)**

*   目前 FreeBSD 没有预构建的“端口”包。你将不得不自己构建和安装反编译器。该过程描述如下。
*   在您构建了反编译程序之后，您可能需要安装下面的包并执行下面的命令:`**sudo pkg install python37 sudo ln -s /usr/local/bin/python3.7 /usr/local/bin/python3**`
*   现在，您已经准备好运行反编译器了。要反编译名为`**test.exe**`的二进制文件，运行`**$RETDEC_INSTALL_DIR/bin/retdec-decompiler.py test.exe**` 获取更多信息，运行`retdec-decompiler.py`和 **`--help`。**

**内置 Docker**

Docker 支持由社区维护。如果有些事情对你不起作用，或者如果你有改进的建议，打开一个问题或公关。

**构建映像**

Docker 中的构建不需要在本地安装所需的库。对于尝试 RetDec 而不设置整个构建工具链来说，这是一个很好的选择。

要构建 RetDec Docker 映像，请运行

**坞站构建-t retdec–<坞站配置文件**

这将从该存储库的主分支构建映像。

要使用存储库的本地副本构建映像，请使用开发 Dockerfile， **`Dockerfile.dev` :**

**坞站 build -t retdec:dev。-f dock file . dev**

**运行容器**

如果您的`**uid**`不是 1000，请确保 RetDec 可以访问包含您的输入二进制文件的目录:

**chmod 0777/path/to/local/directory**

现在，您可以在容器中运行反编译器:

**docker run–RM-v/path/to/local/directory:/destination retdec retdec-decompiler . py/destination/binary**

注意:不要修改`**/destination**`部分。你只需要换`**/path/to/local/directory**`。输出文件将被生成到`**/path/to/local/directory**`。

**自动化团队城市建设**

我们的 TeamCity 服务器从`**master**`分支的最新提交中不断生成最新的 RetDec 包。这些主要供 RetDec 开发人员、贡献者和其他产品试验人员使用(例如，测试正式版本中出现的问题是否仍然存在于当前的`**master**`)。

您可以随意使用它们，但是请记住，不能保证它们能在您的系统上工作(尤其是 Linux 版本)，并且有可能会出现退化。要获得稳定的 RetDec 版本，要么下载最新的官方预建包，要么构建最新的 RetDec 版本标签。

*   [Windows Server 2016，版本 10.0](https://retdec-tc.avast.com/repository/download/Retdec_WinBuild/.lastSuccessful/package/retdec-master-windows-64b.zip?guest=1)
*   [Ubuntu 仿生 Linux，版本 18.04](https://retdec-tc.avast.com/repository/download/RetDec_LinuxBuild/.lastSuccessful/package/retdec-master-linux-64b.zip?guest=1)
*   [Mac OS X，版本 10.14.6](https://retdec-tc.avast.com/repository/download/Retdec_MacBuild/.lastSuccessful/package/retdec-master-macos-64b.zip?guest=1)

**储存库概述**

该存储库包含以下库:

*   `**ar-extractor**`–从档案中提取目标文件的库(基于 LLVM)。
*   用于将二进制文件翻译成 LLVM IR 模块的 LLVM 通道库。
*   `**capstone2llvmir**`–LLVM IR 翻译库的二进制指令。
*   `config`–用于表示和管理 RetDec 配置数据库的库。
*   `**cpdetect**`–用于二进制文件中编译器和打包器检测的库。
*   `**crypto**`–加密函数的集合。
*   `**ctypes**`–表示 C 函数数据类型的 C++库。
*   `**debugformat**`–DWARF 和 PDB 调试信息的统一表示库。
*   **`demangler`**–能够处理由 GCC/Clang、Microsoft Visual C++和 Borland C++编译器生成的名称的解混淆库。
*   `**dwarfparser**`–DWARF 调试信息的高级表示库。
*   `**fileformat**`–用于解析和统一表示各种目标文件格式的库。目前支持以下格式:COFF，精灵，英特尔十六进制，马赫-O，体育，原始数据。
*   `**llvm-support**`–LLVM 相关实用功能集。
*   用于单元测试的 LLVM IR 仿真库。
*   `**llvmir2hll**`–用于将 LLVM IR 模块翻译成高级源代码(C，类似 Python 的语言)的库。
*   `**loader**`–用于统一表示加载到内存中的二进制文件的库。支持与 fileformat 相同的格式。
*   `**macho-extractor**`–从 fat Mach-O 二进制文件中提取常规 Mach-O 二进制文件的库(基于 LLVM)。
*   **`patterngen`**–二值模式提取器库。
*   **`pdbparser`**–微软 PDB 文件解析器库。
*   **`stacofin`**–静态代码查找器库。
*   **`unpacker`**–解包函数集合。
*   **`utils`**–通用 C++实用程序库。

该存储库包含以下工具:

*   `**ar-extractortool**`–ar-extractor 库的前端(安装为`**retdec-ar-extractor**`)。
*   `**bin2llvmirtool**`—`**bin2llvmir**`库的前端(安装为`**retdec-bin2llvmir**`)。
*   `**bin2pat**`–从二进制文件生成模式的工具(安装为`**retdec-bin2pat**`)。
*   `**capstone2llvmirtool**`—`**capstone2llvmir**`库的前端(安装为`**retdec-capstone2llvmir**`)。
*   `**configtool**`—`**config**`库的前端(安装为`**retdec-config**`)。
*   `**ctypesparser**`–c++库，用于将 C 函数数据类型从 JSON 文件解析为`ctypes`表示(安装为`**retdec-ctypesparser**`)。
*   `**demangler_grammar_gen**` —为`**demangler**`库生成新语法的工具(安装为`**retdec-demangler-grammar-gen**`)。
*   `**demanglertool**`—`**demangler**`库的前端(安装为`**retdec-demangler**`)。
*   `**fileinfo**`–二进制分析工具。支持与`**fileformat**`相同的格式(安装为`**retdec-fileinfo**`)。
*   `**idr2pat**`–从 IDR 知识库中提取模式的工具(安装为`**retdec-idr2pat**`)。
*   `**llvmir2hlltool**`—`**llvmir2hll**`库的前端(安装为`**retdec-llvmir2hll**`)。
*   `**macho-extractortool**`—`**macho-extractor**`库的前端(安装为`**retdec-macho-extractor**`)。
*   `**pat2yara**`–将图案加工成 YARA 签名的工具(安装为`**retdec-pat2yara**`)。
*   `**stacofintool**`—`**stacofin**`库的前端(安装为`**retdec-stacofin**`)。
*   `**unpackertool**`–基于插件的解包器(安装为`**retdec-unpacker**`)。

该存储库包含以下脚本:

*   `**retdec-decompiler.py**`–主要的反编译脚本将它们绑定在一起。这是用于完全二进制到 C 反编译的工具。
*   `**retdec-decompiler.py**`使用的支持脚本:
    *   `**retdec-color-c.py**`–用 IDA 颜色标签装饰输出 C 源代码–IDA 的语法高亮显示。
    *   `**retdec-config.py**`–反编译程序的配置文件。
    *   `**retdec-archive-decompiler.py**`–反编译给定 AR 档案中的对象。
    *   `**retdec-fileinfo.py**`–一个 Fileinfo 工具包装器。
    *   从给定的库中提取函数签名。
    *   `**retdec-unpacker.py**`–尝试使用任何受支持的解包器来解包给定的可执行文件。
    *   `**retdec-utils.py**`–Python 实用程序的集合。
*   `**retdec-tests-runner.py**`–运行单元测试目录中的所有测试。
*   `type_extractor`–生成类型信息(仅供内部使用)

[**Downloa**d](https://github.com/avast/retdec)