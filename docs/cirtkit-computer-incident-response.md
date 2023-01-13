# CIRTKit:计算机事故响应小组的工具

> 原文：<https://kalilinuxtutorials.com/cirtkit-computer-incident-response/>

CIRTKit 是计算机事故响应小组的工具。一个 DFIR 控制台来统治他们。构建在 Viper 框架之上。

**安装**

**数据库设置**

lib/核心/数据库. py

它需要一个数据库来存储恶意软件工件和调查数据。目前，它可以使用 SQLite 和 Postgres SQL 数据库。

如果您需要多个分析师协作进行调查，那么您需要将其设置为使用 Postgres，否则如果您希望在本地存储信息，您可以使用 SQLite。

*   **SQLite**

对于 SQLite，您可以简单地运行 CIRTKit，它将创建并连接到一个本地 SQLite 文件。或者您可以指定连接字符串来使用不同的文件。

*   **Postgres**

设置 Postgres 数据库，并使用刚刚配置的数据库的凭证编辑 database.py 顶部的行。

**也读作:** [Fwknop:单包授权端口敲门](https://kalilinuxtutorials.com/fwknop-packet-authorization-port-knocking/)

DB_USER = "
DB_PASSWD = "

**安装依赖关系**

您可以使用提供的 requirements.txt 文件“pip install -r requirements.txt”安装带有 pip (Python 打包系统)的 decencies

**执行**

python cirtkity.py

您还可以指定'-i '标志并指定特定的调查。如果不存在，CIRTKit 将创建一个新的调查

[**Download**](https://github.com/opensourcesec/CIRTKit)

**贷方:鲍勃**