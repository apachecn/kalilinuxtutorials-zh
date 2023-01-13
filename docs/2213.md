# Android qf:(Android Quick Forensics)帮助从 Android 设备中快速收集取证证据，以便识别潜在的危害痕迹

> 原文：<https://kalilinuxtutorials.com/androidqf/>

[![](img/a34084563bd0a8683e2cf50f31edc876.png)](https://blogger.googleusercontent.com/img/a/AVvXsEj4ehrhGisn0JdmNeC9_cF-VHSd7UwKYsSX7MtIKSHxTU39UPjxgI9Vm9UgCIJqfJuqaYAOt4n_k89gywMGeXB-505lCEcrtB2epW1QcIqvpK45VF5oyQ1AetmOoLy9i9HER-Mz0TCRLfxbnhnDP7yF-vQLIjB1HcFbMaaXLHx1PDKDjdy-aDxX5rJg=s694)

**Android qf**(Android Quick Forensics)是一款便携式工具，可以简化从 Android 设备获取相关取证数据。它是 Snoopdroid 的继任者，用 Go 重新编写，并利用了官方的 adb 二进制文件。

androidqf 旨在提供一个简单、可移植的跨平台实用程序，以快速从 Android 设备获取数据。它在功能上与 mvt-android 相似。然而，与 MVT 相反，androidqf 被设计成非技术通用户也能轻松运行。

**建造**

Linux、Windows 和 Mac 的可执行二进制文件应该在最新版本中可用。如果您在运行二进制文件时遇到问题，您可能希望自己构建它。

为了构建 androidqf，你需要安装 Go 1.15+。你还需要安装`**make**`。准备就绪后，您可以克隆存储库，并针对您选择的平台运行以下任何命令:

**制作 linux
制作达尔文
制作 windows**

这些命令将在 *build/* 文件夹中生成二进制文件。

**如何使用**

在启动 androidqf 之前，你需要将目标 Android 设备通过 USB 连接到你的计算机，并且你需要启用 USB 调试。请参考官方文档了解如何做到这一点，但也要注意不同制造商的 Android 手机可能需要不同于默认的导航步骤。

一旦启用了 USB 调试，就可以开始启动 androidqf 了。它将首先尝试通过 USB 桥连接到设备，这将导致 Android 手机提示您手动授权主机密钥。确保对它们进行授权，最好是永久授权，这样提示就不会再出现了。

现在，androidqf 应该在您放置 androidqf 二进制文件的同一路径上执行并创建一个采集文件夹。在执行的某个时候，androidqf 会提示你一些选择:这些提示会暂停采集，直到你提供一个选择，所以要注意。

可以提取以下数据:

1.  所有已安装的软件包和相关分发文件的列表。
2.  (可选)所有已安装的 apk 的副本或仅未标记为系统应用的副本。
3.  `**dumpsys**` shell 命令的输出，提供关于设备的诊断信息。
4.  `**getprop**` shell 命令的输出，提供构建信息和配置参数。
5.  shell 命令的输出，提供了所有正在运行的进程的列表。
6.  (可选)SMS 和 MMS 消息的备份。

**加密&潜在威胁**

在未加密的驱动器上携带 androidqf 采集数据可能会让您自己，甚至是那些您从中获取数据的人，面临巨大的风险。例如，你可能在一个有问题的边境被拦住，你的 androidqf 驱动器可能被没收。原始数据可能不仅暴露了您的旅行目的，还可能包含非常敏感的数据(例如安装的应用程序列表，甚至是 SMS 消息)。

理想情况下，您应该对驱动器进行完全加密，但这并不总是可能的。您也可以考虑将 androidqf 放在一个 VeraCrypt 容器中，并随身携带一份 VeraCrypt 来挂载它。然而，VeraCrypt 容器通常只受密码保护，您可能会被迫提供密码。

或者，androidqf 允许用提供的 age 公钥加密每次采集。优选地，该公钥属于终端用户不拥有或至少不携带私钥的密钥对。这样，最终用户即使在胁迫下也无法解密获取的数据。

如果您将名为`**key.txt**`的文件放在与 androidqf 可执行文件相同的文件夹中，androidqf 将自动尝试压缩和加密每个采集，并删除原始的未加密副本。

一旦您检索到加密的采集文件，您可以像这样解密它:

**$ age–decrypt-I ~/path/to/private key . txt-o . zip . zip . age**

请记住，至少有一部分未加密数据可以通过高级取证技术恢复，这是始终可能的，尽管我们正在努力减少这种情况。

[**Download**](https://github.com/botherder/androidqf)