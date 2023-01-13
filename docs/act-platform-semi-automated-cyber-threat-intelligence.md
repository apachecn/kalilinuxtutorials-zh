# Act 平台:收集和交换威胁情报信息的开放平台

> 原文：<https://kalilinuxtutorials.com/act-platform-semi-automated-cyber-threat-intelligence/>

[![Act Platform : Open Platform For Collection & Exchange Of Threat Intelligence Information](img/9bb1f6487e5a53660cbad809d5e40c02.png "Act Platform : Open Platform For Collection & Exchange Of Threat Intelligence Information")](https://1.bp.blogspot.com/-Y584eJJFp1U/XYXLpNVZPoI/AAAAAAAACjA/hjvkfHwY5C0yrJ5tucr45TPfUnmyeLvrgCLcBGAsYHQ/s1600/ACT.png)

半自动网络威胁情报或 ACT 是由 mnemonic as 领导的一个研究项目，NTNU 奥斯陆大学、挪威安全局(NSM)、KraftCERT 和 Nordic Financial CERT 都参与了该项目。

ACT 项目的主要目标是开发一个网络威胁情报平台，以揭露网络攻击、网络间谍和破坏活动。该项目将产生数据丰富和数据分析的新方法，以便能够识别威胁物剂、其动机、资源和攻击方法。此外，该项目将开发新的方法、工作流程和机制，用于创建和分发威胁情报和对策，以阻止正在进行的攻击并防止未来的攻击。

在这个库中，ACT 平台的代码是在开源许可下发布的。

**也可阅读-[Shodan Eye:工具收集所有直接连接到互联网的设备的所有信息](https://kalilinuxtutorials.com/shodan-eye/)**

**安装**

**先决条件**

*   Java 8 来运行应用程序。
*   Maven 用于管理依赖性、构建代码、运行单元测试等。
*   阿帕奇·卡珊德拉的储存装置。支持 Apache Cassandra 3.x 的任何版本。
    *   从`**deployment-service/resources/cassandra.cql**` **导入 Cassandra 数据库模式。**
*   用于分度的[弹性搜索](https://www.elastic.co/products/elasticsearch)装置。需要 6.8 版的 Elasticsearch。
*   (可选)为多节点环境安装 [ActiveMQ](https://activemq.apache.org/) 。
*   (可选)安装用于运行集成测试的 [Docker](https://www.docker.com/) 。

**编译**

*   从存储库的根文件夹执行`**mvn clean install -DskipTests**`来编译代码。
*   然后按照[部署指南](https://github.com/mnemonic-no/act-platform/wiki/Architecture-and-Deployment-Guide)运行应用程序。

**测试**

*   通过`**docker pull cassandra**`下载一张卡珊德拉图片。
*   通过`**docker pull docker.elastic.co/elasticsearch/elasticsearch:6.8.3**`下载一张 Elasticsearch 图片。
*   通过`**docker pull webcenter/activemq**`下载一个 ActiveMQ 映像。
*   执行`**mvn clean install**`运行所有测试，包括集成测试。
*   执行`**mvn clean install -DskipSlowTests**`跳过集成测试。
*   默认情况下，集成测试将尝试连接到本地主机上的 Docker 和端口 2375。设置$DOCKER_HOST 环境变量来覆盖这种行为。

[**Download**](https://github.com/mnemonic-no/act-platform)