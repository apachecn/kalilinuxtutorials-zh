# 系统信息:一个免费的，强大的，多用途的工具，帮助您监控系统资源，调试软件和检测恶意软件

> 原文：<https://kalilinuxtutorials.com/system-informer/>

[![](img/c6c05e0ca5c4a63e51028d47f954cdef.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgr-uOWMY4K2NpBwdYAQQgyUQ8Qjg1pdsD6cEmJzn3zF7RhmgfI6C8ludJqH7JzZagjGzojeq6voUxbHcXnubyZdTlWwDZ2LjAIiJCfBwgznV0hyyY5GQL3XK65mlYU_wmOO68ZC3i_Te_evdnI7pMw0mdWibxBikmiPp5_oOZymduv8ZLNV7q4xrfy/s728/system-informer-a-free-powerful-multi-purpose-tool-that-helps-you-monitor-system-resources-debug-software-and-detect-malware-380x250%20(2).png)

**System Informer** ，一款免费、强大、多用途的工具，帮助您监控系统资源、调试软件和检测恶意软件。由 Winsider 研讨会&解决方案公司为您带来。

## 系统需求

Windows 7 或更高版本，32 位或 64 位。

## 特性

*   突出显示系统活动的详细概述。
*   图表和统计数据允许您快速跟踪资源消耗和失控的进程。
*   不能编辑或删除文件？发现哪些进程正在使用该文件。
*   查看哪些程序有活动的网络连接，并在必要时关闭它们。
*   获取磁盘访问的实时信息。
*   查看内核模式、WOW64 和。净支持。
*   超越服务。msc:创建、编辑和控制服务。
*   小巧便携，无需安装。
*   100%自由软件(麻省理工学院)

## 建设项目

需要 Visual Studio (2022 或更高版本)。

执行位于`**build**`目录中的`**build_release.cmd**`来编译项目，或者如果您更喜欢使用 Visual Studio 构建项目，则加载`**SystemInformer.sln**`和`**Plugins.sln**`解决方案。

您可以下载免费的 Visual Studio Community Edition 来构建 System Informer 源代码。

有关更多信息，或者如果您在构建时遇到问题，请参阅构建自述文件。

## 增强功能/缺陷

请使用 GitHub 问题跟踪器来报告问题或建议新功能。

## 设置

如果您从 USB 驱动器运行 System Informer，您可能也想在那里保存 System Informer 的设置。为此，在 SystemInformer.exe 所在的目录下创建一个名为“system informer . exe . settings . XML”的空白文件。您可以使用 Windows 资源管理器来完成此操作:

*   确保在“工具”>“文件夹选项”>“查看”中取消选中“隐藏已知文件类型的扩展名”。
*   右键单击文件夹，然后选择“新建”>“文本文档”。
*   将该文件重命名为 system informer . exe . settings . XML(删除“.”。txt”扩展名)。

[Download](https://github.com/winsiderss/systeminformer)