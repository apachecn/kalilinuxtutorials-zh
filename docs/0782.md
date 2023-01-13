# Memguard:用于在内存中存储敏感信息的安全软件飞地

> 原文：<https://kalilinuxtutorials.com/memguard-secure-software-enclave-for-storage-of-sensitive-information-in-memory/>

[![Memguard : Secure Software Enclave For Storage Of Sensitive Information In Memory](img/504bc9334a041834868178d7ba45e8ca.png "Memguard : Secure Software Enclave For Storage Of Sensitive Information In Memory")](https://1.bp.blogspot.com/-FCbqnyA6GPA/XUgehmeZpPI/AAAAAAAABsI/mZfwoY8Fms8odnwWnkOkxo4453A06aIkwCLcBGAs/s1600/Image-1.png)

**MemGuard** 安全软件飞地，用于在内存中存储敏感信息。该软件包试图降低敏感数据被暴露的可能性。它支持所有主要的操作系统，并且是用纯 Go 编写的。

**特性**

*   敏感数据分别使用 xSalsa20 和 Poly1305 在内存中加密和验证。该方案还能抵御冷启动攻击。
*   内存分配通过使用系统调用直接向内核查询资源来绕过语言运行时。这避免了来自垃圾收集器的干扰。
*   存储明文数据的缓冲区用保护页和金丝雀值来加强，以检测虚假访问和溢出。
*   努力防止敏感数据接触磁盘。这包括锁定内存以防止交换和处理核心转储。
*   实现了内核级不变性，因此试图修改受保护区域会导致访问冲突。
*   多个端点提供会话清除和安全终止功能以及信号处理，以防止留下剩余数据。
*   通过确保在恒定时间内完成数据的复制和比较，减少了旁道攻击。
*   通过利用垃圾收集器自动销毁变得不可到达的容器，可以减少意外的内存泄漏。

一些功能的灵感来自于[libna](https://github.com/jedisct1/libsodium)，所以归功于他们。

完整的文档和 API 的完整概述可以在[这里](https://godoc.org/github.com/awnumar/memguard)找到。有趣且有用的代码示例可以在[示例](https://github.com/awnumar/memguard/blob/master/examples)子包中找到。

**也可阅读-[red ghost:Linux 后期开发框架](https://kalilinuxtutorials.com/redghost-linux-post-exploitation-2/)**

**安装**

**$去找 github.com/awnumar/memguard**

我们**强烈**鼓励你为一个干净可靠的构建固定一个特定的版本。这可以通过使用[模块](https://github.com/golang/go/wiki/Modules)来完成。

**投稿**

*   使用包装并确定摩擦点。
*   阅读源代码并寻找改进。
*   给 [`./examples`](https://github.com/awnumar/memguard/blob/master/examples) 添加有趣有用的程序样本。
*   开发概念验证攻击和缓解措施。
*   提高与更多内核和架构的兼容性。
*   实现特定于内核和特定于 cpu 的保护。
*   利用 memguard 编写有用的安全和加密库。
*   提交性能改进或基准代码。

问题是用来报告错误和讨论提议的。拉取请求应该针对主服务器。

**未来目标**

*   能够将数据传输到加密的 enclave 对象或从加密的 enclave 对象传输数据。
*   捕捉分段错误，在崩溃前清除内存。
*   评估并改进现有策略，尤其是针对[保险箱](https://github.com/awnumar/memguard/blob/master/core/coffer.go)物品的策略。
*   将威胁模型正式化，并评估我们在这方面的表现。
*   利用所学到的经验，将补丁应用到 Go 语言和运行时的上游。

[**Download**](https://github.com/awnumar/memguard)