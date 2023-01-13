# Agente:分布式简单而强大的发布管理和监控系统

> 原文：<https://kalilinuxtutorials.com/agente/>

[![Agente : Distributed Simple & Robust Release Management & Monitoring System](img/ec16970a5e8cf657f4fada36fa369acf.png "Agente : Distributed Simple & Robust Release Management & Monitoring System")](https://1.bp.blogspot.com/-fu4-bMYE-1A/XkP24ZycI9I/AAAAAAAAE6M/NjvKd2I8iEYTHWpIxHKRhOJeMf330EUNACLcBGAsYHQ/s1600/Agente%25281%2529.png)

Agente 是一个简单而健壮的分布式发布管理和监控系统。

**路线图**

*   核心系统
*   第一个工人代理
*   管理仪表板
*   Jenkins vs CI 工具扩展
*   管理仪表板
*   第一主代理
*   所有相关的第三方系统集成(版本控制、CI、数据库、排队等)。)

**也读作-[接管:子域接管漏洞扫描器](https://kalilinuxtutorials.com/takeover-sub-domain-vulnerability-scanner/)**

**要求**

*   Go > 1.11
*   雷伊斯·拉比特
*   一种数据库系统

**Docker 环境**

**对于 PostgreSQL**

**docker run–name agente _ PostgreSQL-e POSTGRES _ PASSWORD = 123456-e POSTGRES _ USER = agente-p 5432:5432-d POSTGRES

docker exec agente _ PostgreSQL psql–username = agente-c '创建数据库 agente _ dev'**

对于 rabbitq

dock run–hostname my-rabbit–agent _ rabbitq-e rabbitq _ default _ user = local-e rabbitq _ default _ pass = local-p 5672:5672-d rabbitq:3 管理

**开发**

git clone -b 开发 https://github.com/streetbyters/agente

go mod 厂商

**#开发模式**
go run。/cmd -mode dev -migrate -reset
去运行。/cmd-模式 dev

**#测试模式**
go run。/cmd-模式测试-迁移-重置
运行。/cmd 模式测试

**建造**

我们将首先发布适用于 Linux 环境的代理。
[详见](https://github.com/streetbyters/agente/blob/master/docs/build.md)

[**Download**](https://github.com/streetbyters/agente)