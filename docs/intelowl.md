# 英特尔:从单个 API 以多种方式大规模分析文件、域和 IP

> 原文：<https://kalilinuxtutorials.com/intelowl/>

[![IntelOwl : Analyze Files, Domains, IPs In Multiple Ways From A Single API At Scale](img/b7a8dd7f012b88707650a7004344c788.png "IntelOwl : Analyze Files, Domains, IPs In Multiple Ways From A Single API At Scale")](https://1.bp.blogspot.com/-NzPODXi8Rok/X0gVjnpmtnI/AAAAAAAAHb4/zWih2v7ZC28NqKSHX3-uM-l7AAdeVcy_wCLcBGAsYHQ/s728/intel_owl.png)

**英特尔**由**分析器**组成，运行这些分析器可以从外部来源(如 VirusTotal 或 AbuseIPDB)检索数据，或者从内部分析器(如 Yara 或 Oletools)生成英特尔

这个解决方案是为每个人谁需要一个单一的点来查询有关特定文件或可观察的信息(域，IP，网址，散列)。

**特性**

*   完整的 django-python 应用程序
*   简单且完全可定制的 API 和分析器
*   克隆项目，设置配置，然后就可以运行了
*   官方前端客户端: **[英特尔-ng](https://github.com/intelowlproject/IntelOwl-ng)** 提供仪表板、分析数据可视化、请求新分析的易用表单等功能。

**可用的免费内部模块**

*   静态文档分析
*   静态 RTF 分析
*   静态 PDF 分析
*   静态 PE 分析
*   静态通用文件分析
*   用 ML 进行字符串分析
*   对等签名验证
*   PE 能力提取
*   仿真 Javascript 分析
*   Android 恶意软件分析

*   **需要额外配置的空闲模块**:
    *   Cuckoo(需要至少一个工作的 Cuckoo 实例)
    *   MISP(需要至少一个工作的 MISP 实例)
    *   Yara (Community、Neo23x0、Intezer 和 McAfee 规则已经可用。有机会添加您自己的规则)

**可用的外部服务**

*   **所需付费或试用 API 密钥**
    *   灰噪音 v2
*   必需的付费或免费 API 密钥
    *   VirusTotal v2 + v3
    *   杂交分析
    *   整数
    *   远视 DNSDB
    *   hunter . io–电子邮件搜索
    *   奥尼菲
    *   Censys.io
    *   安全轨道
    *   智力
    *   Pulsedive API(也可以在没有 API 键的情况下工作)
*   必需的免费 API 密钥
    *   GoogleSafeBrowsing
    *   AbuseIPDB
    *   肖丹
    *   honeybb
    *   艾伦沃·OTX
    *   max 他们都是
    *   Auth0
*   所需的访问请求
    *   CIRCL passived ns+passivesl
*   没有 api 密钥
    *   Fortiguard URL 分析器
    *   灰噪声 Alpha API v1
    *   塔罗斯的声誉
    *   Tor 项目
    *   Robtex
    *   威胁矿工
    *   虐待. ch MalwareBazaar
    *   虐待. ch URLhaus
    *   团队 Cymru 恶意软件哈希注册表
    *   特兰科等级
    *   谷歌文档
    *   CloudFlare DoH 经典
    *   CloudFlare DoH 恶意软件
    *   经典 DNS 解析

**法律声明**

作为该项目的用户，您必须阅读、接受并遵守下面列出的每个下载/安装软件包的许可条款。通过继续安装，您接受每个软件包的许可条款，并承认您对每个软件包的使用将受其各自许可条款的约束。

、[收紧](https://github.com/fireeye/stringsifter)、[剥离](https://github.com/jesparza/peepdf)、 [pefile](https://github.com/erocarrera/pefile) 、[工具](https://github.com/decalage2/oletools)、[【xlmmacrosbator】](https://github.com/DissectMalware/XLMMacroDeobfuscator)

**致谢**

该项目的创建和升级得益于以下组织:

*   切尔特戈
*   Hn/P

[**Download**](https://github.com/intelowlproject/IntelOwl)