# 武器库-侦查工具安装程序

> 原文：<https://kalilinuxtutorials.com/arsenal/>

[![](img/48a47808e0289d98241643844aaed607.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi4ENPqPOswZ2m6R8XwQU5hDqsF32xsCjkQD1M75mSKztchdJaYpSTre7JXnFZBWLr1Zp-I4mEwIZjZ3fZS2L1JO2stbo54YTu0MgaiDCa9M3b7ECjoEhtoihtefBYcNjW3BbWQ9bgpDtarko83bAgEGh9dVsetPVVt9S-l1G4DUcISqk95RUia_i6e/s728/Arsenal.png)

**Arsenal** 是一个简单的 shell 脚本(Bash ),用于为您的环境安装最重要的工具和需求，并节省安装所有这些工具的时间。

## 武器库中的工具

| 名字 | 描述 |
| --- | --- |
| 积累 | OWASP Amass 项目使用开源信息收集和主动侦察技术来执行攻击面的网络映射和外部资产发现 |
| ffuf | 一个用 Go 编写的快速 web fuzzer |
| dnsX | 快速和多用途的 DNS 工具包允许运行多个 DNS 查询 |
| 梅格 | meg 是一个获取大量 URL 的工具，但仍然对服务器很“友好” |
| 重力 | grep 的包装器，以避免输入常见的模式 |
| XnLinkFinder | 这是一个用于发现正在搜索目标的端点的工具 |
| httpX | httpx 是一个快速和多用途的 HTTP 工具包，允许使用 retryablehttp 库运行多个探测器，它旨在通过增加线程来保持结果的可靠性 |
| Gobuster | Gobuster 是一个用来暴力破解(DNS，打开亚马逊 S3 桶，网页内容)的工具 |
| 核心 | Nuclei tool 是一款基于 Golang 语言的工具，用于根据 nucleus 模板跨多个目标发送请求，从而避免误报或不相关的结果，并在各种主机上提供快速扫描 |
| 子 finder | Subfinder 是一个子域发现工具，它通过使用被动的在线资源为网站发现有效的子域。它具有简单的模块化架构，并针对速度进行了优化。subfinder 只做一件事——被动子域枚举，它做得很好 |
| 纳阿布 | Naabu 是一个用 Go 编写的端口扫描工具，它允许您以快速可靠的方式枚举主机的有效端口。这是一个非常简单的工具，可以对主机/主机列表进行快速 SYN/CONNECT 扫描，并列出所有返回回复的端口 |
| 资产查找器 | 查找与给定域潜在相关的域和子域 |
| http probe | 获取一个域列表，并探测工作的 http 和 https 服务器 |
| 令人震惊 | Knockpy 是一个 python3 工具，旨在通过字典攻击快速枚举目标域上的子域 |
| waybackurl | 从 Wayback 机器中获取*的已知 URL。域并在 stdout 上输出它们 |
| 对数传感器 | 一个强大的传感器工具，用于发现登录面板和 POST 表单 SQLi 扫描 |
| Subzy | 子域接管工具，它基于来自 can-i-take-over-xyz 的匹配响应指纹工作 |
| XSS-罢工 | 高级 XSS 检测套件 |
| antdns | 通过改变和置换发现子域 |
| Nosqlmap | NoSQLMap 是一款开源 Python 工具，旨在审计和自动执行注入攻击，并利用 NoSQL 数据库和使用 NoSQL 的 web 应用程序中的默认配置缺陷，从而从数据库中泄露或克隆数据 |
| 副蜘蛛 | 人类的参数挖掘器 |
| 戈斯皮德 | Go spider——用 Go 编写的快速网络蜘蛛 |
| 目击者 | Witness 是一个 Python 工具，由@CptJesus 和@christruncer 编写。它的目标是帮助你有效地评估你的目标的哪些资产应该首先关注。 |
| CRLFuzz | 用 Go 编写的 CRLF 漏洞快速扫描工具 |
| 东戈 403 | dontgo403 是一个绕过 40 倍错误的工具 |
| 变色龙 | 变色龙通过使用 wappalyzer 的技术指纹集以及为每种检测到的技术定制的词表，提供更好的内容发现 |
| 揭露 | uncover 是一个 go wrapper，使用知名搜索引擎的 API 来快速发现互联网上暴露的主机。它是按照自动化的思想构建的，因此您可以查询它，并使用您当前的管道工具来利用结果 |
| wpscan | WordPress 安全扫描仪 |
| 图表地图 | GraphQLmap 是一个脚本引擎，用于与 graphql 端点进行交互以进行测试 |
| 达尔福克斯 | DalFox 是一个强大的开源 XSS 扫描工具和参数分析器和实用程序，可以加快检测和验证 XSS 缺陷的过程。它带有一个强大的测试引擎，为酷黑客提供了许多利基功能！ |
| http 请求走私 | HTTP 请求走私检测工具 |
| 混合 | commix ([ comm]and[I]inject e[x]ploiter)是一个开源渗透测试工具，由 Anastasios Stasinopoulos (@ancst)编写，它可以自动检测和利用命令注入漏洞 |
| GoLinkFinder | 一个最小 JS 端点提取器 |
| JWT 工具包 v2 | JWT Tookkit 是一个验证，伪造，扫描和篡改 jwt(JSON 网络令牌)的工具包 |
| GitLeaks | 检查 git repos 中的秘密和密钥 |
| WhatWeb | 下一代网络扫描仪 |
| 阿尔俊 | Arjun 可以找到 URL 端点的查询参数。如果你不明白这是什么意思，没关系，继续读下去 |

## 阿森纳的要求

*   Python3
*   饭桶
*   红宝石
*   Wget
*   GO-Lang
*   生锈:快速:

## 围棋装置

```
 sudo apt-get remove -y golang-go
 sudo rm -rf /usr/local/go
 wget https://go.dev/dl/go1.19.1.linux-amd64.tar.gz
 sudo tar -xvf go1.19.1.linux-amd64.tar.gz
 sudo mv go /usr/local
 nano /etc/profile or .profile
 export GOPATH=$HOME/go
 export PATH=$PATH:/usr/local/go/bin
 export PATH=$PATH:$GOPATH/bin 
 source /etc/profile #to update you shell dont worry

```

## 如何安装

```
git clone https://github.com/Micro0x00/Arsenal.git
cd Arsenal
sudo chmod +x Arsenal.sh
sudo ./Arsenal.sh

```

[Click Here To Download](https://github.com/Micro0x00/Arsenal)