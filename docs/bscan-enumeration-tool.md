# Bscan:一个异步目标枚举工具

> 原文：<https://kalilinuxtutorials.com/bscan-enumeration-tool/>

Bscan 是一个命令行实用程序，用于执行主动信息收集和服务枚举。

在其核心，bscan 异步产生众所周知的扫描实用程序的进程，将扫描结果重新调整为突出显示的控制台输出和定义良好的目录结构。

**也可理解为:** [Bincat:集成 IDA 的二进制代码静态分析器](https://kalilinuxtutorials.com/bincat-binary-code-static-analyser/)

**安装**

它被编写为在 [Kali Linux](https://www.kali.org/) 上运行，但是没有什么固有的东西阻止它在任何安装了适当工具的操作系统上运行。有几种不同类型的打包版本和安装它们的方法。

启动和运行的最简单方法是为您的操作系统安装适当的单文件可执行版本的程序(不需要安装 Python):

**在 Linux 上(即 Kali)**
wget-O bscan https://releases.brianwel.ch/bscan/linux
**在 Windows 上**
powershell-c【Net。ServicePointManager]::security protocol =[Net。security protocol type]::TLS 12；wget ' https://releases . Brian wel . ch/bscan/windows '-OutFile ' bscan . exe ' "
**要下载特定版本，请使用以下模式**
wget-O bscan https://releases.brianwel.ch/github/bscan/linux/0.1.4

也可以从 PyPI 下载最新的打包版本(注意这需要现有的 Python 3.6+安装)；

pip 安装 bscan

类似地，您可以从版本控制中获得最先进的版本:

pip 安装 https://github.com/welchbj/bscan/archive/master.tar.gz

基本用法

bscan 具有多种配置选项，可用于根据您的需求调整扫描。这里有一个简单的例子:

$ bscan \
–最大并发 3 \
–模式[Mm]微软\
–状态-间隔 10 \
–详细-状态\
scanme.nmap.org

**这是怎么回事？**

*   **–max-concurrency 3**表示一次运行的并发扫描子进程不超过 3 个
*   **–patterns[Mm]Microsoft**定义一个自定义正则表达式模式，用于在生成的扫描输出中突出显示匹配项
*   **–状态间隔 10** 告诉 bscan 每 10 秒打印一次运行时状态更新
*   **–verbose-status**表示每个状态更新都将打印所有当前运行的扫描子进程的详细信息
*   **scanme.nmap.org**是我们要列举的主机

bscan 还依赖于一些附加的配置文件。默认文件可在 bscan/configuration 目录中找到，用于以下目的:

*   **patterns.txt** 指定当与扫描输出匹配时，在控制台输出中高亮显示的正则表达式模式
*   **required-programs.txt** 指定 bscan 计划使用的已安装程序
*   **port-scans.toml** 定义要在目标上运行的端口发现扫描，以及用于从扫描输出中解析端口号和服务名称的正则表达式
*   **service-scans.toml** 定义基于每个服务在目标上运行的扫描

**详细选项**

以下是运行 bscan-help 时应该看到的内容:

用法:bscan [OPTIONS] targets
异步服务枚举工具
**位置参数:**
目标执行枚举的目标和/或网络
**可选参数:**
-h，–help 显示此帮助消息并退出
–brute-pass-list F 用于暴力强制的密码列表文件名
–brute-user-list F 用于暴力强制的用户列表文件名
–cmd-print-width I 最大整数此目录中缺少的所需配置文件将改为从该程序附带的默认文件中加载
–强制覆盖现有目录
–max-concurrency I 允许并发运行的子进程的最大整数(默认为 20)
–no-program-check disable 检查是否存在所需的系统程序
–no-file-check disable 检查是否存在已配置的单词列表等文件
–no-service-scans 禁止对已发现的服务进行扫描
–output-dir D 写入输出文件的基本目录
–patterns[[…]] 要在输出文本中突出显示的正则表达式模式
–ping-sweep 在运行更密集的扫描之前启用对网络范围内主机的 ping 扫描过滤
–quick-only 是否仅运行快速扫描(不包括对所有端口的全面扫描)
–QS-method S 执行初始 TCP 端口扫描的方法； 必须对应于配置的端口扫描
–状态-间隔 I 打印状态更新之间暂停的整数秒；非正值禁用更新(默认为 30)
–ts-method S 执行全面 TCP 端口扫描的方法；必须对应于已配置的端口扫描
–udp 是否运行 UDP 扫描
–UDP-方法 S 执行 UDP 端口扫描的方法；必须对应于已配置的端口扫描
–verbose-status 是否打印详细的运行时状态更新，基于由`--status-interval`标志
–版本程序版本
–we B- word-list F 用于扫描的单词列表指定的频率

[**Download**](https://github.com/welchbj/bscan)