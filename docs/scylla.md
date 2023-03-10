# Scylla:简单的信息收集引擎

> 原文：<https://kalilinuxtutorials.com/scylla/>

[![Scylla : The Simplistic Information Gathering Engine](img/ebc01c9a530be3686ce98dc72e65744a.png "Scylla : The Simplistic Information Gathering Engine")](https://1.bp.blogspot.com/-DOerJvlj3QY/YHb9kdq6SuI/AAAAAAAAItI/uDxhDbIXzucDGQeKqQJj_kSYbh3q8gkjACLcBGAsYHQ/s728/Screen%2BShot%2B2020-05-10%2Bat%2B6.png)

**Scylla** 是 Python 3.6 开发的 OSINT 工具。Scylla 允许用户在 Instagram & Twitter 账户、网站/网络服务器、电话号码和姓名上进行高级搜索。Scylla 还允许用户找到分配给某个用户名的所有社交媒体资料(主要平台)。在延续，锡拉有 shodan 支持，所以你可以在互联网上搜索设备，它也有深入的地理定位能力。

最后,“锡拉”有一个财务部分，允许用户检查信用卡/借记卡号是否被泄露/粘贴，并返回卡 IIN/BIN 上的信息。这是该工具的第一个版本，如果您想为 Scylla 贡献更多内容，请联系开发者。

**安装**

**git 克隆 https://www.github.com/DoubleThreatSecurity/Scylla
CD Scylla
sudo python 3-m pip install-r requirements . txt
python 3 Scylla . py–help**

**用途**

**python 3 Scylla . py–insta gram Dave Smith–Twitter Dave Smith**

*   **命令 1** 将返回指定 Instagram & Twitter 账户的账户信息。

**python 3 Scylla . py–用户名 johndoe**

*   **命令 2** 将返回与该用户名相关的所有社交媒体(主平台)资料。

**python 3 Scylla . py–用户名 johndoe -l="john doe"**

*   **命令 3** 将重复命令 2，但它也将对“-l”参数执行深入的 google 搜索。注意:当搜索带有空格的查询时，请确保在引号中的查询后面加上等号。如果您的查询没有空格，将是这样的:python 3 Scylla . py–username John doe-l query

**python 3 Scylla . py–google.com 信息**

*   **命令 4** 将返回关于网络服务器/网站的重要 WHOIS 信息。

**python 3 Scylla . py-r+14167777777**

*   命令 5 将转储该电话号码的信息(运营商、位置等。)

**python3 scylla.py -s apache**

*   **命令 6** 会根据你的 API 密匙转储 shodan 可以抓取的所有 apache 服务器的 IP 地址。该查询可以是 shodan 可以验证的任何内容。
*   给出了一个示例 API 密钥。我将推荐阅读下面的 API 通知，以获取更多信息。

**python 3 Scylla . py-s webcamxp**

*   **Command 7** 会根据你的 API key 转储 shodan 可以抓取的互联网上所有开放网络摄像头的 IP 地址和端口。你也可以只使用网络摄像头查询，但 webcamxp 返回更好的结果。
*   给出了一个示例 API 密钥。我将推荐阅读下面的 API 通知，以获取更多信息。

**python 3 Scylla . py-g 1.1.1.1**

*   命令 8 将对指定的 IP 地址进行地理定位。它将返回经度&纬度，城市，州/省，国家，邮政编码区域和地区。

**python 3 Scylla . py-c 123456789123456**

*   **命令 9** 将检索输入的信用卡/借记卡号的 IIN 信息。它还会检查卡号是否被泄露/粘贴。Scylla 将返回卡的品牌、卡的方案、卡的类型、货币、国家和 IIN 银行的信息。注:输入完整的卡号，如果你想看看它是否被泄露。如果您只想检查前 6-8 位数字(也称为 BIN/IIN 号码)的数据，只需输入信用卡/借记卡号的前 6、7 或 8 位数字。最后，所有这些生成的信息都是公开的，因为这是一个 OSINT 工具，不会生成任何透露细节的信息。这可以防止恶意使用该选项。

菜单

**用法:Scylla . py[-h][-v][-ig insta gram][-tw TWITTER][-u USERNAME]
[–INFO INFO][-r REVERSE _ PHONE _ LOOKUP][-l LOOKUP][-s SHODAN _ QUERY][-g GEO][-c CARD _ INFO]**

**可选参数:**
-h，–帮助显示此帮助消息并退出
-v，–version 返回 scyla 的版本【T10 –用户名用户名
查找与给定用户名
关联
的社交媒体资料(主平台)–信息信息返回关于指定网站(WHOIS)的信息
w/地理位置
-r 反向电话查找，–反向电话查找反向电话查找
返回关于指定电话号码的信息
(反向查找)
-l 查找，–查找查找查找
对给定
参数的前 35 项进行谷歌搜索 提供:经度，
纬度，城市，国家，邮政编码，地区等。
-c CARD_INFO，–CARD _ INFO CARD _ INFO
检查信用卡/借记卡号是否已粘贴到
违规…转储站点。还返回 IIN 的银行
信息

**API 通知**

用于反向电话号码查找的 API(免费包)最多有 250 个请求。现在在程序中使用的那个在不久的将来肯定会用完。如果你想继续生成 API 密匙，进入[https://www.numverify.com](https://www.numverify.com)，创建账户后选择自由计划。然后只需转到 scylla.py，用您帐户仪表板中的新 API 密钥替换原来的 API 密钥。将您的新密钥插入到 keys[]数组中(在源代码的顶部)。对于 Shodan API 密钥，它只是一个给程序的样本密钥。开发人员建议创建一个 shodan 帐户，并将您自己的 API 密钥添加到源代码(scylla.py)顶部的 shodan_api[]数组中。

**道德声明**

这个程序的开发者 Josh Schiavone 编写了以下代码，仅供教育和娱乐之用。生成的信息不得用于伤害、跟踪或威胁他人。Josh Schiavone 对滥用本程序不负任何责任。愿上帝保佑你们。

[**Download**](https://github.com/DoubleThreatSecurity/Scylla)