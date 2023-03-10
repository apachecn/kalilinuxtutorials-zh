# pastego–使用 go & recession 语法抓取/解析 pastebin

> 原文：<https://kalilinuxtutorials.com/pastego-scrape-parse-pastebin/>

Pastego 使用 go 和语法表达式(PEG)抓取/解析 Pastebin。

## **Pastego 安装**

T2`**$ go get -u github.com/edoz90/pastego**`

**也可阅读 [Hackertarget:工具和网络情报帮助组织进行攻击面发现](https://kalilinuxtutorials.com/hackertarget-attack-surface-discovery/)**

## **用途**

搜索关键字区分大小写

`**pastego -s "password,keygen,PASSWORD"**`

您可以使用布尔运算符来减少误报

`**pastego -s "quake && ~earthquake, password && ~(php || sudo || Linux || '<body>')"**`

该命令将搜索具有`quake`但不具有`earthquake`字的库，以及具有`password`但不具有`php`、`sudo`、`Linux`、`<body>`字的库。

```
usage: pastego [<flags>]

Flags:
      --help              Show context-sensitive help (also try --help-long and --help-man).
  -s, --search="pass"     Strings to search, i.e: "password,ssh"
  -o, --output="results"  Folder to save the bins
  -i, --insensitive       Search for case-insensitive strings
```

支持的表达式/运算符:

```
&&` - and

`||` - or

`~` - not

`'string with space'`

`(myexpression && 'with operators')
```

### **按键组合**

`q`、`ctrl+c`:退出`pastego`

`k`、`↑`:显示上一个框

`j`、`↓`:显示下一个箱子

`n`:向前跳 15 格

`p`:向后跳 15 格

`N`:移动到下一组结果(按字母顺序)

`P`:移至上一个结果块(按字母顺序)

`d`:从文件系统中删除文件

`HOME`:转到顶部

## **要求**

#### [goquery](https://github.com/PuerkitoBio/goquery)

**`go get -u "github.com/PuerkitoBio/goquery"`**

#### [中枢人物](https://github.com/alecthomas/kingpin)

**`go get -u "gopkg.in/alecthomas/kingpin.v2"`**

#### [gocui](https://github.com/jroimartin/gocui)

`**go get -u "github.com/jroimartin/gocui"**`

使用[鸽子](https://github.com/mna/pigeon)从 PEG 创建代码:

`**go get -u github.com/mna/pigeon**` 

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/edoz90/pastego) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***