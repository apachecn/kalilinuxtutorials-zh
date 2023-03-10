# 阴谋核心:发现你的攻击面

> 原文：<https://kalilinuxtutorials.com/intrigue-core-external-attack/>

[![Intrigue Core : Discover Your Attack Surface](img/00b580860a07f3d1e0b99444d841936a.png "Intrigue Core : Discover Your Attack Surface")](https://4.bp.blogspot.com/-ts7CQhBbam0/XN4gu9g6GJI/AAAAAAAAAZg/z41s_UYzsh0oQWynJaNknRbAfR6_pYQjQCLcBGAs/s1600/Intrigue-Core.png)

**Intrigue Core** 是一个用于外部攻击面发现和自动化 OSINT 的框架。有许多使用案例:

*   应用程序和基础架构(资产)发现
*   安全研究和漏洞发现
*   恶意软件活动研究&指标充实
*   探索性研究

**开发者**

要开始设置开发环境，请遵循下面的说明！

**建立开发环境**

遵循适当的安装指南:

*   流浪(首选)–[http://core . intrigue . io/getting-started-with-intrigue-core-on-vagger-virtualbox/](http://core.intrigue.io/getting-started-with-intrigue-core-on-vagrant-virtualbox/)
*   docker-[https://core . intrigue . io/2017/03/07/using-intrigue-core-with-docker/](https://core.intrigue.io/2017/03/07/using-intrigue-core-with-docker/)

现在您有了一个工作环境，浏览到 web 界面。

**使用网络界面**

要使用 web 界面，请浏览至 [http://127.0.0.1:7777](http://127.0.0.1:7777/) 。一旦你能够连接，你可以按照这里的指示:【http://core.intrigue.io/up-and-running/ 

**配置系统**

许多任务通过外部 API 工作，因此需要配置密钥。要设置它们，请浏览到“配置”选项卡，然后单击模块的名称。您将被带到相关的注册页面，在这里您可以提供一个 API 密钥。

这些密钥最终存储在文件:config/config.json 中。

**也可阅读-[LNK 接吻者:AutoIt HackTool，Shortcuts.lnk 有效载荷生成器](https://kalilinuxtutorials.com/lnk-kisser/)**

**API**

Intrigue-core 是 API 优先构建的，允许 UI 中的所有功能都很容易自动化。提供了以下自动化方法。

**通过 core-cli 使用 API**

为了方便起见，添加了命令行实用程序 core-cli。

**列出所有可用的任务:**

**$捆绑销售。/core-cli.rb 列表**

**开始一项任务:**

**# # core-CLI . Rb start[项目名称][任务][类型#实体][深度][选项 1 =值 1 #……#……][处理程序][策略名称][自动充实]
$ bundle exec。/core-CLI . Rb start new _ project create _ entity DNS record # intrigue . io 3
get entity:{ " type " =>" DNS record "，" name"= > "intrigue.io "，" details " =>{ " name " =>" intrigue . io " } }
任务结果:{"result_id":66103}**

**通过 curl 使用 API**

你可以用 curl 来驱动框架。请参见下面的示例:

**$ curl-s-X POST-H " Content-Type:application/JSON "-d ' { " task ":" create _ entity "，" entity": { "type": "DnsRecord "，" attributes": { "name"**

[**Download**](https://github.com/intrigueio/intrigue-core)