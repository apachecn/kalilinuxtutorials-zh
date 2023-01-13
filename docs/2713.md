# OSRipper : AV 规避 OSX 后门和密码框架

> 原文：<https://kalilinuxtutorials.com/osripper/>

[![](img/155d665d47902710b78d3d5b93f95346.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEizROCakYtG-jzaelc9exJbxaaUQXbnaTsBZy78E_zUOFx28XCdCtCZkmdDWxhNNyW-hDPraMWuKPjCBHqm4uaQOAmG8bHckl4MrgNGyWKAe9Wo3FH4G-mlktyLxTx-9SFVjaMRvcyMeRN3-SFNM5Wx78lkfd1StOrs4ulhb9nLk2I-H7SmJDQMTusL/s728/OSRipper%20logo%20(1).png)

OSripper 是一个完全不可检测的后门生成器和密码器，专门研究 OSX M1 恶意软件。它也可以在 windows 上运行，但目前还没有对它的支持，而且它不是 windows 的 FUD(至少现在还不是)，现在我不会关注 windows。

**您也可以在 discord 上 PM 我，寻求支持或请求新功能 SubGlitch1#2983**

## 特性

*   FUD(适用于 macOS)
*   作为官方应用的 Cloacks(微软、ExpressVPN 等)
*   转储；系统信息、浏览器历史、登录、ssh/aws/azure/gcloud 信用、剪贴板内容、本地用户等。(关于塞德里克·欧文斯雨燕的更多信息)
*   加密通信
*   类似 Rootkit 的行为
*   每个后门程序都是独一无二的
*   ngrok 支持

## 描述

请查看 wiki 了解 OSRipper 如何工作的信息(变化非常频繁)

## 入门指南

### 依赖关系

你需要 python。如果你不想下载 python，你可以下载一个编译版本。python 依赖关系在 requirements.txt 文件中指定。

从版本 1.4 开始，您需要在 path 中安装 metasploit，以便它可以处理 meterpreter 侦听器。

## 安装

### Linux

**安装 git python -y
git 克隆 https://github.com/SubGlitch1/OSRipper.git
CD OS ripper
sudo python 3 setup . py**

## Windows 操作系统

**git 克隆 https://github.com/SubGlitch1/OSRipper.git
CD OS ripper
sudo python 3 setup . py**

或者从 https://github.com/SubGlitch1/OSRipper/releases/tag/v0.2.3 下载最新版本

### 执行程序

只有这个

**sudo python3 main.py**

[**Download**](https://github.com/SubGlitch1/OSRipper)