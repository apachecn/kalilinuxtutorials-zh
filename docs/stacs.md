# Stacs:静态令牌和凭证扫描器

> 原文：<https://kalilinuxtutorials.com/stacs/>

[![](img/26dac445f22da1d7ad8eaf7cb64bb6ef.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjS6bATrCkBnPShgwybK_Sk6QHd74YjH7zdT9jmn4VElLx2Ngjh0-3BxSMi95-M6LujAA3r08M3ZxV4oCpFt5MvlLwQ1Uw2Vuk7flG_xhkTwDa8FeAukcv1cpNXvA7h5hwWKYFZHN9Z9OssozoDc9LN_WGS7tziCb41a1vUSvgXoxrbufzGeMi0whdY=s728)

**Stacs** 是一款 YARA 驱动的静态凭证扫描仪，支持二进制文件格式、嵌套归档分析、可组合规则集和忽略列表以及 SARIF 报告。

**STACS 支持什么？**

目前，STACS 支持递归解压缩 tarballs，gzips，bzips，zips，7z，iso，rpm 和 xz 文件。因为 STACS 处理的是检测到的文件类型，而不是文件名，所以自动支持基于这些类型的适当文件格式(例如 Docker 图像、Android APKs 和 Java JAR 文件)。

**谁应该用 STACS？**

STACS 是为任何发布二进制工件的团队设计的。STACS 为开发人员提供了自动检查静态凭证和密钥材料在发布中的意外包含的能力。

然而，这并不意味着 STACS 不能帮助 SaaS 应用程序、企业软件，甚至源代码！

例如，STACS 可用于在上传到公共和私有容器注册中心的 Docker 映像中查找静态凭证。它还可以用于查找意外编译到可执行文件、移动设备包和“企业档案”中的凭证，例如 Java 应用服务器所使用的凭证。

**它是如何工作的？**

STACS 使用运行时提供给 STACS 的“规则包”来检测静态凭证。这些规则包定义了一组针对提供给 STACS 的文件运行的 YARA 规则。当找到与规则的匹配时，生成“发现”。这些发现代表文件内部的潜在凭证，并被报告给开发人员以进行补救或“忽略”。

如果发现结果是误报，也就是说，匹配的不是真实的凭据，开发人员可以生成一组“忽略列表”，以确保这些匹配不会出现在未来的报告中。

STACS 的真正威力来自自动检测和解开嵌套的档案，以及可组合的忽略列表和规则包。

**忽略列表？**

为了允许灵活和协作的使用，STACS 支持可组合的忽略列表。这允许忽略列表包括其他忽略列表，这些忽略列表允许基于组织指南的“忽略树”的组成。这些忽略列表在使用许多相同框架或产品的组织中特别有用。如果一个团队已经将一个发现标记为假阳性，其他团队就不必对相同的发现进行分类。

**规则包？**

与忽略列表一样，规则包也是可组合的。这使得组织能够定义一组基线规则供所有团队使用，同时仍然允许团队维护特定于其产品的规则集。

**我怎么用？**

使用 STACS 最简单的方法是使用发布到 Docker Hub 的 Docker 图片。然而，STACS 也可以直接从 Python 的 PyPI 安装，或者通过克隆这个库来安装。请参见下面的相关章节开始使用！

一项基于云的服务即将推出，它允许直接集成到构建和发布管道中，以便在发布之前检测静态凭证！

**码头工人**

利用公布的图像，STACS 可以用来扫描文物了！STACS Docker 映像为要扫描的文件提供了许多卷装载，以便直接装载到扫描容器中。

例如，要扫描当前文件夹中的所有内容，可以运行以下命令(必须安装 Docker)。

**docker run \
–RM \
–mount type = bind，source=$(pwd)，target =/mnt/stacs/input \
stacs can/stacs:最新**

默认情况下，STACS 会将 SARIF 格式的任何结果直接输出到 STDOUT，为了保持有序，所有日志消息都将被发送到 STDERR。对于更高级的使用情形，还提供了许多其他卷装载。这些允许用户控制要使用的规则包、忽略列表和缓存目录。

**皮珀**

STACS 也可以直接从 Python 的 PyPi 安装。这提供了一个`**stacs**`命令，开发人员可以使用它在他们的本地开发环境中直接扫描项目。

STACS 可以直接从 PyPi 安装，使用:

**pip 安装堆栈**

[**Download**](https://github.com/stacscan/stacs)