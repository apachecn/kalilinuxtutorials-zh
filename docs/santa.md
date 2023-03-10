# Santa:MAC OS 的二进制白名单/黑名单系统

> 原文：<https://kalilinuxtutorials.com/santa/>

[![Santa : A Binary Whitelisting/Blacklisting System For macOS](img/4a080010c396f436e67d18f1df9de5aa.png "Santa : A Binary Whitelisting/Blacklisting System For macOS")](https://1.bp.blogspot.com/-Wm6WtYEMSmc/XxQxirsxx7I/AAAAAAAAG7g/IOWa26_sz3ArlIrpXXnDVLkTHxZZIeM9QCLcBGAsYHQ/s1600/1.png)

**Santa** 是 macOS 的二进制授权系统。它由一个监视执行的内核扩展(或 macOS 10.15+上的系统扩展)、一个根据 SQLite 数据库的内容做出执行决定的 userland 守护进程、一个在发生阻塞决定时通知用户的 GUI 代理以及一个用于管理系统和使数据库与服务器同步的命令行实用程序组成。

它被命名为圣诞老人，因为它跟踪顽皮或善良的二进制文件。

圣诞老人是谷歌 Macintosh 运营团队的一个项目。

**文档**

圣诞老人文档存储在[文档](https://github.com/google/santa/blob/master/docs)目录中。这里有一个 Read the Docs 实例:[https://Santa . readthedocs . io](https://santa.readthedocs.io)。

这些文档包括部署选项、圣诞老人各部分如何工作的细节以及开发圣诞老人本身的说明。

**获得帮助**

如果你有问题或者需要帮助，圣诞老人开发小组是一个很好的地方。

如果你认为你有一个 bug，请随时报告[一个问题](https://github.com/google/santa/isues)，我们会尽快回复。

如果你认为你已经发现了一个漏洞，请阅读[安全政策](https://github.com/google/santa/security/policy)的披露报告。

**管理相关功能**

*   多种模式:在默认的监控模式下，除了那些被标记为阻塞的二进制文件，所有的二进制文件都被允许运行，同时被记录到事件数据库中。在锁定模式下，只允许运行列出的二进制文件。
*   事件日志记录:当 kext 被加载时，所有二进制启动都会被记录。在任一模式下，所有未知或被拒绝的二进制文件都存储在数据库中，以便以后进行聚合。
*   基于证书的规则，具有覆盖级别:不依赖于二进制文件的散列(或“指纹”)，可执行文件可以由它们的签名证书来允许/阻止。因此，您可以跨版本更新允许/阻止给定发布者使用该证书签名的所有二进制文件。只有当二进制文件的签名验证正确时，其证书才能允许二进制文件，但是二进制文件指纹的规则将覆盖证书的决定；也就是说，您可以允许列出一个证书，同时阻止用该证书签名的二进制文件，反之亦然。
*   基于路径的规则(通过 nsregularyexpression/ICU):这允许与托管客户端(配置文件的前身，使用相同的实现机制)中类似的功能，通过 mcxalr 二进制文件限制应用程序启动。这个实现带来了额外的好处，可以通过 regex 进行配置，并且不依赖于 LaunchServices。正如 wiki 中所详述的，在评估规则时，这是最低的优先级。
*   故障安全证书规则:你不能加入一个拒绝规则来阻止用于签署 launchd 的证书，也就是 pid 1，以及 macOS 中使用的所有组件。因此，每次操作系统更新中的二进制文件(在某些情况下是全新版本)都会被自动允许。这并不影响来自苹果应用商店的二进制文件，这些二进制文件使用各种证书，这些证书会定期为常见的应用程序更改。同样，你不能屏蔽圣诞老人本身，圣诞老人使用不同于其他谷歌应用程序的独立证书。

**意图&期望**

没有一个系统或进程能够阻止所有的攻击，或者提供 100%的安全性。写圣诞老人的目的是帮助保护用户免受伤害。人们经常下载恶意软件并信任它，给恶意软件凭证，或允许未知软件泄漏更多关于您系统的数据。作为一个集中管理的组件，Santa 可以帮助阻止恶意软件在大量机器中传播。独立地，圣诞老人可以帮助分析什么是运行在你的电脑上。

圣诞老人是深度防御策略的一部分，您应该继续以您认为合适的任何其他方式保护主机。

**安全&性能相关特性**

*   内核缓存:允许的二进制文件被缓存在内核中，所以只有在二进制文件没有被缓存的情况下，才进行请求所需的处理。
*   用户域组件相互验证:每个用户域组件(守护程序、GUI 代理和命令行实用程序)使用 XPC 相互通信，并在接受任何通信之前检查它们的签名证书是否相同。
*   Kext 只使用 KPI:内核扩展只使用提供的内核编程接口来完成它的工作。这意味着 kext 代码应该继续跨操作系统版本工作。

**已知问题**

*   Santa 只阻塞执行(execve 和 variants)，它不保护用 dlopen 加载的动态库、磁盘上已被替换的库或用 DYLD_INSERT_LIBRARIES 加载的库。从 0.9.1 版本开始，我们确实解决了某些 macOS 版本中出现的 __PAGEZERO 缺失问题。我们也在努力防范类似的攻击途径。
*   Kext 通信安全:kext 一次只接受一个客户端的连接，并且该客户端必须以 root 用户身份运行。我们还没有找到一种好的方法来确保 kext 只接受来自有效客户端的连接。
*   数据库保护:SQLite 数据库是带权限安装的，因此只有根用户可以读/写它。我们正在考虑进一步保护这一点的方法。
*   脚本:Santa 目前被编写为忽略任何非二进制的执行。这是因为在权衡管理成本与收益之后，我们发现不值得。此外，许多应用程序利用临时生成的脚本，我们不可能允许列表，不这样做会导致问题。如果对其他人有用，我们很乐意重新考虑这个问题(或者至少让它成为一个选项)。

**同步服务器**

*   `**santactl**`命令行客户端包括一个标志，用于与管理服务器同步，管理服务器上传机器上发生的事件并下载新规则。有几个开源服务器可以与之同步:
    *   基于 AppEngine 的服务器，实现了社交投票，使管理大型车队变得更加容易。
    *   一个简单的 golang 服务器，提供简单配置文件中的硬编码规则。
    *   [central](https://github.com/zentralopensource/zentral/wiki)–从多个来源提取数据并将配置部署到多个服务的集中式服务。
*   或者，`**santactl**`可以在本地配置规则(无需同步服务器)。

**Kext 签名**

macOS 10.9 及更高版本上的内核扩展必须使用 Apple 提供的带有内核扩展标志的开发者 ID 证书进行签名。如果没有它，加载扩展的唯一方法是启用 kext-dev-mode 或禁用 SIP，这取决于 OS 版本。

出于分发目的，对此有两种可能的解决方案:

1.  使用我们提供的 kext 的[预构建、预签名版本](https://github.com/google/santa/releases)。每次对 kext 代码进行更改时，我们都会更新您可以使用的预构建版本。这并不妨碍你对圣诞老人的非 kext 部分进行修改和分发。如果您对 kext 进行了更改并提出了一个 pull 请求，我们可以将它们合并并发布一个新版本的预签名 kext。
2.  申请自己的 [kext 签名证书](https://developer.apple.com/contact/kext/)。苹果公司只允许在组织内广泛发行，他们不会仅仅为了测试而发行。

**免责声明**

这不是谷歌的官方产品。

[**Download**](https://github.com/google/santa)