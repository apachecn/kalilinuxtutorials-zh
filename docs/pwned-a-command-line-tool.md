# Pwned——一个命令行工具，用于查询“我被 Pwned 了吗？”服务

> 原文：<https://kalilinuxtutorials.com/pwned-a-command-line-tool/>

一个命令行工具，用于查询特洛伊亨特的我被 pwn 了吗？使用 hibp Node.js 模块的服务。

## **Pwned 安装**

下载并安装 [Node.js](https://nodejs.org/en/download/) ，然后使用`npm`全局安装`pwned`:

```
npm install pwned -g
```

或者，您可以使用 [`npx`](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) 包运行器按需运行它:

```
npx pwned
```

## **如何 Ue？**

```
pwned <command>**
 **Commands:
  pwned ba <account|email>      get all breaches for an account (username or email address)
  pwned breach <name>           get a single breached site by breach name
  pwned breaches                get all breaches in the system
  pwned dc                      get all data classes in the system
  pwned pa <email>              get all pastes for an account (email address)
  pwned pw <password>           securely check a password for public exposure
  pwned search <account|email>  search breaches and pastes for an account (username or email
                                address)

Options:
  -h, --help     Show help                                                                 [boolean]
  -v, --version  Show version number                                                       [boolean]
```

**也可理解为**[**Hash pump——在各种哈希算法中利用哈希长度扩展攻击的工具**](https://kalilinuxtutorials.com/hashpump-tool-exploit-hash-length/)

### **例题**

获取帐户的所有违规:

```
$ pwned ba pleasebeclean@fingerscrossed.tld
✔ Good news — no pwnage found!
```

获取系统中的所有违规，将结果过滤到“adobe.com”域:

```
$ pwned breaches -d adobe.com
-
  Title:        Adobe
  Name:         Adobe
  Domain:       adobe.com
  BreachDate:   2013-10-04
  AddedDate:    2013-12-04T00:00:00Z
  ModifiedDate: 2013-12-04T00:00:00Z
  PwnCount:     152445165
  Description:  In October 2013, 153 million Adobe accounts were breached with each containing an internal ID, username, email, <em>encrypted</em> password and a password hint in plain text. The password cryptography was poorly done and <a href="http://stricture-group.com/files/adobe-top100.txt" target="_blank" rel="noopener">many were quickly resolved back to plain text</a>. The unencrypted hints also <a href="http://www.troyhunt.com/2013/11/adobe-credentials-and-serious.html" target="_blank" rel="noopener">disclosed much about the passwords</a> adding further to the risk that hundreds of millions of Adobe customers already faced.
  DataClasses:
    - Email addresses
    - Password hints
    - Passwords
    - Usernames
  IsVerified:   true
  IsFabricated: false
  IsSensitive:  false
  IsActive:     true
  IsRetired:    false
  IsSpamList:   false
  LogoType:     svg
```

通过漏洞名称获取单个漏洞站点:

```
$ pwned breach MyCompany
✔ No breach found by that name.
```

获取系统中的所有数据类，返回原始 JSON 结果以供外部/链式消费:

```
$ pwned dc --raw
["Account balances","Address book contacts","Age groups","Ages","Apps installed on devices","Astrological signs","Auth tokens","Avatars","Bank account numbers","Banking PINs","Beauty ratings","Biometric data","Browser user agent details","Buying preferences","Car ownership statuses","Career levels","Cellular network names","Charitable donations","Chat logs","Credit card CVV","Credit cards","Credit status information","Customer feedback","Customer interactions","Dates of birth","Deceased date","Deceased statuses","Device information","Device usage tracking data","Drinking habits","Drug habits","Eating habits","Education levels","Email addresses","Email messages","Employers","Ethnicities","Family members' names","Family plans","Family structure","Financial investments","Financial transactions","Fitness levels","Genders","Geographic locations","Government issued IDs","Health insurance information","Historical passwords","Home ownership statuses","Homepage URLs","IMEI numbers","IMSI numbers","Income levels","Instant messenger identities","IP addresses","Job titles","MAC addresses","Marital statuses","Names","Nationalities","Net worths","Nicknames","Occupations","Parenting plans","Partial credit card data","Passport numbers","Password hints","Passwords","Payment histories","Payment methods","Personal descriptions","Personal health data","Personal interests","Phone numbers","Physical addresses","Physical attributes","Political donations","Political views","Private messages","Professional skills","Profile photos","Purchases","Purchasing habits","Races","Recovery email addresses","Relationship statuses","Religions","Reward program balances","Salutations","School grades (class levels)","Security questions and answers","Sexual fetishes","Sexual orientations","Smoking habits","SMS messages","Social connections","Social media profiles","Spoken languages","Support tickets","Survey results","Time zones","Travel habits","User statuses","User website URLs","Usernames","Utility bills","Vehicle details","Website activity","Work habits","Years of birth","Years of professional experience"]
```

获取电子邮件地址的所有粘贴:

```
$ pwned pa nobody@nowhere.com
-
  Source:     Pastebin
  Id:         YrpQA60S
  Title:      null
  Date:       2018-01-24T07:54:15Z
  EmailCount: 16476
-
  Source:     Pastebin
  Id:         suPshHZ1
  Title:      null
  Date:       2017-09-06T03:41:33Z
  EmailCount: 20444
-
  Source:     Pastebin
  Id:         xyb8vavK
  Title:      null
  Date:       2015-06-01T00:16:46Z
  EmailCount: 8
-
  Source:     Pastebin
  Id:         DaaFj8Be
  Title:      CrackingCore - Redder04
  Date:       2015-04-05T22:22:39Z
  EmailCount: 116
-
  Source:     Pastebin
  Id:         9MAAgecd
  Title:      IPTV Yabancı Combolist
  Date:       2015-02-07T15:21:00Z
  EmailCount: 244
-
  Source:     Pastebin
  Id:         QMx1dPUT
  Title:      null
  Date:       2015-02-02T20:45:00Z
  EmailCount: 6607
-
  Source:     Pastebin
  Id:         zUFSee4n
  Title:      nethingoez
  Date:       2015-01-21T15:13:00Z
  EmailCount: 312
-
  Source:     AdHocUrl
  Id:         http://siph0n.in/exploits.php?id=4560
  Title:      BuzzMachines.com 40k+
  Date:       null
  EmailCount: 36959
-
  Source:     AdHocUrl
  Id:         http://siph0n.in/exploits.php?id=4737
  Title:      PayPalSucks Database 102k
  Date:       null
  EmailCount: 82071
-
 Source:     AdHocUrl
  Id:         http://balockae.online/files/BlackMarketReloaded_users.sql
  Title:      balockae.online
  Date:       null
  EmailCount: 10547
```

安全地检查密码，看它是否已经暴露在数据泄露中:

```
$ pwned pw Password1234
⚠ Oh no — pwned 3360 times!
```

搜索帐户的违规和粘贴(截断违规数据):

```
$ pwned search nobody -t
breaches:
  -
    Name: BattlefieldHeroes
  -
    Name: CannabisForum
  -
    Name: Forbes
  -
    Name: Gawker
  -
    Name: HackForums
  -
    Name: LoungeBoard
  -
    Name: PokemonCreed
  -
    Name: Win7Vista
pastes:   null
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/wKovacs64/pwned)