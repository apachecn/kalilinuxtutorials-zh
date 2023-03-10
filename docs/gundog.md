# Gundog:微软 365 Defender 中的引导狩猎

> 原文：<https://kalilinuxtutorials.com/gundog/>

[![Gundog : Guided Hunting In Microsoft 365 Defender](img/429491abd4e47302ea71fb39349f39df.png "Gundog : Guided Hunting In Microsoft 365 Defender")](https://1.bp.blogspot.com/-oo25HUiI-S4/YM7b9egMxDI/AAAAAAAAJok/HD8181esfqkya1dM8CUghnzfv7OrSTgZgCLcBGAsYHQ/s728/1%2B%25281%2529.png)

gun dog–微软 365 Defender 中基于 PowerShell 的引导狩猎

Gundog 在微软 365 Defender 中为你提供了引导狩猎。尤其是(如果不仅仅是)目前的电子邮件和端点警报。

**功能**

您提供一个 AlertID(您可能会通过电子邮件通知收到),然后 gundog 将搜索尽可能多的相关数据。它不像在门户网站中那样给你提供高级搜索的灵活性，但是它会给你一个快速的、第一次的警报、所有相关实体和一些丰富的概述。

它所做的所有搜索都基于警报时间戳，因此我们只关心警报之前或之后不久的事件。

它还为您提供了它搜索的每个实体的 PowerShell 对象，如$Network，它在 Microsoft 365 Defender DeviceNetworkEvents 表中找到的与此警报相关的所有内容。

**gundog 还推出了一些其他功能，让您的生活更加轻松:**

*   默认情况下，只显示最相关的数据(就是这样)
*   它尽可能地为您提供上下文:最后一次 AAD 登录&用户的 AAD 地址
*   可以自动过滤网络连接，仅显示更相关的连接(例如，删除与 Office 365 的连接)
*   地理位置(国家和城市)丰富了网络连接
*   在变量部分，您可以轻松地调整大多数参数，如每个查询的高级搜索时间范围
*   此外，它还在其他服务上搜索 IOC，如 abuse.ch、urlscan.io 或 ip-api.com。如果你在商业上使用他们，我要求你申请他们的付费服务。

在用 gundog 进行第一次评估后，你可以继续在入口中深入挖掘兔子洞。

请随意扩展 gundog 并向我发送拉请求！为了获得最佳的心理体验，请使用带有 gundog 的 Windows 终端 Dracula 主题。

**快速使用**

**强制参数:
–TenantID
–ClientID
–client secret
可选参数:
–健忘事件
(背景:gundog 要做的第一件事就是从事件 API 中查询最近 30 天的所有事件和警报。这些被保存到一个全局变量中。如果您重新启动 gundog，它将不会再次查询所有事件，除非您将健忘事件设置为 true。)**

**要求**

在 AAD 中注册一个新的 App，给它以下权限:(如何[注册一个 app](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/exposed-apis-create-app-webapp)

**微软图形
–目录。全部阅读
——IdentityRiskEvent。read . All
–IdentityRiskyUser。阅读所有
——安全事件。read . All
–用户。阅读
微软威胁防护
–高级狩猎。read all
–事件。read . All
Windows Defender ATP
–advanced query。读取所有
–警报。读取所有
–文件。读取所有
–Ip。read . All
–网址。全部读取
–用户。read . All
–漏洞。全部阅读**

[**Download**](https://github.com/jangeisbauer/gundog)