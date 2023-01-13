# Pftriage : Python 工具和库，帮助在恶意软件分类和分析期间分析文件

> 原文：<https://kalilinuxtutorials.com/pftriage-python-malware-analysis/>

Pftriage 是一个在恶意软件分类期间帮助分析文件的工具。它允许分析师快速查看和提取文件的属性，以便在分类过程中提供帮助。

该工具还具有分析功能，可以检测恶意软件使用的常见恶意指标。

**也可以理解为:** [ADAPT:为 WebApps 执行自动化渗透测试的工具](https://kalilinuxtutorials.com/adapt/)

**依赖关系**

*   pefile
*   filemagic

**注意:**在 Mac 上——苹果已经实现了他们自己版本的文件命令。然而，libmagic 可以用自制软件安装

**$ brew 安装 libmagic**

**用途**

用法:pftriage [options]
显示关于要分类的文件的信息。
立场论点:
把文件归档以便分诊。
可选参数:
-h，–help 显示此帮助信息并退出
-i，–imports 显示导入树
-s，–sections 显示节的概述。更多详细信息
通过-v 开关
–移除覆盖移除覆盖数据。
–提取叠加提取叠加数据。
-r，–资源显示资源信息
-R，–rich 显示 Rich 头信息
-D DUMP_OFFSET，–DUMP _ OFFSET
使用传递的偏移量或' ALL '转储数据。目前
仅适用于资源。
-e，–导出显示导出
-a，–分析分析文件。
-v，–详细显示版本。
-V，–版本打印版本并退出。

**章节**

使用-s 或 sections 开关显示部分信息。此外，您可以传递(-v)以获得更详细的部分细节视图。

导出区段传递转储和所需的区段虚拟地址。(例如:–转储 0x00001000)

—-部分概述(使用-v 获取详细的部分信息)—-
名称原始大小原始数据指针虚拟地址虚拟大小熵哈希
。正文 0x 00012200 0x 00000400 0x 00001000 0x 000121d 8 6.71168555177 ff 38 FCE 4 f 48772 f 82 fc 77 B4 ef 223 FD 74
。rdata 0x 00005 a 00 0x 00012600 0x 00014000 0x 0000591 a 4.81719489022 b 0c 15 ee 9 BF 8480 a 07012 cf 277 c 3083
。数据 0x 00001 a00 0x 00018000 0x 0001 a000 0x 0000 ab80 5.28838495072 5d 969 a 878 a 5106 ba 526 aa 29967 ef 877 f
。rsrc 0x 00002200 0x 00019 a00 0x 00025000 0x 00002144 7.91994689603d 361 caffeadb 934 c 9 F6 b 13 b 2474 c 6 f0f
。覆盖 0x 00009 b30 0x 0001 bc00 0x 00000000 0x 0000000 0N/A

**资源**

使用-r 或 resources 显示资源数据。

—-资源概述—
类型:CODATA
名称语言 SubLang 偏移量大小代码页类型
0x 68 LANG _ RUSSIAN 0x 000250 E0 0x 00000 CEE 0x 000004 E4
0x 69 LANG _ RUSSIAN 0x 00025 DD 0 0x 000011 e 6 0x 00004 E4
类型:RT_MANIFEST
名称语言 SubLang 偏移量大小代码页类型
0x 1 LANG _ ENGLISH ENGLISH _ US 0x 0000026 fb8 0x 00018 b

要提取特定的资源，请使用-D 和所需的偏移量。如果要提取所有资源，请传递 ALL is 而不是特定的偏移量。

**进口**

使用-i 或 imports 显示导入数据和模块。被识别为序数的进口将被识别并包括所使用的序数。

[*]加载文件…
—-
导入的模块数量:4 个
KERNEL32.dll
|–GetProcessHeap
|–heap free
|–HeapAlloc
|–SetLastError
|–GetLastError
WS2 _ 32 . dll
|–getaddrinfo
|–freeaddrinfo
|–close socket Ordinal【3】(按序数导入)
|–WSAStartup Ordinal[t

**出口**

使用-e 或-exports 显示导出。

[*]加载文件…
—- Exports —-
总导出数:5
地址序号名
0x 00001151 1 find resources
0x 00001103 2 load bitmap
0x 00001137 3 LoadICON
0x 0000109 4 LoadIMAGE
0x 0000111d 5 LoadSTRINGW

**丰富的标题**

使用-R 或-Rich 标志显示 Rich 标题。

[*]加载文件…
—丰富的头细节—
校验和:0x2b41e6a9
Id 产品计数 Build Id Build
——————
150 aliasobj 900 1 20413
132 utc 1500 _ CPP 36 21022 9.0 2008
149 masm 900 17 21022 9.0 2008
1208

**元数据**

如果命令行上没有传递任何选项，将显示文件和版本元数据。

【*】加载文件…【*】处理文件详情…
———文件摘要—-
通用
文件名 samaple.exe
魔型 PE32 可执行文件(GUI) Intel 80386、 对于 MS Windows
Size 135168
第一字节 4d 5a 90 00 03 00 00 00 00 04 00 00 00 ff ff 00 00
哈希
MD5 8 E8 A8 Fe 8361 c 7238 f 60 D6 bbf DBD 304 a 8
SHA1 557832 EFE 10 daff 3 f 528 a3c 3589 e b5 a6 DFD 12447
sha 256 1188
Image Base 0x400000
编译时间 Thu Jun 23 16:04:21 2016 UTC
校验和 0
文件名 sample.exe
EP 字节 55 8b EC 51 83 65 fc 00 8d 45 fc 56 57 50 E8 64
签名 0x4550
第一个字节 4d 5a 90 00 03 00 00 00 04 00 00 ff ff 00 00 ff 00

**分析**

PFTriage 可以对文件执行简单的分析，以帮助识别恶意特征。

[ *]加载文件… [* ]分析文件…
[*]分析完成…
[！]校验和无效校验和
[！] AntiDebug AntiDebug 函数导入[GetTickCount]
[！] AntiDebug AntiDebug 函数导入[QueryPerformanceCounter]
[！]导入可疑 API 调用[TerminateProcess]
[！] AntiDebug AntiDebug 函数导入[setunhandledexception filter]
[！] AntiDebug AntiDebug 函数导入[IsDebuggerPresent]

[**Download**](https://github.com/idiom/pftriage)