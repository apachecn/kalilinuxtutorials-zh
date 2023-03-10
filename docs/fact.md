# FACT:一个从机器集群中收集、处理和可视化法医数据的工具

> 原文：<https://kalilinuxtutorials.com/fact/>

[![](img/9c1fdd1d4b19ef48024b4ebc8c359495.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjjAOj0mYdzKyJ-cnJ1yL0cKKQMTk6iQLUE9I2zZjm4-1G4z7z7rMuSyN29-KtI1bZaXyP7PX6LPO2EpdzLqGydQjsX6cLrCJf7s8lyB8Py-Nb-4FW9D2Vsr_m0c60Eivgq_SZgdH2GdJl-RA3bZcq2_BkOKHKcNK24GF78JKvtJk9xTOfFHyelBX0_=s728)

**FACT** 是一个工具，用于收集、处理和可视化运行在云中或内部的机器集群中的取证数据。

**部署**

对于基本的单节点部署，我们建议使用 Docker 和 Docker Compose。首先，阅读`**docker-compose.yaml**`了解配置和要求。然后，使用以下命令启动堆栈:

**坞站-合成 up -d**

**安装**

要为部署安装 FACT

1.  Docker 构建单节点部署
2.  Kubernetes 多节点部署

对于开发环境，请参见开发人员文档

**Docker 构建单节点部署**

您可以使用我们的 Docker Compose 设置在 Docker 桌面支持的平台上运行 FACT。此设置还不能用于生产。

**先决条件**

1.  码头工人
2.  复合坞站
3.  大量磁盘空间用于存储磁盘映像
4.  至少 4GB 可用内存，建议 8GB

配置`**docker-compose.yml**`

从这个库下载`**docker-compose.ym**` [`l`](https://github.com/unicornunicode/FACT/raw/main/docker-compose.yaml) 。

在文本编辑器中打开它，用运行 Docker 的机器的 IP 地址替换`**${HOST_IP}**`。或者，在运行`**docker-compose**`的 shell 环境中设置`**HOST_IP**`。您可以使用您的操作系统工具找到您的 IP 地址，或者在使用 Docker Desktop 时，尝试使用`**host.docker.internal**`。

IP 地址可以是用于连接互联网的地址，或者在使用 Docker Desktop 时，是底层 Docker Desktop 虚拟机的内部 IP 地址。它应该可以从您的主机和 Docker 中访问。

**启动所有服务**

打开一个 shell，进入包含`**docker-compose.yml**`的目录，并使用以下命令启动所有服务:

**坞站-合成 up -d**

**使用事实**

查看用户指南。

**用户指南**

**概念**

*   控制者:操作的总指挥者。记录用户所做的事情，并将任务分配给工作人员。
*   工人:从管制员那里接任务。这些任务指导工人从目标中捕捉和分析证据。
*   目标:您希望从中获取证据的机器。

**UI**

一旦安装了 FACT，就可以通过在 web 浏览器中打开 http://localhost:3000 来打开 UI，开始使用 FACT。

**添加目标**

您可能要做的第一件事是添加一个目标。访问“目标”页面，将您希望从中获取证据的目标添加到事实中。给它一个显示名称以供参考(稍后在 Kibana 中使用)，并输入用于连接目标的用户、主机和端口。

您应该添加一个现有的 SSH 密钥对来连接到目标，或者生成一个新的密钥对并将其安装在目标上。将私钥粘贴到框中。

使用非 root 用户时，您应该选中“使用 sudo”复选框。

目前，“使用 sudo”只有在用户没有密码提示(`**NOPASSWD**`)的情况下才有效。

**发现磁盘**

在您收集磁盘之前，FACT 必须了解它们。选择您想要捕获的所有目标，然后按“扫描磁盘”。花些时间来发现每台机器上的块设备。

在幕后，它在每个目标上运行`**lsblk -lb**`。

**抓取磁盘镜像**

磁盘发现完成后，您可以选择要捕获的磁盘。选择块设备将捕获整个设备，包括它的所有分区。选择一个分区设备将只捕获该分区上的文件系统。一旦你完成挑选，按下“采集磁盘”。这可能需要几分钟、几小时或几天的时间，具体取决于您要捕获的数据量、您拥有的工作线程数量以及目标和工作线程的磁盘性能等因素。

在幕后，它在每个目标上运行`dd`,并通过 SSH 将设备传输给工作人员。

**分析磁盘图像**

捕获磁盘后，可以通过选择设备并按“摄取捕获”来开始分析。这将启动在收集的磁盘映像中摄取数据的过程。可能也需要一段时间。

**查看数据**

一旦摄取完成，通过访问 http://localhost:5601 打开 Kibana。

要查看事件日志，请打开菜单并访问“发现”。可能会提示您创建一个索引模式。创建一个索引模式`**fact-*-files**`或`**fact-***`来匹配所有事实索引。或者，选择一个文件时间属性(mtime、ctime 或 atime)作为时间字段，按该属性对条目进行排序。

创建索引模式后，您可以再次打开“Discover”来查看事件日志，并对其进行搜索和排序。

**显影**

有关设置开发环境、林挺和测试的详细信息，请参见开发人员文档。

**发展中的事实**

**要求**

*   计算机编程语言
*   诗意
*   节点. js
*   弹性搜索和 Kibana
*   相当大的磁盘空间用于存储磁盘映像
*   至少 4GB 可用内存，建议 8GB

**设置**

如果您还没有，克隆这个库。

使用以下方式安装开发依赖项:

**设置虚拟环境并安装依赖项
poem Install–no-root
进入虚拟环境
poem shell
安装 grpcwebproxy
python tools/download-grpcwebproxy . py
可选:安装 Git hooks 来检查您的代码并提交消息
python tools/hooks . py Install
可选:在 UI 上工作时
cd ui
npm install**

**检查**

在提交提交或拉取请求之前，考虑运行代码格式化程序、linter、类型检查和测试:

**安装了 git 钩子
git 提交
没有安装 Git 钩子
python tools/pre-commit . py**

如果您希望跳过 linter，请键入 checks 和 tests:

**安装了 git 钩子
SKIP_CHECKS=y git commit
没有安装 Git 钩子
SKIP _ CHECKS = y python tools/pre-commit . py**

**工具**

`**tools**/`中的所有工具必须从项目根目录运行。

**写消息**

对于提交消息和拉请求，我们遵循传统的提交 1.0.0:

**【可选范围】:**

我们使用以下类型:

*   专长:新功能
*   **修正**:一个错误修正
*   **文档**:仅文档变更
*   **style** :不影响代码含义的变化
*   **重构**:既不修复 bug 也不增加特性的代码变更
*   **测试**:增加缺失的测试或修正现有的测试
*   **ci** :对我们的 ci 配置文件和脚本的更改
*   **杂务**:不修改 src 或测试文件的其他变更
*   **在制品**:在制品

为了帮助您编写提交消息，您可以使用:

**询问您一系列关于提交的问题
MK commit–auto select**

**更新 gRPC 协议**

对`**.proto**`文件中定义的 gRPC 协议进行任何更改后，必须使用协议缓冲编译器重新生成服务、存根和类型。这可以通过运行以下命令来完成:

**如果你还没有进入虚拟环境
诗歌外壳
编译 Makefile 中指定的文件如果它们改变了
make proto
为 UI 做同样的事情
make proto-ts**

[**Download**](https://github.com/unicornunicode/FACT)