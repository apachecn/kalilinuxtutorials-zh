# Solr-GRAB:使用或不使用用户名和密码窃取 Apache Solr 实例查询

> 原文：<https://kalilinuxtutorials.com/solr-grab-steal-apache-solr-instance-queries-with-or-without-a-username-and-password/>

[![Solr-GRAB : Steal Apache Solr Instance Queries With Or Without A Username And Password](img/362d4b7bf4499c04cc6601924d8b19a1.png "Solr-GRAB : Steal Apache Solr Instance Queries With Or Without A Username And Password")](https://1.bp.blogspot.com/-DujCI922dc4/YLstiTOJfJI/AAAAAAAAJVY/p16F-Q35laMJx89I3rJwxgjQah3EneMAgCLcBGAsYHQ/s728/Solr-GRAB%25281%2529.png)

Solr-GRAB 是一个窃取 Apache Solr 实例查询的工具，不管有没有用户名和密码。

**注意:**本项目只能用于授权测试和教育目的。

**下载**

**git 克隆 https://github.com/GnosticPlayers/Solr-GRAB**

**用途**

您可以通过 Censys 搜索 Apache Solr 实例，使用 dork **`"Welcome To Solr"`** 或 **`"Apache Solr Admin"`。**要获取查询，只需访问 http 接入点，有时在端口 80、443 或 8080 上。

*   将“ [http://URLHERE/](http://urlhere/) ”替换为所需的 URL，如 **`"http://127.0.0.1/"`。**
*   将“PROJECTHERE/”替换为所需的项目条目，比如目录 **`"users/"`。**
*   在 apache solr 查询中，将“IDHERE”替换为 JSON 中每个条目唯一的 ID，例如 **`"id"`** 或 **`"global_id"`。**
*   最后，用查询中找到的行数替换“AMOUNTOFROWSHERE”，比如`**"74332"**`。

现在用: **`bash index.sh`执行。**

有时，您会遇到一个 404 未找到的错误。如果是这样，在`**"http://URLHERE/"**` & `**"PROJECTHERE"**`之间加上`**"/solr/"**`，比如: **`https://127.0.0.1/solr/users/`** 。这应该可以解决问题。

[**Download**](https://github.com/GnosticPlayers/Solr-GRAB)