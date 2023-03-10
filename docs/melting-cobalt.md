# Melting-Cobalt:一个 Cobalt Strike 扫描器，将检测到的 Team Server 信标检索到一个 JSON 对象中

> 原文：<https://kalilinuxtutorials.com/melting-cobalt/>

[![](img/a69bbf66751108ad7d93e86e70d2cb1a.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjI4-Nh28PKbTHKisOfTcH2O54MFmj-HDmoFI_CXG1LWe-udv2bFrRvUCN_fS1vevEmyrmU1EF3qxM1QIlvhc8BTZkM34wyXZ3FshgMpUuu59BPgJ4b3XcMmgHM-42_qj-qBt6tnDjvttJrhPavXa0f5b3tkRBvGdvqkFDaPffoD2d6EXDuHCkcIEdN=s728)

**熔化钴**工具，用于搜寻/挖掘钴撞击信标，并“减少”其信标配置，以备日后索引。狩猎可以是大范围的，也可以是互联网范围的，使用安全路径、Shodan、ZoomEye 或 IP 列表等服务。

**入门**

*   安装熔融钴
*   配置您的令牌开始狩猎
*   布雷信标开始减少它们
*   审查结果`**cat results.json | jq**`

**安装**

要求:`**virtualenv**`和`**python3.8+**`

*   `**git clone https://github.com/splunk/melting-cobalt && cd melting-cobalt**`将项目和光盘克隆到项目目录中。
*   `**pip install virtualenv && virtualenv -p python3 venv && source venv/bin/activate && pip install -r requirements.txt**`创建 Virtualenv 并安装需求。

继续配置 SecurityTrails、Shodan 或 ZoomEye API 密钥。

**配置** `melting-cobalt.conf`

将`**melting-cobalt.conf.example**`复制到`**melting-cobalt.conf**`！

确保为一个可用的提供程序设置令牌。如果您需要为您的帐户创建一个，请遵循[这些](http://need wiki page)说明。

配置示例:

**【全局】**
**output = results . json
#将匹配项存储在 JSON 此处
log _ path = melting-cobalt . log
#设置日志文件的 log _ path
log _ level = INFO
#设置日志文件的日志级别
#可能值:INFO，ERROR，VERBOSE
nse _ script = grab _ beacon _ config . NSE
#获取 cobalt 配置的 NSE 脚本的路径。这是专门使用 https://github.com/whickey-r7/grab_beacon_config
搜索=搜索。yml
#包含不同的搜索运行在每个互联网扫描服务提供商(如 shodan，zoomeye，安全线索)时，狩猎队服务器。
# shod an _ token = token here
shod an token for search
zoo meye _ token = token here
zoo meye token for search
security trails _ token = token here
security trails token for search**

**搜索互联网**

要修改跨不同提供者执行的默认挖掘，请定制`**search.yml**`。默认熔化-钴搜索示例如下。

运行:

`**python melting-cobalt.py**`

**搜索 IP 列表**

用潜在钴罢工 C2 IPs 填充`**ips.txt**`一条新生产线交付，例如:

**1.1.1.1
2.2.2.2
3.3.3.3**

运行:

`**python melting-cobalt.py -i ips.txt**`

如果你需要来自猎人的灵感，我们强烈推荐:

*   DFIR 报告
*   真棒-钴-罢工
*   钴罢工机器人

**用途**

**用法:melting-cobalt . py[-h][-c CONFIG][-o OUTPUT][-v][-I INPUT]
扫描开放的 cobalt strike 团队服务器，获取它们的信标配置，并将其作为 json 日志写入，以便由任何分析工具
如 splunk、elastic 等进行分析..
可选参数:
-h，–help 显示此帮助消息并退出
-c CONFIG，–CONFIG CONFIG
CONFIG 文件路径
-o OUTPUT，–OUTPUT 输出
文件写入结果，默认为 results.json.log
v，–version 显示当前 melting-cobalt 版本
i INPUT，–INPUT 输入
换行 delivered file of cobalt strike server IPS 以获取信标配置。ips.txt 示例**

**搜索示例**

以下搜索是现成的，更多搜索可能会添加到`search.yml`以获取更多数据。

**庄丹**

##### 找到特定的 JARM 签名，开箱后我们跟踪钴击 4.x

`**'ssl.jarm:07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1'**`

##### 通过 HTTP 头和端口过滤，以减少有噪声的结果

`**'ssl.jarm:07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1 port:"22, 80, 443, 444, 1234, 2000, 2222, 3000, 3780, 4000, 4443, 6379, 7443, 8443, 8080, 8081, 8082, 8087, 8088, 8099, 8089, 8090, 8181, 8888, 8889, 9443, 50050" HTTP/1.1 404 Not Found Content-Length: 0'**`

##### shod an 检测到团队服务器

`**'product:"cobalt strike team server"'**`

*注意*:会产生很多嘈杂的结果，除非你想烧掉你的许可积分，否则不要实际安排。

##### 团队服务器证书序列号

`**'ssl.cert.serial:146473198'**`

**安检通道**

##### 查找特定的 JARM 签名

`**'SELECT address, ports.port FROM ips WHERE jarm = "07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1"'**`

##### 通过 HTTP 头和端口过滤以减少噪音 nmap_results

`**'SELECT address, ports.port, isp.name_normalized, ports.port, address, asn.number, jarm, http.headers.raw FROM ips WHERE jarm = "07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1" OR jarm = "07d14d16d21d21d07c07d14d07d21d9b2f5869a6985368a9dec764186a9175" OR jarm = "2ad2ad16d2ad2ad22c42d42d00042d58c7162162b6a603d3d90a2b76865b53" AND http.headers.content_type = "text/plain" AND http.headers.raw = "content-length:0" AND ports.port IN (22, 80, 443, 444, 1234, 2000, 2222, 3000, 3780, 4000, 4443, 6379, 7443, 8443, 8080, 8081, 8082, 8087, 8088, 8099, 8089, 8090, 8181, 8888, 8889, 9443, 50050)'**`

[**Download**](https://github.com/splunk/melting-cobalt)