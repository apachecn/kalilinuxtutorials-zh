# PackageDNA:分析不同编程语言的软件包的工具，这些语言正在或将要被用在它们的代码中

> 原文：<https://kalilinuxtutorials.com/packagedna/>

[![Impost3r : A Linux Password Thief](img/4a687c08e84e01dca72aae6bc105a816.png "Impost3r : A Linux Password Thief")](https://1.bp.blogspot.com/-_O0iQEZGUEo/YSXHS5I4jiI/AAAAAAAAKjg/C4lzwJ-Ch6MksCsFYQ367taiQ0mrQtG4gCLcBGAsYHQ/s728/PackageDNA%2B%25281%2529.png)

**PackageDNA** 让开发人员、研究人员和公司能够分析他们代码中正在使用或将要使用的不同编程语言的软件包，提供信息让他们提前知道这个库是否符合流程。安全开发，如果目前支持，可能的后门(恶意嵌入代码)，域名抢注分析，版本的历史和软件包的报告漏洞(CVE)。

**安装**

使用以下内容克隆此存储库:

**git 克隆 https://github.com/ElevenPaths/packagedna**

**PackageDNA 使用 python-magic** ，它是 libmagic C 库的一个简单包装器，并且还必须安装**:**

 **Debian/Ubuntu
$ sudo apt-get 安装 libmagic1
Windows
你将需要 libmagic 的 dll。@julian-r 已经上传了这个项目的一个版本，其中包括二进制文件
到 PyPI:https://pypi.python.org/pypi/python-magic-bin/0.4.14
过去库的其他来源都是 Windows 的文件。您需要从[binary-zip]\share\misc 中复制文件 magic，并将其位置传递给 Magic(magic_file=…)。
如果你使用的是 64 位版本的 python，你需要 64 位的 libmagic 二进制文件，可以在这里找到:https://github.com/pidydx/libmagicwin64.
更新的版本可以在这里找到:https://github.com/nscaife/file-windows.
OSX
使用自制软件时:brew 安装 libmagic
使用 macports 时:端口安装文件
更多详细信息:https://pypi.org/project/python-magic/

运行安装程序进行安装:

**python 3 setup . py install–用户**

**外部模块**

PackageDNA 使用您应该预先安装的外部模块进行分析:

微软应用部门

**https://github.com/microsoft/ApplicationInspector**

virustotal api

**https://www.virustotal.com/**

图书馆 API

**https://libraries.io/**

机器人足球赛

**https://github.com/rubocop/rubocop**

安装后，您应该在主菜单的选项[7]配置中配置外部模块。

**【1】virus total API Key:你的 API Key
【2】app inspector 绝对路径:/Local/Path/MSAppInpsectorInstallation
【3】libraries . io API Key:你的 API Key
【4】Github Token:你的 Token
【B】Back
【X】Exit**

**注意:**外部模块不是强制性的。PackageDNA 将继续执行，但是我们建议对这些模块进行所有配置，以便该工具执行完整的分析

**运行包 DNA**

在 PackageDNA 目录中:

**。/packagedna.py**

***_****_*_ *| _*\ | |*_ \ |*|**|
|**|*|****_ |***|**_ | |*|*//*/`|/ __)| |/ / / _`/ *| |****| |*| | |(*| | |(*_ | | |(*| | |**/|**//||*|*)|*| _*，*| _*|****/】 /package DNA . py
[*]———————————————*
【！]从菜单中选择:
[*]————————————————————*
【1】分析包(最新版本)
【2】分析包(所有版本)
【3】分析本地包
【4】信息收集
【5】上传文件并分析所有包【T6]输入您的选择:****

[**Download**](https://github.com/Telefonica/packagedna)**