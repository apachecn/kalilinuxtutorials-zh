# pastego:使用 go 和衰退语法抓取/解析 pastebin

> 原文：<https://kalilinuxtutorials.com/pastego-scrape-parse-pastebin-using-go-and-expression-grammar/>

[![Pastego : Scrape/Parse Pastebin Using GO And Expression Grammar](img/b513a13f76c6fb17e4986f02eac3ba10.png "Pastego : Scrape/Parse Pastebin Using GO And Expression Grammar")](https://1.bp.blogspot.com/-IeeYLzG0T8Q/X3xzfUPoemI/AAAAAAAAHu4/dPHk3NzKwSYSvbjA46wSsoJWOQiDhngkwCLcBGAsYHQ/s728/pastego%25281%2529.png)

**Pastego** 是一个使用 go 和语法表达式(PEG)的抓取/解析 Pastebin。

**安装**

`**$ go get -u github.com/notdodo/pastego**`

**用途**

搜索关键字区分大小写

`**pastego -s "password,keygen,PASSWORD"**`

您可以使用布尔运算符来减少误报

`**pastego -s "quake && ~earthquake, password && ~(php || sudo || Linux || '<body>')"**`

该命令将搜索具有`quake`但不具有`earthquake`字的库，以及具有`password`但不具有`php`、`sudo`、`Linux`、`<body>`字的库。

**用法:**`pastego [<flags>]`

**Flags:**

`–help`显示上下文相关的帮助(也可尝试–help-long 和–help-man)。

`-s, –search="pass"`要搜索的字符串，即:" password，ssh"

`-o, –output="results"`文件夹要保存的 bin

`-i, --ignore-case`搜索不区分大小写的字符串

支持的表达式/运算符:

` & & `–and

` | | `–or

`~ `–not `

'带空格的字符串' `

`(myexpression & &'带运算符')`

**按键组合**

`q`，`ctrl+c`:退出`pastego`
`k`，`↑`:显示上一个 bin
`j`，`↓`:显示下一个 bin
`n`:向前跳 15 个 bin
`p`:向后跳 15 个 bin
`N`:移动到下一个结果块(按字母顺序)
`P`:移动到上一个结果块(按字母顺序)
`d`:从文件系统中删除文件
`HOME`

**要求**

*   [goquery](https://github.com/PuerkitoBio/goquery)

`**go get -u "github.com/PuerkitoBio/goquery"**`

*   [中枢人物](https://github.com/alecthomas/kingpin)

`**go get -u "gopkg.in/alecthomas/kingpin.v2"**`

*   [gocui](https://github.com/jroimartin/gocui)

`**go get -u "github.com/jroimartin/gocui"**`

*   使用[鸽子](https://github.com/mna/pigeon)从 PEG 创建代码:

`**go get -u github.com/mna/pigeon**`

**免责声明**

你需要一个专业帐户来使用这个:pastebin 将**阻止/黑名单**你的 IP。

[pastebin 用于](https://pastebin.com/pro)

*   或者…
    *   增加每个请求之间的时间间隔
    *   创建一个脚本，在 pastebin 警告您时重新启动路由器
*   **进行中……**
    *   添加标志，以通过/读取代理列表，以避免免费用户的 IP 禁令/节流

[**Download**](https://github.com/notdodo/pastego)