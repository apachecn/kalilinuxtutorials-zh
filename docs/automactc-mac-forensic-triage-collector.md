# AutoMacTC:自动化 Mac 取证分类收集器

> 原文：<https://kalilinuxtutorials.com/automactc-mac-forensic-triage-collector/>

[![AutoMacTC : Automated Mac Forensic Triage Collector](img/31785417dbc769e15cda679fdf1da96b.png "AutoMacTC : Automated Mac Forensic Triage Collector")](https://1.bp.blogspot.com/-JbpO2_rW180/XbMuewysOuI/AAAAAAAADHI/TKTLxwI95OEZnnt3ciSgRiu76i1y0EuTACLcBGAsYHQ/s1600/Mac%2B%25281%2529.png)

AutoMacTC 是一个模块化的法医检伤分类收集框架，旨在访问 macOS 上的各种法医工件，解析它们，并以可用于分析的格式呈现它们。

输出可以为 macOS 环境中的事件响应提供有价值的见解。Automactc 可以在活动系统或死磁盘(作为挂载卷)上运行。)

**要求**

*   Python 2.7 (Mac 系统自带 Python 2.7。Python 3 支持将包含在未来的更新中)
*   MacOS 目标系统，用于实时收集(在 macOS 主要版本 10.11 到 10.14 上测试成功)
*   MacOS 分析系统，用于对装载的磁盘映像进行分类

**也可以读作-[r buster:又一个恐怖分子](https://kalilinuxtutorials.com/rbuster-dirbuster/)**

**基本用法**

最简单的方法是，您可以通过下面的调用来运行 automactc。注意:automactc 需要 sudo 特权才能运行，并且应该专门从/usr/bin/python2.7 中调用以确保完整的功能。

**sudo/usr/bin/python 2.7 automatc . py-m all**

这将使用默认设置运行所有模块(-m)，即–默认输入目录将是/，或者当前卷的根目录–默认输出目录将是。/，或运行 auto matc 的工作目录(不是脚本的位置)–输出文件名的默认前缀将是 auto matc-output–默认行为是填充运行时。调试和信息的日志–单个工件输出文件的默认格式是 CSV–默认 CPU 优先级设置为低–完成时的默认行为是将所有输出文件压缩到 tar.gz

为了列出所有可用的模块，只需运行:

**automatc . py-l**

可以分别用-i 和-o 标志指定 inputdir 和 outputdir。

**automatc . py-I/-o/automatc _ output-m all**

可以在每个模块的基础上指定包含或排除的模块。换句话说，您可以包含特定的模块，比如 pslist、bash 和 profiler:

**automatc . py-m PS list bash profiler**

或者，您可以排除特定的模块，运行除指定模块之外的所有模块，如 dirlist 和 autoruns:

**automatc . py-x 目录自动运行**

**输出控制**

对于每个模块，automactc 将生成一个输出文件并用数据填充它。输出文件格式默认为 CSV，但是可以使用-fmt 标志切换到 JSON。目前不可能在每个模块的基础上指定输出格式。

**automatc . py-m all-fmt JSON**

在用数据成功填充输出文件后，该文件将被转入 automactc 完成其第一个模块时生成的. tar 归档文件。完成最后一个模块后，automactc 将 GZIP。tar 存档到. tar.gz。

tar 归档文件的名称遵循以下命名约定:

**前缀，主机名，ip，automatc _ runtime . tar**

第一个字段 prefix 可以在运行时用-p 指定，如果未指定，前缀将设置为 automatc-output。其他字段由运行时收集的数据填充。这在针对单个事件在多个系统上运行 automactc 时非常有用。

**automatc . py-m all-p 老奶奶级**

虽然默认行为是生成一个 tarball，但是使用-nt 标志将会阻止创建 tar 归档文件，并将输出文件保留在输出目录中。

**automatc . py-m all-p granny-Smith-nt**

**当前模块**

–PS list(automatc 运行时的当前进程列表)
–lsof(automatc 运行时打开的当前文件句柄)
–netstat(automatc 运行时的当前网络连接)
–ASL(解析的 Apple 系统日志(。asl)文件)
–autoruns(解析各种持久化位置和 plist)
–bash(解析 bash/。* _ 所有用户的历史文件)
–chrome(解析 chrome 访问历史和下载历史)
–core analytics(解析 Apple diagnostics 产生的程序执行证据)
–dirlist(列出磁盘上的文件和目录)
–firefox(解析 Firefox 访问历史和下载历史)
–install history(解析程序安装历史)
–mru(解析 SFL 和 MRU plist 文件)
–quarantines(解析 QuarantineEventsV2 数据库)
–quick look(解析
–safari(解析 safari 访问历史和下载历史)
–spot light(解析用户 spotlight top 搜索)
–ssh(解析每个用户的 known_hosts 和 authorized_keys 文件)
syslog(解析 system.log 文件)
–system info(基本系统标识，如当前 IP 地址、序列号、主机名)
–Terminal state(解析终端保存的状态文件)
–users(列出系统上现有和已删除的用户)
–utmpx

**高级用法**

默认情况下，automactc 将详细的调试日志记录填充到一个名为`prefix,hostname,ip,runtime.log`的文件中。您可以使用以下命令禁用该日志的生成:

automatc . py-m all-nl

默认情况下，automactc 会将信息和错误日志消息打印到控制台。要在安静模式下运行 automactc 并且不向控制台写入任何消息，请使用-q。INFO 消息包括程序启动消息、每个模块启动一条消息以及完成/清除消息。

**automatc . py-m all-q**

要将调试消息与信息和错误消息一起打印到控制台，请使用-d 标志。

**automatc . py-m all-d**

默认情况下，Automactc 以尽可能低的 CPU 优先级(niceness)运行。使用-r 标志可以禁用 niceness 并以正常优先级运行。

**automatc . py-m all-r**

如果磁盘作为卷安装在分析系统上，Automactc 也可以针对失效磁盘运行。装载后，使用适当的 inputdir(指向卷装载点)和-f 运行 automactc，打开取证模式。

注意:对于一个活动系统，如果您希望在挂载的外围设备上收集目录列表，您可以使用-f 和-i /，否则目录列表将不会递归到挂载的/卷中。

**automatc . py-I/Volumes/mounted _ IMAGE/-o/path/to/output-f-m all**

**目录论**

**目录包含/排除**

使用-K 标志可以将目录列表递归限制到特定的目录。默认情况下，dirlist 将尝试从 inputdir 卷的根目录递归，除非用此标志另行指定。可以在空格分隔的列表中指定多个目录。

**automatc . py-m dirlist-K/Users//Applications//tmp**

还可以用-E 标志从目录列表递归中排除特定的目录。

**automatc . py-m dirlist-E/path/to/known dev directory**

默认情况下，以下目录和文件被排除在活动系统之外:

/.fseventsd(减少输出冗长度)
/。DocumentRevisions-V100(减少输出冗长)
/。Spotlight-V100(减少输出冗长)
/Users/*/Pictures(避免权限错误)
/Users/*/Library/Application Support/address book(避免权限错误)
/Users/*/Calendar(避免权限错误)
/Users/*/Library/Preferences/com . apple . address book . plist(避免权限错误)

默认情况下，对装载的映像运行取证模式时，会排除以下目录:

/.fseventsd(减少输出冗长度)
/。DocumentRevisions-V100(减少输出冗长)
/。Spotlight-V100(减少输出冗长)

要排除的任何其他目录都将附加到该默认列表中，除非您首先提供了-E no-defaults 参数，在这种情况下，只有您指定的目录会被排除。

automatc . py-m dirlist-E no-defaults/path/to/known 目录

**哈希**

下面的散列参数可用于目录列表和自动运行模块。

默认情况下，目录列表模块将只使用 sha256 算法对文件进行哈希处理。如果您希望同时使用 SHA256 和 MD5 算法，请使用`-H sha256 md5`。如果您希望只使用 md5，请使用-H md5。如果您希望两者都不使用，请使用-H none。注意:如果在启用散列的情况下对死磁盘运行目录列表模块，这通常需要很长时间来运行。

automatc . py-m 目录列表-H sha256 md5

默认情况下，目录列表模块将只散列大小小于 10mb 的文件。要在不同的大小阈值下覆盖此设置和哈希文件，可以使用-S 标志以兆字节为单位更改阈值。注意:增加大小阈值可能会增加运行目录列表模块的时间。例如，要散列最大 15MB 的文件:

automatc . py-m 目录表-S 15

**捆绑包、签名、多线程**

默认情况下，目录列表模块不会递归到包目录中，包括以下内容:

。应用程序“，”。框架“，”。lproj '，'。插件“，”。kext '，'。osax '，'。捆绑包“，”。驱动程序“，”。wdgt '

要覆盖此设置，请使用-R 标志。注意:这将产生更大的输出，并且花费更多的时间。这些包目录将在未来的更新中进行配置。

默认情况下，dirlist 模块将检查所有。app，。kext 还有。发现 osax 文件。要防止 dirlist 模块检查任何代码签名，请使用-NC 标志。此参数可用于目录列表和自动运行模块。

**automatc . py-m 目录-NC**

默认情况下，dirlist 模块是多线程的，以提高处理速度。可以用-NM 标志禁用多线程。

**automatc . py-m 目录-NM**

**帮助菜单**

用法:automatc . py[-m INCLUDE _ MODULES[INCLUDE _ MODULES…]|-x
EXCLUDE _ MODULES[EXCLUDE _ MODULES…]|-l][-H]
[-I input DIR][-o output DIR][-p 前缀][-f][-nt][-nl][-T2][-fmt { CSV，JSON }][-NP][-b][-q |-d]【T3][-K DIR _ INCLUDE _ DIRS[DIR _ INCLUDE _ DIRS…]。
模块过滤器:
-m INCLUDE _ MODULES[INCLUDE _ MODULES…]，–INCLUDE _ MODULES INCLUDE _ MODULES[INCLUDE _ MODULES…]
要使用的模块，使用“all”运行所有模块，仅空格分隔的列表

-x EXCLUDE _ MODULES[EXCLUDE _ MODULES…]，–EXCLUDE _ MODULES EXCLUDE _ MODULES[EXCLUDE _ MODULES…]
假定您要运行除此处指定的
之外的所有模块，仅空格分隔的列表
-l，–list
一般参数:
-h，–help 显示此帮助消息并退出
-i INPUTDIR，–input dir input dir
输入目录(使用 mountdmg.sh 脚本挂载 dmg，
使用-f 分析挂载的 HFS 或 APFS 卷)
-o OUTPUTDIR，–output dir output dir
输出目录
-p 前缀，–PREFIX 前缀
前缀附加到 tarball 和/或输出文件
-f 不会将输出文件
打包到 tarball
-nl，–no _ log file，如果提供了标志，则不会在磁盘上生成日志文件
-fmt {csv，json}，–output _ format { csv，json}
在 CSV 和 json 输出之间切换，默认为 csv
-np，–no _ low _ priority
，如果提供了标志，则不会以最高精度
运行 automactc(最低 CPU 优先级)。 高精度
是默认的
-b，–多重处理
如果提供了标志，将多重处理模块
【警告:实验性！]
控制台日志记录详细程度:
-q，–如果提供了标志则不输出到控制台
-d，–debug 启用控制台调试日志记录
特定模块参数:
-K DIR _ INCLUDE _ DIRS[DIR _ INCLUDE _ DIRS…]，–DIR _ INCLUDE _ DIRS DIR _ INCLUDE _ DIRS[DIR _ INCLUDE _ DIRS…]
目录列表模块的目录包含过滤器，
默认为卷根目录，仅空格分隔列表
-E DIR_EXCLUDE 默认值在自述文件中指定。仅空格
分隔列表。将“no-defaults”作为第一项
以覆盖默认排除，然后提供您的
自己的排除
-H DIR _ HASH _ ALG[DIR _ HASH _ ALG…]，–DIR _ HASH _ ALG DIR _ HASH _ ALG[DIR _ HASH _ ALG…]
sha256 或 md5 或两者或无，至少推荐一个
，默认为 sha 256。也适用于
自动运行模块
-S DIR_HASH_SIZE_LIMIT，–DIR _ HASH _ SIZE _ LIMIT DIR _ HASH _ SIZE _ LIMIT
文件大小过滤器，以
兆字节为单位，默认为 10MB。也适用于自动运行
模块
-R，–dir _ recurse _ bundles
如果提供了标志，将完全递归应用程序包。
这会花费更多的时间和空间
-NC，–dir _ no _ code _ signatures
如果提供了标志，将不检查 app 和 kext 文件的代码签名
。也适用于自动运行
模块
-NM，–dir _ no _ multithreading
如果提供了标志，将不会多线程化目录列表
模块

[**Download**](https://github.com/CrowdStrike/automactc)