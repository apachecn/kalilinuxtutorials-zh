# UAC:类 Unix 工件收集器

> 原文：<https://kalilinuxtutorials.com/uac/>

[![UAC : Unix-like Artifacts Collector](img/65bfea874439323e21ed47ec78c068d2.png "UAC : Unix-like Artifacts Collector")](https://1.bp.blogspot.com/-ZVth4mHg_t0/YHSfyW9emuI/AAAAAAAAItA/QXZQhtkM1HcD7mgByEpb9bzeSqxtPZOOwCLcBGAsYHQ/s728/UAC%25281%2529.png)

**UAC** 是一个用于事件响应的实时响应收集工具，它利用内置工具来自动收集类似 Unix 的系统工件。它尊重在执行过程中变化的易失性和工件的顺序。它旨在促进和加快数据收集，并在事件响应期间减少对远程支持的依赖。

UAC 也可以运行安装的法医图像。请查看`conf/uac.conf`文件了解更多详情。

您可以在工件收集期间使用您自己的经过验证的工具。它们将被用来代替目标系统提供的内置函数。更多信息请参考`bin/README.txt`。

**支持的系统**

*   [计]高级交互执行程序（Advanced Interactive Executive）
*   加州大学伯克利分校软件(Berkeley Software Distribution)
*   Linux 操作系统
*   马科斯
*   Solaris

**收藏家**

*   **进程(-p)**

收集信息，计算 MD5 散列，并从运行的进程中提取字符串。

*   **网络(-n)**

收集带有相关进程信息的活动网络连接。

*   **用户(-u)**

收集用户帐户信息、登录相关文件和活动。将被收集的文件和目录的列表可以在`conf/user_files.conf`文件中找到。

*   **系统(-y)**

收集系统信息、系统配置文件和内核相关的详细信息。将被收集的文件和目录的列表可以在`conf/system_files.conf`文件中找到。

*   **硬件(-w)**

收集低级硬件信息。

*   **软件(-s)**

收集关于已安装的软件包和软件的信息。

*   **磁盘卷和文件系统(-d)**

收集有关磁盘、卷和文件系统的信息。

*   **Docker 和虚拟机(-k)**

收集 docker 和虚拟机的信息。

*   **正文文件(-b)**

使用`stat`或`stat.pl`工具从文件和目录中提取信息，创建一个[主体文件](https://wiki.sleuthkit.org/index.php?title=Body_file)。在创建文件活动的时间线时，主体文件是一个中间文件。它是一个用竖线(" | ")分隔的文本文件，每个文件占一行。 [Plaso](https://github.com/log2timeline/plaso) 或 [mactime](https://wiki.sleuthkit.org/index.php?title=Mactime) 工具可以用来读取这个文件并对内容进行排序。

*   **对数(-l)**

收集日志文件和目录。将被收集的文件和目录的列表可以在`conf/logs.conf`文件中找到。

*   **可疑文件(-f)**

收集可疑的文件和目录。将被收集的文件和目录的列表可以在`conf/suspicious_files.conf`文件中找到。

**扩展**

*   chkcrookit

运行[工具(如果可用)。请注意，chrootkit 工具不是由 UAC 提供的。您需要在目标系统上获得它，或者下载并编译它，并通过`bin`目录获得它的静态二进制文件。更多信息请参考`bin/README.txt`。](http://www.chkrootkit.org)

*   fls

对所有安装的滑车装置运行侦察工具包 [fls](http://wiki.sleuthkit.org/index.php?title=Fls) 工具(如果可用)。请注意，fls 工具不是由 UAC 提供的。您需要在目标系统上获得它，或者下载并编译它，并通过`bin`目录获得它的静态二进制文件。更多信息请参考`bin/README.txt`。

*   **hash_exec**

收集所有可执行文件的 MD5 哈希。默认情况下，只有小于 3072000 字节(3MB)的文件才会被哈希。更多详情请查看`extensions/hash_exec/hash_exec.conf`文件。警告:此扩展将更改被接触文件的最后访问日期。

**配置文件**

根据当前系统上运行的内核名称，将自动选择以下配置文件之一。不过，您可以使用-P 选项手动选择一个。当 UAC 无法识别当前运行系统的正确配置文件时，或者当您对装载的取证映像运行 UAC 时，这很有用。

*   **aix**

使用这个概要文件来收集 AIX 工件。

*   **bsd**

使用这个概要文件来收集基于 BSD 的系统工件。
*例如 FreeBSD、NetBSD、OpenBSD、NetScaler……*

*   **linux**

使用这个概要文件收集基于 Linux 的系统工件。
*例如 Debian、Red Hat、SuSE、Arch Linux、OpenWRT、QNAP QTS、运行在 Windows 之上的 Linux(WSL)…

*   **苹果电脑**

使用此描述文件来收集 macOS 工件。

*   **索拉里斯**

使用此配置文件收集 Solaris 工件。

**选项**

*   **日期范围(-R)**

日志、可疑文件、用户文件和哈希可执行文件收集期间使用的日期范围。日期范围用于限制使用 find 的-atime、-mtime 或-ctime 参数过滤文件所收集的数据量。默认情况下，UAC 将搜索在给定日期范围内数据上次修改时间(-mtime)或状态上次更改时间(-ctime)的文件。更多详情请参见`conf/uac.conf`。标准格式是 YYYY-MM-DD，表示开始日期，没有结束日期。对于结束日期，请使用 YYYY-MM-DD..YYYY 年月日。

*   **输出文件传输(-T)**

使用 scp 将输出文件传输到远程服务器。必须以`[user@]host:[path]`的形式指定目的地。建议使用 SSH 密钥认证，以便自动进行传输，并避免在传输过程中出现任何密码提示。

*   **调试(-D)**

提高调试水平。

*   详细(-V)

提高详细级别。

*   **以非 root (-U)身份运行**

允许非超级用户运行 UAC。请注意，数据收集将受到限制。

**配置文件**

*   **conf/uac.conf**

主 UAC 配置文件。

*   **conf/logs.conf**

日志(-l)收集器将搜索和收集的目录或文件路径。如果添加了目录路径，将自动收集所有文件和子目录。`find`命令行工具将用于搜索文件和目录，因此添加到该文件的模式需要与`-name`选项兼容。有关说明，请查看`find`手册页。

*   **conf/suspective _ files . conf**

可疑文件(-f)收集器将搜索和收集的目录或文件路径。如果添加了目录路径，将自动收集所有文件和子目录。`find`命令行工具将用于搜索文件和目录，因此添加到该文件的模式需要与`-name`选项兼容。有关说明，请查看`find`手册页。

*   **conf/system_files.conf**

系统文件(-y)收集器将搜索和收集的目录或文件路径。如果添加了目录路径，将自动收集所有文件和子目录。`find`命令行工具将用于搜索文件和目录，因此添加到该文件的模式需要与`-name`选项兼容。有关说明，请查看`find`手册页。

*   **conf/user_files.conf**

用户文件(-u)收集器将搜索和收集的目录或文件路径。如果添加了目录路径，将自动收集所有文件和子目录。`find`命令行工具将用于搜索文件和目录，因此添加到该文件的模式需要与`-name`选项兼容。有关说明，请查看`find`手册页。

*   **conf/exclude.conf**

将从集合中排除的目录或文件路径。如果增加一个目录路径，所有文件和子目录都会自动熟练。`find`命令行工具将用于搜索文件和目录，因此添加到该文件的模式需要与`-path`和`-name`选项兼容。有关说明，请查看`find`手册页。

**用途**

**UAC(类 Unix 工件收集器)
用法:。/uac 收藏者[-e EXTENSION _ LIST] [-P PROFILE][选项][目的地]**

**收藏者:**
-a 启用所有收藏者。
-p 收集信息，计算 MD5 哈希，从运行的进程中提取字符串。
-n 收集带有相关过程信息的活动网络连接。
-u 收集用户账户信息、登录相关文件和活动。
-y 收集系统信息、系统配置文件和内核相关的详细信息。
-w 收集底层硬件信息。
-s 收集已安装软件包和软件的相关信息。
-d 收集有关磁盘、卷和文件系统的信息。
-k 收集 docker 和虚拟机信息。
-b 使用 stat 工具从文件和目录中提取信息，创建一个主体文件。
-l 收集日志文件和目录。
-f 收集可疑文件和目录。

**扩展名:**
-e 扩展名 _ 列表
逗号分隔的扩展名列表。
全部:启用所有扩展。运行 chkrootkit 工具。运行侦察工具包 fls 工具。
hash_exec:哈希可执行文件。

**配置文件:**
-P 配置文件强制 UAC 使用特定的配置文件。
aix:用这个收集 aix 神器。bsd:使用这个来收集基于 BSD 的系统工件。linux:使用这个来收集基于 Linux 的系统工件。
macos:用这个收集 macos 神器。
solaris:用这个收集 solaris 神器。

**选项:**
-R 起始日期 YYYY-MM-DD 或范围 YYYY-MM-DD..YYYY-MM-DD
-T 目的地
使用 scp 将输出文件传输到远程服务器。
必须以[user@]host:[path]
-D 的形式指定目的地，增加调试级别。
-V 增加详细级别。
-U 允许非根用户运行 UAC。请注意，数据收集将受到限制。
-v 打印版本号。
-h 打印此帮助摘要页面。

**目的地:**
指定保存输出的目录。
默认是当前目录。

**输出**

UAC 完成后，所有收集的数据都被压缩，生成的文件存储在目标目录中。压缩文件经过哈希处理(md5 ),值存储在. MD5 文件中。

**例题**

针对当前运行的系统运行所有收集器，并将当前目录用作目标。扩展将不会运行:

**。/uac -a**

针对当前运行的系统运行所有收集器和所有扩展，并使用`/tmp`作为目标目录:

**。/uac -a -e all /tmp**

在当前运行的系统上只运行 hash_exec 和 chkrootkit 扩展，强制`linux`配置文件并使用`/mnt/share`作为目标目录:

**。/uac -e hash_exec，chkrootkit -P linux /mnt/share**

针对当前运行的系统仅运行进程、硬件和日志收集器，强制`solaris`配置文件，使用`/tmp`作为目标目录，并增加详细级别:

**。/uac -p -w -l -P solaris -V /tmp**

[**Download**](https://github.com/tclahr/uac)