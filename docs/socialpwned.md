# SocialPwned:一个 OSINT 工具，允许从一个目标获取电子邮件，发布在社交网络上

> 原文：<https://kalilinuxtutorials.com/socialpwned/>

[![](img/79c05919110980995b4f304d57fa1cb7.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgGQDOdg4EIu3_4eH_1lXffqGOgqyZue1gWsqwx2HlDv22dgH9wKtGfZd8JPx_W1FBPGWZj3b3OLY2NAws25hPYVzFGp6addHEnaJC1PZjlDtrrWqLdqJRJRfRuilotW3bi8CcEfu8YHpfSXiugja4NEvoR3_1M-55eNRRQnPo_9cc8oKU2QrA_Eaxg=s676)

**social powned**是一个 OSINT 工具，允许从目标获取在 Instagram、Linkedin 和 Twitter 等社交网络上发布的电子邮件，以找到 PwnDB 或 Dehashed 中可能的凭据泄露，并通过 GHunt 获取谷歌帐户信息。

该工具的目的是在道德黑客的足迹阶段帮助搜索易受攻击的目标。一家公司的员工在社交网络中发布他们的电子邮件是很常见的，无论是职业的还是个人的，因此如果这些电子邮件的凭据被泄露，则有可能发现的密码在要审计的环境中被重复使用。如果不是这种情况，至少您会对遵循此目标创建密码的模式有所了解，并且能够以更高的效率执行其他攻击。

社交所有者使用不同的模块:

*   **Instragram** :利用@LevPasha 的非官方 Instagram API，开发了不同的方法来获取用户发布的邮件。需要 Instagram 帐户。
*   **Linkedin** :利用@tomquirk 的非官方 Linkedin API，开发了不同的方法来获取一家公司的员工及其联系方式(电子邮件、twitter 或电话)。此外，还可以将找到的员工添加到您的联系人中，以便您以后可以访问他们的联系人和信息网络。该模块还生成不同的文件，这些文件包含组织可能的用户名组合。Linkedin 帐户是必需的。
*   Twint :使用来自@twintproject 的 Twint，你可以跟踪用户发布的所有想要邮件的推文。Twitter 账户不是必须的。
*   受@davidtavarez 创建的工具 PwnDB 的启发，开发了一个模块，用于从找到的电子邮件中搜索所有凭据泄露。此外，对于每封电子邮件，都有一个 POST 请求，要求找出泄漏的来源。
*   **Dehashed** :提供清晰的密码，以及无法破解的密码哈希。有必要在 Dehashed 上付费来获得一个 API 密匙，但是当 PwnDB 很慢或者不提供结果时，这是一个很好的选择。
*   GHunt:使用@mxrch，GHunt 创建的工具，可以获得与谷歌邮件相关的信息，例如评论、个人资料图片、可能的位置或公共日历事件。

**安装**

**简单易行的方法**

**$ service docker start
$ docker pull mrtuxx/social powned
$ docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–help**

### 手动方式

**Tor** 的安装取决于您的系统。在 Debian 上:

$ sudo apt-get install for
$/etc/init . d/tor start

使用 **Git** 克隆存储库:

$ git 克隆 https://github.com/MrTuxx/SocialPwned.git
$ CD social powned
$ sudo pip 3 install–user–upgrade git+https://github . com/twint project/twint . git @ origin/master # egg = twint
$ sudo pip 3 install-r requirements . txt
$ sudo python 3 social powned . py–credentials . JSON–help

## 使用

要使用 Instagram 和 Linkedin 功能，你需要在每个社交网络上创建一个账户。凭证必须在 JSON 文件中指明:

**{
"instagram":{
"用户名":"用户名"，
"密码":"密码"
}，
"linkedin":{
"电子邮件":"电子邮件"，
"密码":"密码"
}，
"ghunt":{
"SID":"SID "，
"SSID":"SSID "，
"APISID":"APISID "，【APISID】。**

**注意:**GHunt 模块工作所需的 cookies 可以通过以下步骤获得

**用法:social powned . py[-h]–CREDENTIALS 凭据[–pwn db][–tor-PROXY PROXY][–insta gram][–info QUERY]
[–LOCATION LOCATION _ ID][–hashtag-ig QUERY][–search-users-ig 用户名][–search-ig 查询][–my-followers][–my-followers][–followers-ig][–followers-ig][–LinkedIn]
[–COMPANY COMPANY COMPANY _ ID][–search-companies 查询][]**

**输出格式**

每次运行 SocialPwned 时，都会生成一个具有以下格式的目录:

**输出
session _ year _ month _ day _ time
deashed
raw _ deashed . txt
social pwned _ deashed . txt
电子邮件** 

*   反散列目录在一个文件中包含原始 API 信息，在另一个文件中包含与电子邮件相关的密码。
*   pwndb 目录包含一个仅包含密码的文件，另一个包含密码和相关电子邮件的文件，最后一个文件添加了泄漏源。
*   电子邮件目录包含一个文件，其中包含所有获得的电子邮件。
*   instagram 目录包含一个文件，其中包含用户帐户及其相关的电子邮件地址。
*   twitter 目录包含一个文件，其中包含用户帐户及其相关的电子邮件地址。
*   linkedin 目录包含不同的文件，这些文件包含获得的用户名的组合。灵感来源于 linkedin2username 工具。
*   socialpwned.json 文件以 json 格式提供了 SocialPwned 及其不同模块获得的所有信息。其中每个项目的 ID 是电子邮件，如果您有关于用户的信息，但没有他的电子邮件，ID 将是他唯一的社交网络标识符。

**基本示例和组合**

**Instagram**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–info espaa**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–location 832578276**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–hashtag-ig some hashtag–pwn db**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–target-ig username–pwn db**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–target-ig username–followers-ig–followers-ig–pwn db**

**Linkedin**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials . JSON–LinkedIn–search-companies“我的目标”**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials . JSON–LinkedIn–search-companies“我的目标”-employees–pwn db**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials . JSON–LinkedIn–company 123456789–employees–pwn db**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials . JSON–LinkedIn–company 123456789–employees–add-contacts**

**docker run-v $(pwd)/credentials . JSON:/social wned/credentials . JSON-v $(pwd)/output:/social wned/output-it mrtuxx/social wned social powned . py–credentials credentials . JSON–LinkedIn–user-contacts user-id–pwn db**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials credentials . JSON–LinkedIn–user-contacts user-id–add-contacts**

**推特**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–Twitter–hashtag-tw some hashtag–pwn db–limit 200–de hashed**

**docker run-v $(pwd)/credentials . JSON:/social wned/credentials . JSON-v $(pwd)/output:/social wned/output-it mrtuxx/social wned social wned . py–credentials credentials . JSON–Twitter–target-tw username–all-tw–pwn db–de hashed–ghunt**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–Twitter–target-tw username–all-tw–followers-tw–pwn db**

**GHunt**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–ghunt–email-GH " email @ example . com "**

**脱灰**

**docker run-v $(pwd)/credentials . JSON:/social owned/credentials . JSON-v $(pwd)/output:/social owned/output-it mrtuxx/social owned social powned . py–credentials . JSON–de hashed–email-DH " email @ example . com "**

**连击**

**docker run-v $(pwd)/credentials . JSON:/social powned/credentials . JSON-v $(pwd)/output:/social powned/output-it mrtuxx/social powned social powned . py–credentials . JSON–insta gram–target-ig 用户名–followers-ig–followers-ig–LinkedIn–公司 123456789–员工–Twitter–target-tw 用户名–all-tw–pwn db–ghunt–de hashed**

**docker run-v $(pwd)/credentials . JSON:/social wned/credentials . JSON-v $(pwd)/output:/social wned/output-it mrtuxx/social wned social wned . py–credentials . JSON–insta gram–target-ig 用户名–LinkedIn–target-in 用户名–Twitter–target-tw 用户名–all-tw–pwn db–ghunt–de hashed**

[**Download**](https://github.com/MrTuxx/SocialPwned)