# Turbinia:数字取证工具的自动化和规模化

> 原文：<https://kalilinuxtutorials.com/turbinia-digital-forensics-tools/>

Turbinia 是一个用于部署、管理和运行分布式取证工作负载的开源框架。

它旨在自动运行常见的取证处理工具(即 Plaso、TSK、strings 等)，以帮助在云中处理证据，扩展大量证据的处理，并通过尽可能并行处理来缩短响应时间。

**工作原理**

Turbinia 由客户机、服务器和工作人员的不同组件组成。

这些组件可以运行在云中，本地机器上，或者两者的混合。Turbinia 客户端向 Turbinia 服务器请求处理证据。

Turbinia 服务器从这些传入的用户请求中创建逻辑作业，它创建并调度由工作人员运行的取证处理任务。

在可能的情况下，要处理的证据将按作业进行拆分，并且可以创建许多任务来并行处理证据。

一个或多个工作线程持续运行以处理来自服务器的任务。这些任务创造或发现的任何新证据都将反馈到 Turbinia 进行进一步处理。

**也可阅读-[RPI-Hunter:自动发现&向兰莓](https://kalilinuxtutorials.com/rpi-hunter/)投放有效载荷**

使用

初始安装和配置完成后，让系统正常运行的基本步骤是:

```
Start Turbinia server component with turbiniactl server command Start one or more Turbinia workers with turbiniactl psqworker Send evidence to be processed from the turbinia client with turbiniactl ${evidencetype} Check status of running tasks with turbiniactl status
```

turbiniactl 可以用来启动不同的组件，下面是基本用法:

**$ turbiniactl–help
用法:turbiniactl[-h][-q][-D][-a][-F][-o OUTPUT _ DIR][-L LOG _ FILE][-R REQUEST _ ID][-R][-S][-C][-V][-D]
[-F FILTER _ PATTERNS _ FILE][-J JOBS _ WHITELIST]
[-J JOBS _ BLACKLIST][-p POLL _ INTERVAL][-p POLL] –all _ fields 显示输出中的所有任务状态字段
-f，–Force _ evidence 在潜在的
不安全条件下强制证据处理请求
-o OUTPUT_DIR，–OUTPUT _ DIR OUTPUT _ DIR
输出的目录路径
-L LOG_FILE，–LOG _ FILE LOG _ FILE
日志文件
-r REQUEST_ID，–REQUEST _ ID REQUEST _ ID
创建具有此请求 ID 的新请求
-R，–Run _ local 完全在本地运行，没有任何 这可用于运行一次性任务
以在本地处理数据。
-S，–Server 无限期运行 Turbinia Server
-C，–use _ Celery 在使用 Celery/Kombu 进行任务
排队和消息传递(而不是 Google PSQ/pubsub)
，–version 显示版本
-D，–Dump _ json 转储 Turbinia 请求的 JSON 输出，而不是
发送给它
-F FILTER_PATTERNS_FILE，–FILTER _ PATTERNS _ FILE FILTER _ PATTERNS _ FILE
包含换行符的文件这个过滤后的输出将添加到完整输出
的
中-j JOBS_WHITELIST，–JOBS _ WHITELIST JOBS _ WHITELIST
是我们允许运行的作业的白名单(注意
它不会强制它们运行)。
-J JOBS_BLACKLIST，–JOBS _ black list JOBS _ black list
不允许运行的作业的黑名单
-p POLL_INTERVAL，–POLL _ INTERVAL POLL _ INTERVAL
轮询任务状态信息
-t TASK，–TASK 要在本地运行的单个任务的名称(必须与–run _ local 一起使用。
-w，–Wait 等待退出，直到给定请求的所有任务
都已完成
命令:

rawdisk 处理 rawdisk 作为证据
googleclouddisk 处理 Google Cloud 持久磁盘作为证据
Google Cloud Disk embedded
处理 Google Cloud 持久磁盘并嵌入
原始磁盘映像作为证据
目录处理目录作为证据
listjobs 列出所有可用的作业
psqworker 运行 PSQ 工作器
Celery**

用于处理 rawdisk 和 directory 证据类型的命令指定了 Turbinia 应该处理的证据的相关信息。

默认情况下，当添加新的要处理的证据时，turbiniactl 将作为一个客户端，向配置好的 Turbinia server 发送请求，否则如果指定了**–server**，它将启动自己的 Turbinia server 进程。

下面是 turbiniactl 添加要由 Turbinia 处理的原始磁盘类型证据的用法:

$ ./turbiniactl rawdisk -h
用法:turbiniactl raw disk[-h]-l LOCAL _ PATH[-s SOURCE][-n NAME]
可选参数:
-h，–help 显示此帮助消息并退出
-l LOCAL_PATH，–LOCAL _ PATH LOCAL _ PATH
证据的本地路径
-s 来源，–SOURCE SOURCE
证据来源的描述
-n NAME，–NAME 证据的描述性名称

**注释**

*   Turbinia 目前假设所有工作节点都可以平等地获得证据(例如，通过本地映射存储，或通过可附加的持久 Google 云盘等)。
*   并非所有证据类型都受支持
*   仍然只支持少量的处理作业类型，但是更多的正在开发中。

[**Download**](https://github.com/google/turbinia)