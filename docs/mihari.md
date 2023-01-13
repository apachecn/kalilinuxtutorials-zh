# Mihari:连续运行 OSINT 查询和管理结果的助手

> 原文：<https://kalilinuxtutorials.com/mihari/>

[![Mihari : A Helper To Run OSINT Queries & Manage Results Continuously](img/620b76f859c4192d652cfe9dafb892ec.png "Mihari : A Helper To Run OSINT Queries & Manage Results Continuously")](https://1.bp.blogspot.com/-w6y_WO93Xls/X1KFySWwFPI/AAAAAAAAHd0/4pKvYuKKiEYU_EkiewLt3a7-gkqSjT0NgCLcBGAsYHQ/s728/eyecmihari-1%25281%2529.png)

Mihari 是运行查询的助手&持续管理结果。Mihari 可用于 C2、登陆页面和钓鱼搜索。

它是如何工作的？

*   Mihari 对 Shodan、Censys、VirusTotal、SecurityTrails 等进行查询。并从结果中提取工件(IP 地址、域、URL 和散列)。
*   Mihari 检查 DB (SQLite3 或 PostgreSQL)是否包含工件。
    *   如果它不包含工件:
        *   米哈里在飞机上制造了一个警报。(可选)
        *   Mihari 向 Slack 发送通知。(可选)
        *   米哈里在 MISP 创造了一个事件。(可选)

**截图**

*   五级警报示例

![](img/c7fb2a3aef7a7a89fffd7340f1dca3fa.png)

*   时差通知示例

![](img/3ff494625c46b8e03dc0e9f6563a9f3d.png)

*   MISP 事件示例

![](img/ef773d4e60ac8b6a7712f48c76016906.png)

**要求**

*   Ruby 2.6+版本
*   SQLite3
*   libpq

**# For Debian/Ubuntu**
apt-get 安装 sqlite3 libsqlite3-dev libpq-dev

**安装**

**宝石安装 mihari**

或者你可以用 Docker 来使用这个工具。

**码头工拉妮丝/米哈里**

**基本用法**

默认情况下，Mihari 支持以下服务。

*   [二进制边缘](https://www.binaryedge.io/)
*   [Censys](http://censys.io)
*   [CIRCL 被动 DNS](https://www.circl.lu/services/passive-dns/) / [被动 SSL](https://www.circl.lu/services/passive-ssl/)
*   [crt.sh](https://crt.sh/)
*   [糖尿病儿科](https://dnpedia.com/)
*   [域名寄存器](https://dnstwister.report/)
*   奥尼菲
*   [OTX](https://otx.alienvault.com/)
*   [被动总计](https://community.riskiq.com/)
*   [安全轨道](https://securitytrails.com/)
*   [庄丹](https://shodan.io)
*   [Spyse](https://spyse.com)
*   [urlscan.io](https://urlscan.io)
*   [VirusTotal](http://virustotal.com)
*   ZoomEye

**$ mihari**
**命令:**
–mihari alerts #显示服务器上的警报
–mihari binary edge[查询] # BinaryEdge 主机按查询搜索
–mihari Censys[查询] # Censys IPv4 按查询搜索
–mihari CIRCL[域|SHA1] # CIRCL 被动 DNS/SSL 按域或 SHA1 证书指纹查找
–mihari crtsh[查询] # crt.sh 通过查询进行 DNPedia 域搜索
–mihari dnstwester[DOMAIN]#通过域进行 dnstwester 查找
–mihari free _ TEXT[TEXT]#通过自由文本与搜索引擎进行交叉搜索
–mihari help[COMMAND]#描述可用的命令或一个特定的命令
–mihari http _ hash #通过 HTTP 响应的哈希与搜索引擎进行交叉搜索(SHA256， MD5 和 murmurhash 3)
–mihari import _ from _ json #通过 STDIN 给出 JSON 输入
–mihari ony phe[QUERY]# ony phe 数据可以通过查询进行搜索
–mihari otx[IP | DOMAIN]#通过 IP 或域进行 otx 查找
–mihari passive _ dns[IP | DOMAIN]#通过 IP 或域使用被动 DNS 服务进行交叉搜索
–mihari passive _ SSL[SHA1]#交叉搜索 通过 ip、域、电子邮件或 SHA1 证书指纹进行被动全面查找
–mihari pulsed ive[ip | DOMAIN]# pulsed 通过 IP 或域进行主动查找
–mihari reverse _ whois[EMAIL]#通过电子邮件使用反向 whois 服务进行交叉搜索
–mihari security trails[IP | DOMAIN | EMAIL]# security trails 通过 IP 进行查找， 域或电子邮件
–mihari security trails _ domain _ feed[REGEXP]# security trails 新的域 feed 按 REGEXP 搜索
–mihari shod an[QUERY]# shod an 主机按查询搜索
–mihari spy se[QUERY]# spy se 按查询搜索
–mihari ssh _ FINGERPRINT[FINGERPRINT]#通过 SSH 指纹与搜索引擎交叉搜索(例如 dc:14:de:8e:d7:c1:15 urlscan 按给定查询搜索
–mihari virus total[IP | DOMAIN]# virus total resolutions 按 IP 或域查找
–mihari ZoomEye[QUERY]# ZoomEye 按查询搜索
**选项:**
[–CONFIG = CONFIG]#配置文件的路径

**交叉搜索**

Mihari 有交叉搜索功能。交叉搜索是跨多个服务的搜索。

您可以使用以下命令获得聚合结果。

| 命令 | Desc。 |
| --- | --- |
| 被动 _dns | 使用 CIRCL 被动 DNS、OTX、PassiveTotal、Pulsedive、SecurityTrails 和 VirusTotal 进行被动 DNS 查找 |
| 被动 _ssl | 使用 CIRCL passive SSL 和 PassiveTotal 进行被动 SSL 查找 |
| 反向 _whois | 使用 PassiveTotal 和 SecurityTrails 检索 Whois 查找 |
| http_hash | 使用 BinaryEdge(SHA256)、Censys(SHA256)、Onyphpe(MD5)和 Shodan(MurmurHash3)进行 HTTP 响应哈希查找 |
| 自由文本 | 使用 BinaryEdge 和 Censys 进行自由文本查找 |
| ssh _ 指纹 | 使用 BinaryEdge 和 Shodan 进行 SSH 指纹查找 |

**Http_Hash 命令**

`http_hash`命令的用法有点复杂。

$ mihari help HTTP _ hash

**用法:**
mihari HTTP _ hash

[–TITLE = TITLE]# TITLE
[–DESCRIPTION = DESCRIPTION]# DESCRIPTION
[–tags =一二三]# tags
[–MD5 = MD5]# MD5 hash
[–sha 256 = sha 256]# sha 256 hash
[–mm H3 = N]

使用该命令有两种方式。

第一个是传递`--md5`、`--sha256`和`--mmh3`参数。

**mihari http _ hash–MD5 = 881191 f 7736 b 5b 8 cfad 5959 ca 99 D2 a 51–sha 256 = b 064187 ebdc 51721708 ad 98 CD 89 dacc 346017 CB 0 FB 0457d 530032d 387 f1 ff 20 e–mm H3 =-1467534799**

另一个是传递`--html`参数。在这种情况下，HTML 文件的哈希是自动计算的。

**wget http://example.com-O/tmp/index . html 米哈里 http _ hash–html/tmp/index . html**

**示例用法**

**#Censys 查找熊猫 C2**
mihari censys '("PANDA "和" SMAdmin "和" la yui ")'–title "熊猫 C2"

**#VirusTotal 被动 DNS 查找一个假主机**
mihari virus total " jp post-hi . top "-title "假被动 DNS "

**#您可以传递一个" defanged "指示符作为输入**
mihari virustotal "]top”-title“假冒被动 DNS”

**从 JSON 导入**

**echo '{ "title": "test "，" description": "test "，" artifacts": ["1.1.1.1 "，" github.com "，" 2 . 2 . 2 . 2 "]} ' | mihari import _ from _ JSON**

输入是一个 JSON 数据，应该有标题，描述和工件的关键。tags key 是可选参数。

{
"title": "test "，
"description": "test "，
"artifacts": ["1.1.1.1 "，" github.com"]，
"tags": ["test"]
}

| 钥匙 | Desc。 | 必需或可选 |
| --- | --- | --- |
| 标题 | 警报的标题 | 需要 |
| 描述 | 警报的描述 | 需要 |
| 史前古器物 | 一组工件(支持的数据类型:ip、域、url、电子邮件、散列) | 需要 |
| 标签 | 一组标记 | 可选择的 |

**配置**

配置可以通过环境变量或 YAML 文件来完成。

| 钥匙 | 描述 | 默认 |
| --- | --- | --- |
| 数据库 | SQLite 数据库的路径或 DB URL(例如`postgres://postgres:pass@db.host:5432/somedb`) | `mihari.db` |
| BINARYEDGE_API_KEY | BinaryEdge API 密钥 |  |
| censys _ id | Censys API ID |  |
| CENSYS_SECRET | Censys 的秘密 |  |
| CIRCL_PASSIVE_PASSWORD | CIRCL 被动 DNS/SSL 密码 |  |
| CIRCL 被动用户名 | CIRCL 被动 DNS/SSL 用户名 |  |
| MISP _ API _ 端点 | MISP 网址 |  |
| MISP_API_KEY | MISP API 密钥 |  |
| ONYPHE_API_KEY | Onyphe API 密钥 |  |
| OTX_API_KEY | OTX API 密钥 |  |
| PASSIVETOTAL_API_KEY | PassiveTotal API 键 |  |
| PASSIVETOTAL _ 用户名 | PassiveTotal 用户名 |  |
| 脉冲驱动 _API_KEY | 脉冲驱动 API 密钥 |  |
| SECURITYTRAILS_API_KEY | SecurityTrails API 密钥 |  |
| SHODAN_API_KEY | Shodan API 密钥 |  |
| 松弛频道 | 松弛通道名称 | `#general` |
| SLACK_WEBHOOK_URL | Slack Webhook URL |  |
| SPYSE_API_KEY | Spyse API key |  |
| HIVE_API_ENDPOINT | 活动网址 |  |
| HIVE_API_KEY | Hive API 密钥 |  |
| URLSCAN_API_KEY | urlscan.io API 密钥 |  |
| 病毒总数 _API_KEY | VirusTotal API 密钥 |  |
| ZOOMEYE _ 密码 | ZoomEye 密码 |  |
| zoomeye _ usernamme 用户名 | ZoomEye 用户名 |  |

您可以使用 YAML 文件进行配置，而不是使用环境变量。

**mihari virus total 1.1.1.1–config/path/to/YAML . yml**

YAML 文件应该是如下所示的 YAML 散列:

**database:/tmp/mihari . db
the hive _ API _ endpoint:https://localhost
the hive _ API _ key:foo
virus total _ API _ key:foo**

您可以通过 status 命令检查配置状态。

**mihari 状态**

**如何创建自定义脚本？**

创建一个扩展`**Mihari::Analyzers::Base**`并实现以下方法的类。

| 名字 | Desc。 | @返回 | 必需或可选 |
| --- | --- | --- | --- |
| `#title` | 警报的标题 | 线 | 需要 |
| `#description` | 警报的描述 | 线 | 需要 |
| `#artifacts` | 一组工件(支持的数据类型:ip、域、url、电子邮件、散列) | 排列 | 需要 |
| `#tags` | 一组标记 | 排列 | 可选择的 |

**与 Docker 一起使用**

$ docker run–RM Nino Seki/mihari
**#注意，应该通过环境变量**
$ docker run–RM Nino Seki/mihari-e the hive _ API _ ENDPOINT = " http://the hive _ URL "-e the hive _ API _ KEY = " API KEY " mihari
**#或**
$ docker run–RM Nino Seki/mihari–env-file ~/. mihari . env mihari

[**Download**](https://github.com/ninoseki/mihari)