# WhatBreach:一个发现被入侵的电子邮件和数据库的工具

> 原文：<https://kalilinuxtutorials.com/whatbreach-breached-emails-databases/>

**WhatBreach** 是一个搜索被攻破邮件及其对应数据库的工具。它获取单封电子邮件或一系列电子邮件，并利用 haveibeenpwned.com 的[的 API 搜索它们，从那里(如果有任何违规)，它将搜索与数据库相关的 Dehashed 上的查询链接，并输出所有违规以及该电子邮件包含的所有粘贴(如果有)。](https://haveibeenpwned.com)

如果你试图找到数据库，传递一个特定的标志也会试图从 [databases.today](https://databases.today) 下载可用的免费公共数据库。

如果在公开列表中找到该查询，它将为您下载数据库，并将其保存到位于`**~/.whatbreach_home/downloads**`下的项目主文件夹中。

**也可阅读-[DNS lively:Easy Files&通过 DNS 进行有效负载交付](https://kalilinuxtutorials.com/dnslivery/)**

**例题**

例如，我们将使用`user@gmail.com`作为示例搜索:

(venv)admin @ Hades:~/what breach $ python what breach . py-e " user @ Gmail . com "
[I]开始搜索单个电子邮件地址:user@gmail.com
[I]搜索 HIBP 上被破坏的帐户涉及:user@gmail.com
[I]搜索 HIBP 上的粘贴转储涉及:user@gmail.com
[I]发现总共 67 个数据库破坏和总共 59 个粘贴涉及:user@gmail.com

被破坏的站点:|数据库链接:
粘贴# 26 | https://pastebin.com/b0zdYUzc https://pastebin.com/JFvBG4HW
Paste # 25 | https://pastebin.com/hi5yXRCn
Paste # 22 | https://pastebin.com/mVrrDb9d
Paste # 23 | https://pastebin.com/jBCPwT1e
Paste # 20 | https://pastebin.com/uyG5ggf8
Paste # 21 | https://pastebin.com/QrudBvXf
Paste # 28 | https://pastebin.com/6fZtANAb
Paste # 29 | https://pastebin.com/gffDmJ5X
……| …#为节省篇幅被截断
Paste # 13 | https://pastebin . com/rlvk 8j 3e
Paste # 12 | https://pastebin . com/Zan https://www.dehashed.com/search?query=ArmyForceOnline
Gawker | https://www.dehashed.com/search?query=Gawker
Paste # 9 | http://www.pemiblanc.com/test.txt
Paste # 8 | https://pastebin.com/EGS77pC4
Paste # 7 | https://pastebin.com/pQdmx6mc
Paste # 6 | https://pastebin.com/ZwUh4tcG
Paste # 5 | https://pastebin.com/RkdC5arB
MySpace | https://www.dehashed.com/search?query=MySpace
Paste # 3 | https://pastebin . com/guv 70 jqa
Paste # 2 | https://pastebin . com/2 eenex 9n
Paste # 1 | https://pastebin . com/RSD

您还可以选择抑制发现的粘贴:

(venv)admin @ Hades:~/what breach $ python what breach . py-e " user @ Gmail . com "-nP
[I]开始搜索单个电子邮件地址:user@gmail.com
[I]搜索 HIBP 上被破坏的帐户涉及:user@gmail.com
[I]搜索 HIBP 上的粘贴转储涉及:user@gmail.com
[w]抑制发现的粘贴
[ i ]发现总共 67 个数据库破坏，总共 0 个粘贴涉及:user@gmail.com

被破坏的站点:|数据库链接 https://www.dehashed.com/search?query=Dropbox
李特| https://www.dehashed.com/search?query=Leet
MySpace | https://www.dehashed.com/search?query=MySpace
my heritage | https://www.dehashed.com/search?query=MyHeritage
ArmyForceOnline | https://www.dehashed.com/search?query=ArmyForceOnline
17 media | https://www.dehashed.com/search?query=17Media
Xbox 360 iso | https://www.dehashed.com/search?query=Xbox360ISO
LinkedIn | https://www.dehashed.com/search?query=LinkedIn
quin street | https://www . de hashed . com/search？query = quin street
book mate | https://www . de hashed . com/search？query = book mate
…|…#截断以保存 https://www.dehashed.com/search?query=Tumblr
警察| https://www.dehashed.com/search?query=PoliceOne
记者| https://www.dehashed.com/search?query=Onverse
Interpals | https://www.dehashed.com/search?query=Interpals
seed peer | https://www.dehashed.com/search?query=Seedpeer
HeroesOfNewerth | https://www.dehashed.com/search?query=HeroesOfNewerth
bell 2017 | https://www.dehashed.com/search?query=Bell2017

以及发现的数据库:

(venv)admin @ Hades:~/what breach $ python what breach . py-e " user @ Gmail . com "-nD
[I]开始搜索单个电子邮件地址:user@gmail.com
[I]搜索 HIBP 上被破坏的帐户涉及:user@gmail.com
[I]搜索 HIBP 上的粘贴转储涉及:user@gmail.com
[I]发现总共 67 个数据库破坏和总共 59 个粘贴涉及:user@gmail.com
[w]隐藏发现的数据库

被破坏的站点:|数据库链接 https://pastebin.com/b0zdYUzc
Paste # 27 | https://pastebin.com/C6YUMUxk
Paste # 24 | https://pastebin.com/JFvBG4HW
Paste # 25 | https://pastebin.com/hi5yXRCn
Paste # 22 | https://pastebin.com/mVrrDb9d
Paste # 23 | https://pastebin.com/jBCPwT1e
…|…#截断以节省空间
Paste # 9 | http://www.pemiblanc.com/test.txt
Paste # 8 | https://pastebin.com/EGS77pC4
Paste # 7 | https://pastebin . com/pqdmx 6 MC
Paste # 6 | https://pastebin . com/zwuh 4 tcg【T17 https://pastebin.com/bUq60ZKA
糊# 44 | http://siph0n.in/exploits.php?id=3667
糊# 45 | https://pastebin.com/MAFfXwGA
糊# 46 | http://pxahb.xyz/emailpass/www.chocolate.at.txt
糊# 47 | https://pastebin.com/zchq7iQS
糊# 40 | https://pastebin.com/sj9eyM5w
糊# 41 | https://pastebin.com/wY9ghBM9
糊# 42 | https://pred.me/gmail.html
糊# 43 | https://pastebin . com/AnTUDMtj

我还实现了搜索电子邮件地址列表的能力，并检查该电子邮件是否可能是“十分钟电子邮件”，如果找到该电子邮件，它将提示您继续，因为使用该电子邮件的可能性几乎为零:

(venv)admin @ Hades:~/what breach $ python what breach . py-l test . txt-cT
[I]解析电子邮件文件:test.txt
[ i ]开始搜索总共 3 封电子邮件
[ i ]搜索 HIBP 上被破坏的帐户涉及:user@gmail.com
[I]搜索 HIBP 上的粘贴转储涉及:user@gmail.com
[I]发现总共 67 个数据库破坏，总共 59 个粘贴涉及:user@gmail.com

数据库链接:
粘贴# 26 | https://pastebin.com/b0zdYUzc
粘贴# 27 | https://pastebin.com/C6YUMUxk
粘贴# 24 | https://pastebin.com/JFvBG4HW
粘贴# 25 | https://pastebin.com/hi5yXRCn
粘贴# 22 | https://pastebin.com/mVrrDb9d
粘贴# 23 | https://pastebin.com/jBCPwT1e
粘贴# 20 | https://pastebin.com/uyG5ggf8
粘贴# 21 | https://pastebin.com/QrudBvXf
R2 games | https://www . de hashed . com/search？query = R2 games
nemo web | https://www . de hashed . com https://www.dehashed.com/search?query=ArmyForceOnline
Gawker | https://www.dehashed.com/search?query=Gawker
Paste # 9 | http://www.pemiblanc.com/test.txt
Paste # 8 | https://pastebin.com/EGS77pC4
Paste # 7 | https://pastebin.com/pQdmx6mc
Paste # 6 | https://pastebin.com/ZwUh4tcG
Paste # 5 | https://pastebin.com/RkdC5arB
MySpace | https://www.dehashed.com/search?query=MySpace
Paste # 3 | https://pastebin . com/guv 70 jqa
Paste # 2 | https://pastebin . com/2 eenex 9n
Paste # 1 | https://pastebin . com/RSD 在 HIBP 上搜索与以下内容相关的粘贴转储:someuser@gmail.com
[I]共找到 6 个数据库漏洞和 4 个粘贴:someuser@gmail.com

漏洞网站:|数据库链接:
Adobe | https://www.dehashed.com/search?query=Adobe
粘贴# 4 | http://xn-E1 alhsoq 4c . xn-p1ai/base/Gmail . txt
粘贴# 3 | https://pastebin.com/GUV70Jqa
粘贴# 2 | https://pred.me/gmail.html
粘贴# 1 | https://pastebin.com/VVgL8Fzp

该程序非常简单，但为了简单起见，我在下面提供了可接受的参数:

(venv)admin @ Hades:~/what breach $ python what breach . py–help
用法:what breach . py[-h][-e EMAIL][-l PATH][-nD][-nP][-cT][-d]

可选参数:
-h，–帮助显示此帮助消息并退出

强制选项:
-e EMAIL，–EMAIL
传递单个电子邮件扫描
-l PATH、-f PATH、–list PATH、 –no-pastebin 抑制 Pastebin 输出

其他选项:
-cT，–Check-十分钟
检查提供的电子邮件地址是否为十分钟
电子邮件
-d，–下载如果有一个
可用，尝试下载数据库

**安装**

**安装极其简单，只需运行 pip install-r requirements . txt**

**为什么**？

在我从事信息技术的时候，在研究和做 OSINT 的时候，我注意到需要找到电子邮件地址以及它们的密码。

我已经找到了可靠的工具，可以成功地做到这一点，并使这个过程变得快速和简单，但是我还没有找到一个工具，满足我的确切要求。

这个工具基本上是我个人对我认为电子邮件搜索应该如何工作的看法，并与数据库搜索和数据库下载联系在一起。

有什么更好的方法来侵入一封电子邮件，然后得到可能的密码以及所有已知的漏洞呢？

**待办事项**

*   使用 dehashed 时添加域搜索，以便我们可以搜索与域相关的所有内容，而不是特定的违规
*   添加使用 cookies 的能力，这样我们就可以下载 dehashed 了
*   加个蛮横幅，谁不喜欢蛮横幅？
*   添加更多数据库搜索
*   检查数据库中的哈希并验证哈希类型，也许将哈希存储到一个文件中进行破解？

[**Download**](https://github.com/Ekultek/WhatBreach)