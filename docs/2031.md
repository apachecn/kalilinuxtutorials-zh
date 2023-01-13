# Nimplant:用 Nim 编写的跨平台植入程序

> 原文：<https://kalilinuxtutorials.com/nimplant/>

[![RFCpwn : An Enumeration & Exploitation Toolkit Using RFC Calls To SAP](img/2f3fe2bc0e288f19d24b2e51aea20be2.png "RFCpwn : An Enumeration & Exploitation Toolkit Using RFC Calls To SAP")](https://1.bp.blogspot.com/-DHaQ_HIhpOA/XhTvr7F6l6I/AAAAAAAAETQ/QVqYD0GKm-ESeGoU0Xv1L0cpVGZHI8UzwCLcBGAsYHQ/s1600/Rf-1%25281%2529.png)

Nimplant 是一个用 Nim 编写的跨平台(Linux & Windows)移植，作为一个有趣的项目来了解 Nim，看看它能为 red team 工具开发带来什么。目前，Nimplant 缺乏广泛的规避技术；然而，加班机将变得更加复杂。

**安装**

要安装 Nimplant，您需要在远程计算机上安装 Mythic。你可以在 Mythic 项目页面找到 Mythic 的安装说明。

从神话安装根目录，运行命令:

`**./install_agent_from_github.sh https://github.com/MythicAgents/Nimplant**`

安装完成后，重启 Mythic 来构建一个新的代理。

**高亮显示代理特性**

*   跨平台
*   完全异步
*   可以生成从 C 和 C++源代码编译的代理

**命令手动快速参考**

| 命令 | 句法 | 描述 |
| --- | --- | --- |
| 猫 | `**cat [file]**` | 检索文件的输出。 |
| 激光唱片 | `**cd [dir]**` | 更改工作目录。 |
| 丙酸纤维素 | `**cp [source] [destination]**` | 将文件从源复制到目标。模态弹出菜单。 |
| 卷曲 | `**curl [url] [method] [headers] [body]**` | 执行单个 web 请求。 |
| 下载 | `**download [path]**` | 从目标系统下载文件。 |
| 出口 | `**exit**` | 退出回拨。 |
| getenv | `**getenv**` | 获取所有当前的环境变量。 |
| 工作 | `**jobs**` | 列出所有正在运行的作业。 |
| 杀 | `**kill [pid]**` | 试图终止由`**[pid]**`指定的进程。 |
| 限位开关（Limit Switch） | `**ls [path] [recurse]**` | 用可选参数递归列出`**[path]**`中的文件和文件夹。默认为当前工作目录。 |
| mkdir | `**mkdir [dir]**` | 创建一个目录。 |
| 平均变化 | `**mv [source] [destination]**` | 将文件从源移动到目标。模态弹出菜单。 |
| 著名图象处理软件 | `**ps**` | 列出流程信息。 |
| 显示当前工作目录 | `**pwd**` | 打印工作目录。 |
| 空间 | `**rm [path]**` | 删除由`**[path]**`指定的文件 |
| 壳 | `**shell [command]**` | 运行一个 shell 命令，该命令将转换为一个正在生成的进程，命令行:`**cmd.exe /r[command]**` |
| unsetenv | `**setenv [envname] [value]**` | 根据您的选择设置环境变量。 |
| 睡眠 | `**sleep [seconds]**` | 以秒为单位设置代理的回拨间隔。 |
| unsetenv | `**unsetenv [envname]**` | 取消设置环境变量。 |
| 上传 | `**upload**` | 将文件上传到机器上的远程路径。模态弹出菜单。 |

**支持 C2 简介**

目前，在创建新的 Nimplant 代理时，只有一个 C2 配置文件可供使用:HTTP。

**HTTP 简介**

HTTP 概要文件通过基本的非动态概要文件回调 Mythic 服务器。当选择要在编译时标记到 Nimplant 中的选项时，除了与 GET 请求相关的那些参数之外，所有选项都会被考虑。

[**Download**](https://github.com/MythicAgents/Nimplant)