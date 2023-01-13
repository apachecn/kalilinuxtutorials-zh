# dro zer——Android 领先的安全测试框架

> 原文：<https://kalilinuxtutorials.com/drozer-security-testing-framework/>

Drozer(曾经是过去的 Mercury)是 Android 的主要安全测试框架。

它使您能够通过期待应用程序的一部分并与 Dalvik VM、其他应用程序的 IPC 端点和基本操作系统合作，来扫描应用程序和设备中的安全漏洞。

它提供了让你能够利用、分享和理解开放的 Android 滥用的工具。它导致你通过滥用或社会工程向设备发送代理。利用 weasel (MWR 的推进式滥用有效载荷)，它可以通过引入一个完整的操作员，将一个受约束的专家注入一个运行程序，或关联一个转向壳作为远程访问工具(RAT)来扩大可访问的授权。

## **R 对 Drozer**的要求

*   [Python2.7](https://www.python.org/downloads/)

**注意:**在 Windows 上，请确保将 Python 安装的路径和 Python 安装下的脚本文件夹添加到 path 环境变量中。

*   [proto buf](https://pypi.python.org/pypi/protobuf)≥2.6
*   [pyo pensl](https://pypi.python.org/pypi/pyOpenSSL)16.2 以上
*   扭曲≥10.2
*   [Java 开发工具包 1.7](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html)

**注意:**在 Windows 上，请确保将到 javac.exe 的路径添加到 path 环境变量中。

*   [安卓调试桥](https://developer.android.com/studio/releases/platform-tools.html)

**也读作[AutoNSE–Massive NSE AutoSploit 和 AutoScanner](http://kalilinuxtutorials.com/autosploit-and-autoscanner)**

## **命令参考**

| Command | 

### **Describe**

 |
| **运行** | 执行 drozer 模块 |
| **列表** | 显示可以在当前会话中执行的所有 drozer 模块的列表。这将隐藏您没有适当权限运行的模块。 |
| **外壳** | 在代理进程的上下文中，在设备上启动一个交互式 Linux shell。 |
| **cd** | 挂载一个特定的命名空间作为会话的根，以避免重复键入模块的全名。 |
| **清洁** | 删除 drozer 存储在 Android 设备上的临时文件。 |
| **贡献者** | 显示对您系统上使用的 drozer 框架和模块做出贡献的人员列表。 |
| **回声** | 将文本打印到控制台。 |
| **退出** | 终止 drozer 会话。 |
| **帮助** | 显示关于特定命令或模块的帮助。 |
| **装载** | 加载一个包含 drozer 命令的文件，并按顺序执行它们。 |
| **模块** | 从互联网上查找并安装附加的 drozer 模块。 |
| **权限** | 显示授予 drozer 代理的权限列表。 |
| **设置** | 将一个值存储在一个变量中，该变量将作为环境变量传递给它生成的任何 Linux shells。 |
| **未置位** | 删除它传递给它生成的任何 Linux shells 的命名变量。 |

## **安装** 

#### **安装代理**

它可以使用 Android 调试桥(adb)安装。

点击 **[这里](https://github.com/mwrlabs/drozer/releases/download/2.3.4/drozer-agent-2.3.4.apk)** 下载最新的 Drozer 代理。

`$ adb install drozer-agent-2.x.x.apk`

#### **开始会话**

现在，您应该已经在 PC 上安装了控制台，并且代理正在测试设备上运行。现在，您需要将两者联系起来，并准备开始探索。

我们将使用嵌入在 drozer 代理中的服务器来完成这项工作。

如果使用 Android 模拟器，您需要设置一个合适的端口转发，以便您的 PC 可以连接到模拟器内部或设备上的代理打开的 TCP 套接字。默认情况下，它使用端口 31415:

`$ adb forward tcp:31415 tcp:31415`

现在，启动代理，选择“嵌入式服务器”选项并点击“启用”来启动服务器。您应该会看到服务器已经启动的通知。

然后，在您的 PC 上，使用 drozer 控制台进行连接:

#### **在 Linux 上:**

`**$ drozer console connect**`

#### **在 Windows 上:**

**T2`> drozer.bat console connect`**

如果使用真实设备，必须指定设备在网络上的 IP 地址:

#### **在 Linux 上:**

`**$ drozer console connect --server 192.168.0.10**`

#### **在 Windows 上:**

`**> drozer.bat console connect --server 192.168.0.10**`

您应该会看到一个 drozer 命令提示符:

```
selecting f75640f67144d9a3 (unknown sdk 4.1.1)  
dz>
```

提示确认您已连接的设备的 Android ID，以及制造商、型号和 Android 软件版本。

您现在可以开始探索设备了。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/mwrlabs/drozer)