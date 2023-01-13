# SiteDorks:不同网站的搜索词

> 原文：<https://kalilinuxtutorials.com/sitedorks/>

SiteDorks 是一款工具，用于在不同网站上搜索**谷歌、必应、雅虎或 Yandex** 的搜索词。已经提供了一个默认列表，包含 **Github，Gitlab，Surveymonkey，Trello** 等。目前，有 241 个可呆网站的默认列表。当前存档的类别有:

*   分析(10)
*   云(35)
*   代码(38)
*   来文(27)
*   公司(3)
*   文档(36)
*   edu(3)
*   表格(11)
*   组织(13)
*   其他(4)
*   远程(1)
*   肖特纳(15)
*   社会(42)
*   存储(3)

**为什么是 SiteDorks？**

为什么不直接手动输入几个网站的傻瓜呢？因为:

*   查询不同的搜索引擎真的很容易。
*   呆瓜可以按 1 个或多个类别执行。
*   很容易为不同的用途创建不同的输入文件。
*   将新网站添加到您的搜索查询中可以通过将它们添加到输入文件中来安排。
*   它已经包括了很多无聊的网站。
*   可下载网站的列表会定期更新。
*   一些搜索引擎会忽略一个查询中的太多关键字/字符，使用参数计数很容易将你的呆子分成更多的查询。
*   它包含 Bugcrowd、HackerOne、Intigrity 和 YesWeHack 的列表。用一个命令你可以在几个 bug bounty 平台上搜索程序的域🙂

**安装**

Sitedorks 应该能够运行默认的 Kali Linux 安装，而无需安装额外的 Python 包。只需运行:

**git 克隆 https://github.com/Zarcolio/sitedorks**

如果你在运行 sitedorks 时遇到了麻烦，请给我一个问题，我会尽力解决它🙂

**用途**

```
usage: sitedorks [-h] [-cat <category>] [-count <count>] [-engine <engine>] [-file <file>] [-query <query>]
[-site <on|off|inurl>] [-excl <domains>] [-echo]

Use your favorite search engine to search for a search term with different websites. Use single quotes around
a query with double quotes. Be sure to enclose a query with single quotes it contains shell control characters
like space or ';', '>', '|', etc.

optional arguments:
  -h, --help            Show this help message, print categories on file (add -file to check other CSV
                        file) and exit.
  -cat <category>       Choose from 1 or more categories, use ',' (comma) as delimiter. Defaults to all
                        categories.
  -count <count>        How many websites checked per query. Google has a maximum length for queries.
  -engine <engine>      Search with 'google', 'baidu', 'bing', 'duckduckgo' 'yahoo' or 'yandex', defaults
                        to 'google'.
  -file <file>          Enter a custom website list.
  -query <query>        Enter a mandatory search term.
  -site <on|off|inurl>  Turn the 'site:' operator 'on' or 'off', or replace it with 'inurl:' (only for
                        Google), defaults to 'on'.
  -excl <domains>       Excluded these domains from the search query.
  -echo                 Prints the search query URLs, for further use like piping or bookmarking.

usage: sitedorks [-h] [-cat <category>] [-count <count>] [-engine <engine>] [-file <file>] [-query <query>]
                 [-site <on|off|inurl>] [-excl <domains>] [-echo]
```

**例题**

想用谷歌寻找包含各种内容的不同站点的“uber.com”？使用以下命令:

**site dorks-query“Uber . com”’**

想找“优步网站”(查询中有引号和空格)？使用以下命令:

**site dorks-查询“优步网站”**

想要搜索 yandex 的通信邀请，但将站点:排除在查询之外？只需使用以下命令:

**site dorks-cat comm-site disable-engine yandex-query Uber**

如果您想查看哪些类别已存档，例如使用 [hackerone](https://www.hackerone.com) 平台:

**site dorks-file site dorks-hacker one . CSV-cats**

[**Download**](https://github.com/Zarcolio/sitedorks)