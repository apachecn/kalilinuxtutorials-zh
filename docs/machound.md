# MacHound:审计 Bloodhound 在 MacOS 主机上收集和接收活动目录关系的扩展

> 原文：<https://kalilinuxtutorials.com/machound/>

[![MacHound : An extension to audit Bloodhound collecting and ingesting of Active Directory relationships on MacOS hosts](img/b875ebce174b36db710a2262a2c116d6.png "MacHound : An extension to audit Bloodhound collecting and ingesting of Active Directory relationships on MacOS hosts")](https://1.bp.blogspot.com/-nQQKzQjH2Oo/YOqS5tEBLcI/AAAAAAAAJ9U/mEMt6oK0LLQ8plcIfH3ilXbrfdyUAYW4QCLcBGAsYHQ/s728/MacHound%25281%2529.png)

MacHound 是 Bloodhound 审计工具的扩展，允许在 MacOS 主机上收集和获取活动目录关系。MacHound 收集 Mac 计算机上登录用户和管理组成员的信息，并将这些信息输入 Bloodhound 数据库。除了使用 HasSession 和 AdminTo 边之外，MacHound 还向 Bloodhound 数据库添加了三条新边:

*   can SHS-允许实体通过 SSH 连接到主机
*   CanVNC 允许 VNC 托管的实体
*   CanAE–允许在主机上执行 AppleEvent 脚本的实体

**数据收集**

**登录用户(HasSession)**

MacHound 使用 utmpx API 来查询当前活动的用户，并使用 OpenDirectory 和成员资格 API 来验证活动目录用户。

**管理组**

MacHound 收集下列本地管理组的 Active Directory 成员:

**管理员**

允许 root 操作的本地管理组。

**com.apple.access_ssh**

该本地组的成员被允许访问远程登录服务(SSH)。

**com.apple.remote_ae**

该本地组的成员被允许远程执行 AppleEvent 脚本。

**com . apple . access _ screen sharing**

允许本地组成员访问屏幕共享服务(VNC)

**组件**

机器分为两个主要部分:收集器和吸入器。

**收集器**

MacHound collector 是一个 Python3.7 脚本，它在 Active Directory 加入的 MacOS 主机上本地运行。收集器查询本地 OpenDirectory 和 Active Directory，以获取有关特权用户和组的信息。执行的输出是一个 JSON 文件，其中包含所有收集到的信息。

**吸入器**

MacHound ingestor 是一个 Python3.7 脚本，它解析输出 JSON 文件(每台主机一个)，连接到 neo4j 数据库，并将边缘插入数据库。英格斯托尔使用 Python 的 neo4j 库来查询进出 neo4j 数据库的信息。ingestor 必须在对 neo4j 数据库具有 TCP 访问权限的主机上执行。

**入门**

**要求**

MacHound 需要 Python3.7。ingestor 需要 python 3.7 的 neo4j 库。

**收集器**

**部署**

收集器应该在 MAC 上本地部署和执行。输出存储在本地，需要传输到运行 ingestor 的主机。收集器依赖于 Python3.7 中的内置库，不需要额外安装。可以使用 py2app 库将 MacHound 编译为应用程序，以简化部署。

**用途**

默认情况下，收集器不接受任何参数，查询所有信息，并将输出文件写入。/output.json。收集器必须以 root 用户身份执行。

**collector . py-o<output _ file>-c<Admin，CanSSH，CanVNC，CanAE，has session>[-v][-l log _ file _ path]**

**吸入器**

Ingestor 应部署在与 Bloodhound 的 neo4j 数据库有直接 TCP 连接的主机上，最好部署在 neo4j 数据库服务器上，以避免安全风险。ingestor 要求安装 Python 的 neo4j 驱动程序(参见要求文件)。

**ingestor . py<URL _ to _ neo4j>-u<用户名> -p <密码> -i < json_folder >**

[**Download**](https://github.com/XMCyber/MacHound)