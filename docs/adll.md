# aDLL:动态链接库的冒险

> 原文：<https://kalilinuxtutorials.com/adll/>

[![](img/6b2bb7070c92df44b7edfa850742b03a.png)](https://blogger.googleusercontent.com/img/a/AVvXsEju7KxQ-1q2wKkWamM5_xFKIGHkQRsfL5QcKL9n2NuRWCgzdcuVDkgsTU8iAAnWqd-dqkPLPTkfnPxtWC6-Uvn8b-f3Leg_LNMwFDrEmboDa5Qb18pWT97_NNNufCCUZeLZaLFQOmXluEK4CFTrSVRSPBel-aT6sPq6FjScDwHxAyDB4EcUZpkMEyr9=s799)

***aDLL** 是一款专注于自动发现 DLL 劫持漏洞的二进制分析工具。该工具分析加载到内存中的二进制文件的映像，以搜索加载时加载的 dll，并利用 Microsoft Detours 库来拦截对 Load Library/Load LibraryEx 函数的调用，以分析运行时加载的 dll。目的是获得一个 dll 列表，这些 dll 是可执行文件在搜索它们的文件夹中找不到的。*

**入门**

要开始使用 aDLL，可以在 Binaries 文件夹中找到一个编译后的可执行文件。建议使用其架构(32 位或 64 位)与要分析的可执行文件版本相匹配的版本。

为了工具的正确运行，dll“hook 32”、“hook64”、“informer32”和“informer64”必须与可执行文件 aDLL.exe 位于同一目录。

**先决条件**

*aDLL 已经在 Windows 10 系统上开发和测试。* *如果系统比较旧和/或没有安装 Visual Studio，有可能工具会抛出“VCRUNTIME140.dll 未找到”这样的错误。在这种情况下，必须安装 Visual C++可再发行更新。更新可以在这里找到:https://www.microsoft.com/es-ES/download/details.aspx?id=49984。*

**编译**

要修改/重新编译该工具，建议使用 Visual Studio 2015 或更高版本。*Visual Studio 解决方案由三个项目组成:aDLL、Hook e Informer。* _ -aDLL:必须编译成可执行文件。如果出现链接错误，则有必要使用 Visual Studio 链接器作为附加依赖项添加 shlwapi.lib 库。_ _ -Hook:必须编译成与要分析的可执行文件具有相同架构的 DLL。生成的钩子文件必须根据需要重命名为 hook32.dll 或 hook64.dll。如果您希望分析两种体系结构的可执行文件，有必要将两个 DLL 放在与 aDLL.exe 相同的目录中。必须编译为 DLL 并重命名为 informer64.dll 或 informer64.dll。

**用法**

该工具有一个-h 选项，用于在屏幕上打印可用选项的简要描述..

**。\aDLL -h**

*作为一个常见的用法示例，aDLL 应至少接收要分析的可执行文件的路径。*

**。\ aDLL-e " C:\ System32 \ notepad . exe "**

*选项:*

**-h 显示工具的帮助，并简要描述每个选项。
-e 指定 aDLL 要分析的可执行文件的路径。
-t 用可执行路径列表指定文本文件的路径。
-o 指定一个目录的路径，该目录将存储每个扫描的可执行文件的报告。
-m 搜索可执行文件的清单并显示在屏幕上。aDLL 搜索嵌入在二进制文件中的清单，如果它作为外部文件存在，它将找不到清单。
-w 定义搜索运行时加载的 dll 时，可执行进程保持打开的秒数。默认时间为 20 秒。
-如果找到了候选 DLL，aDLL 将通过在搜索顺序中模拟合法 DLL 来自动测试是否执行了恶意 DLL。
-d 与-a 选项一起使用，此选项允许您选择将被用作恶意 DLL 的 DLL 的路径。
-r 可执行文件导入的每个 DLL 可以反过来导入其他 DLL 作为依赖项。将对 aDLL 找到的所有未被重定向(ApiSetSchema 或 WinSxS)且不属于系统已知 DLL 列表的 DLL 进行“n”次递归搜索。**

[**Download**](https://github.com/ideaslocas/aDLL)