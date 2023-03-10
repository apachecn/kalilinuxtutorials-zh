# 令人敬畏的密码破解:令人敬畏的工具、研究、论文和其他项目的精选列表

> 原文：<https://kalilinuxtutorials.com/awesome-password-cracking/>

[![](img/3309ce9e5667e49b9c2245d2b1154fa7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjcndc-dWn5q9xnNUvXqJNZIzKAf38iWXe-fMC6uvUyizG5g4YhlAONhUCUPgzBz0NLC0nNRN88sll4vpOQxnqzZVDZzb47IRVRwLAMac2pAfJim6us_XDgSNPD-zjuQRIgx2CgcJfdwyaZ5sX2mBHeFOFk4Adp2fQ5CSvv2a_ppsQgGTHfszTsY73l/s728/password_cracking%20(2).png)

**Awesome-Password-Cracking**是 Awesome 工具、研究、论文和其他与密码破解和密码安全相关的项目的精选列表。

投稿前请阅读指南！简而言之:

*   列表按字母顺序排序
*   如果有疑问，使用 awesome-lint
*   如果你认为一个项目不应该在这里打开一个问题

## 书

*   哈希破解:密码破解手册(v3)–密码破解手册 v3 是密码恢复(破解)方法、工具和分析技术的扩展参考指南。

## 云

*   cloud _ Crack——使用 Terraform 和 AWS 破解密码。
*   cloudcat——一个为哈希破解自动创建云基础设施的脚本。
*   cloud stomp——通过插件以最低的价格在 EC2 上为高 CPU/GPU 应用程序自动部署实例。
*   cloudtopolis——一个方便在 Google Cloud Shell 平台上安装和提供 Hashtopolis 的工具，快速且完全无人值守(而且是免费的！).
*   NPK——NPK 是一个分布式哈希破解平台，完全由 AWS 中的无服务器组件构建，包括 Cognito、DynamoDB 和 S3。
*   滥用 Google Colab 破解哈希。
*   rook–自动创建 AWS p3 实例，用于基于 GPU 的密码破解。

## 转换

*   7z 2 hashcat–从受密码保护的. 7z 档案中提取信息(和。sfx 文件),这样就可以用 hashcat 破解这些“散列”。
*   macin hash–将 macOS plist 密码文件转换为密码破解程序的哈希文件。
*   NetNTLM-Hashcat–将 John The Ripper/Cain 格式的散列(单数或批量)转换为 Hashcat 兼容的散列格式。
*   rube us-to-Hashcat–将 Rubeus kerberoasting 认证输出转换/格式化为 Hashcat 可读格式。
*   winhello 2 hashcat——使用这个工具可以从 WINDOWS HELLO PIN 中提取“哈希”。这个 hash 可以用 Hashcat 破解。
*   bitwarden 2 hashcat——一个将 Bitwarden 的数据转换成适合 hashcat 的散列的工具。
*   HC _ to _ 7z–将 7-Zip 哈希转换回 7z 档案。
*   hcx tools–将 cap/pcap/pcapng (gz 压缩)WiFi 转储文件转换为 hashcat 格式的便携式解决方案。
*   itunes _ backup 2 hashcat–从 Manifest.plist 文件中提取所需的信息，将其转换为与 hashcat 兼容的哈希。
*   mongodb 2 hashcat——从 MongoDB 数据库服务器中提取 hash 到 hashcat 接受的 hash 格式:-m 24100 (SCRAM-SHA-1)或-m 24200 (SCRAM-SHA-256)。

## 哈希卡特

Hashcat 是“世界上最快、最先进的密码恢复工具”以下是以某种方式与 Hashcat 直接相关的项目。

*   一套自动和轻度自动破解散列的客户端和服务器工具。
*   docker-hashcat–Ubuntu 18.04 CUDA、OpenCL 和 POCL 的最新 hashcat docker。
*   hash cat-stuff——hash cat 列表和东西的集合。
*   hashcat-utils——在高级密码破解中有用的小工具。
*   hash filter——读取 hash cat pot 文件，并将不同的类型解析到 sqlite 数据库中。
*   known _ hosts-hashcat——用 hashcat 破解 ssh known_hosts 文件的指南和工具。
*   pyhashcat–Python C API 绑定到 libhashcat。

### 自动化

*   auto scack——Hashcat 包装器，帮助自动化破解过程。
*   hashcat . launcher——运行和控制 hashcat 的跨平台应用程序。
*   hat——一个自动化的 Hashcat 工具，用于公共单词列表和规则，以加速在约定期间破解散列的过程。
*   hate _ crack——通过 TrustedSec 团队的 Hashcat 实现自动化破解方法的工具。
*   Naive hashcat–Naive hashcat 是一个即插即用的脚本，预先配置了简单的、经验测试过的“足够好”的参数/攻击类型。

### 分布式开裂

*   破解密码的队列和资源系统。
*   fittrack
*   hashtopolis——一个多平台客户端-服务器工具，用于将 hashcat 任务分发到多台计算机。
*   北海巨妖——一个多平台分布式暴力破解密码系统。

### 规则

*   clem9669 规则–hashcat 或 john 的规则。
*   hashcat 规则集合——可能是最大的 hashcat 规则集合。
*   hob 0 rules——基于统计和行业模式的 Hashcat 密码破解规则。
*   无脸男——无脸男项目的词汇表、规则和掩码(RootedCON 2019)。
*   NSA-rules——密码破解规则和由破解密码生成的 hashcat 掩码。
*   nyx geek-rules–Hashcat 和 John the Ripper 的自定义密码破解规则。
*   oneruleturethemall——“破解所有密码的一条规则。或者至少我们希望如此。”
*   pantagrule–从真实世界的泄漏密码中生成的大型 hashcat 规则集。

### 规则工具

*   dup rule–检测和过滤重复的 hashcat 规则。

### 网络界面

*   crackerjack 是用 Python 开发的 Hashcat 的 Web GUI。
*   裂缝
*   胡斯帕斯
*   hashview——用于密码破解和分析的 web 前端。
*   wave crack——wave stone 的 web 界面，用于使用 hashcat 进行密码破解。
*   web HashCat–web hashcat 是一个非常简单但高效的 hashcat 密码破解工具的 web 界面。

## 开膛手约翰

开膛手约翰是“一个开源的密码安全审计和密码恢复工具，可用于许多操作系统。”以下是以某种方式与开膛手约翰直接相关的项目。

*   BitCracker–BitCracker 是第一款开源密码破解工具，用于使用 BitLocker 加密的内存单元。
*   开膛手约翰的 GUI 前端。

## 杂项

*   hashID——识别不同类型散列的软件。
*   命名哈希——不知道它是什么类型的哈希？命名该散列将命名该散列类型！识别 MD5、SHA256 和 300+其他哈希。附带一个简洁的 web 应用程序。

## 网站

### 社区

*   hashcat 论坛——hashcat 开发者的论坛。
*   hash mob——一个成长中的密码恢复社区，旨在成为密码学爱好者的合作中心。
*   Hashkiller 论坛——一个拥有超过 20，000 名注册用户的密码破解论坛。

### 查找服务

*   cm D5–提供在线 MD5 / sha1/ mysql / sha256 加密和解密服务。
*   CrackStation 免费的哈希查找服务，也提供单词表。
*   Hashes.com——具有付费功能的哈希查找服务。
*   hash killer——一个带有论坛的哈希查找服务。
*   在线哈希破解-云密码恢复服务。

## 单词表工具

用于分析、生成和操作单词表的工具。

### 分析

*   PACK–开发用于帮助分析密码列表的实用程序集合，通过检测掩码、规则、字符集和其他密码特征来增强密码破解。
*   pcfg _ cracker——这个项目使用机器学习来识别用户的密码创建习惯。
*   Pipal 密码分析器。

### 生成/操纵

*   common-substr–从输入文本中提取最常见的子字符串的简单工具。专为破解密码而生。
*   Crunch–Crunch 是一个单词列表生成器，你可以在其中指定一个标准字符集或者你指定的字符集。Crunch 可以产生所有可能的组合和排列。
*   CUPP——一个让你通过用户档案数据生成单词表的工具，比如生日、昵称、地址、宠物或亲戚的名字等。
*   duplicut–从大量单词列表中删除重复的单词，不进行排序(用于基于字典的密码破解)。
*   gorilla——使用突变生成单词表或扩展现有单词表的工具。
*   键盘遍历生成器–为破解生成键盘遍历字典。
*   kw processor——高级键盘遍历生成器，具有可配置的基本字符、键盘映射和路径。
*   mask processor–高性能的字生成器，具有每个位置可配置的字符集。
*   mask uni——一个独立的快速单词生成器，秉承了 hashcat 的掩码生成器的精神，支持 unicode。
*   Mentalis 是一个用于自定义单词列表生成的图形工具。它利用常见的人类范例来构造密码，并可以输出完整的单词列表以及与 Hashcat 和 John the Ripper 兼容的规则。
*   Phraser——Phraser 是一个短语生成器，它使用 n-grams 和马尔可夫链来生成用于密码破解的短语。
*   PRINCE processor–使用 PRINCE 算法的独立密码候选生成器。
*   reph raser——一个基于 Python 的 phraser 的重新设计，使用马尔可夫链进行语言正确的密码破解。
*   Rling——RLI 下一代(Rling ),它是 hashcat 实用程序中 RLI 的一个更快的多线程、功能丰富的替代品。
*   基于每个位置的马尔可夫链的单词生成器。
*   TTPassGen——灵活且可脚本化的密码字典生成器，支持强力、组合、复杂规则模式等。
*   令牌反向器-单词列表生成器，用于破解安全令牌。
*   wiki raider——wiki raider 使您能够根据特定国家的维基百科数据库生成单词列表。

## Wordlists

### 特定语言

*   阿尔巴尼亚单词表——名字、姓氏和一些阿尔巴尼亚文学的混合。
*   丹麦电话单词表生成器——这个工具可以根据地区和/或用途(手机、固定电话等)生成丹麦电话号码的单词表。)对破解密码或模糊丹麦目标有用。
*   丹麦语单词表–用于破解丹麦语密码的丹麦语单词表集合。
*   这个项目旨在提供一个人可以用作基本密码的所有东西的法语单词列表。

### 其他

*   Packet Storm 单词表–多种语言的不同单词表的大量集合。
*   rocktastic–包括许多在野外观察到的密码和模式的排列。
*   rocky you 2021–rocky you 2021 . txt 是一个庞大的词汇表，由各种其他词汇表编译而成。
*   weak pass–大型单词列表的集合。

## 具体文件格式

### PDF

*   pdfrip–一个多线程的 PDF 密码破解工具，配备了常见的密码格式生成器和字典攻击。

### PEM

*   破解加密的 PEM 文件的工具。

### JKS

*   JKS 私钥解密高手–破解 JKS 文件中私钥条目的密码，破解 JKS 文件中私钥条目的密码。

### ZIP

*   bk Crack–利用 Biham 和 Kocher 的已知明文攻击破解传统 zip 加密。
*   fcrackzip

## 人工智能

*   ADAMS——通过深度学习和动态字典减少对真实世界密码强度建模的偏差。–用神经网络破解密码的代码。
*   rnn 密码-使用字符-rnn 学习和猜测密码。
*   rules finder——这个工具为给定的字典和密码列表找到有效的密码篡改规则(针对开膛手 John 或 Hashcat)。

[**Download**](https://github.com/n0kovo/awesome-password-cracking)