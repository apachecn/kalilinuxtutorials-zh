# 令牌反向器:破解安全令牌的单词列表生成器

> 原文：<https://kalilinuxtutorials.com/token-reverser/>

[![Token Reverser : Word List Generator To Crack Security Tokens](img/cfce9ee3d77829597db7e12b4e1163e7.png "Token Reverser : Word List Generator To Crack Security Tokens")](https://1.bp.blogspot.com/-MjzpUYDsx-c/XnJlPnN30dI/AAAAAAAAFj0/TDgY2XdZdRQiIbWdHchk4BeUhcQTY5VSgCLcBGAsYHQ/s1600/token-reverser%25281%2529.png)

**令牌反向器**是一个破解安全令牌的单词列表生成器。

**示例用例**

*   您正在测试重置密码功能
*   重置密码令牌已发送到您的电子邮箱(例如 582431 d4c 7b 57 cb4a 3570041 ffeb 7 e 10)
*   您认为，它是您在注册过程中提供的数据的 md5 散列
*   您记得在注册时，您输入了以下数据:
    *   名字:福
    *   姓氏:酒吧
    *   电子邮件:foo.bar@example.com
    *   出生日期:1985 年 5 月 23 日
    *   电话:202-555-0185
    *   地址:森林大道 3634 号
*   此外，您还可以访问以下额外数据:
    *   应用程序用户 ID: 74824
    *   重置密码 HTTP 请求的日期(“日期”响应标头):2020 年 3 月 10 日，星期二，17:12:59 GMT
*   您使用令牌反向器从已知数据生成单词列表:

**。/token-reverser . py–date " 2020 年 3 月 10 日星期二 17:12:59 GMT " foo.bar@example.com 富吧 1985-05-23 202-555-0185 "森林大道 3634 号" 74824 >字样**

*   您使用 hashcat 来破解重置密码令牌:

hashcat64.exe-m 0 582431d 4c 7b 57 cb4a 3570041 ffeb 7 e 10 话
hashcat (v5.1.0)首发……
[…]
582431d 4c 7b 57 cb4a 3570041 ffeb 7 e 10:74824！福！吧！foo.bar@example.com！1583860379
会话……:哈希卡特
地位……..:破解的
哈希。类型……..:MD5
哈希。target……:582431 d4c 7b 57 cb4a 3570041 ffeb 7 e 10
[…]

*   现在您已经知道重置密码令牌是按如下方式生成的:

**md5(用户 ID！名字！姓！邮件！当前时间戳)**

**也可阅读-[pick L3:Windows 活跃用户凭证钓鱼工具](https://kalilinuxtutorials.com/pickl3/)**

**用途**

**用法:**token-reverser . py[-h][-d DATE][-o TIMESTAMP _ OFFSET][-s SEPARATORS][-s]data[data…]

**字表生成器破解安全令牌 v1.1**

**位置参数:**
data 数据块

**可选参数:**
【h】，–help 显示此帮助消息并退出
-d DATE，–DATE 日期时间戳 –TIMESTAMP-OFFSET TIMESTAMP _ OFFSET
应该使用多少个先前的(从日期到时间戳)时间戳
作为附加数据块，默认:1 个
-s 分隔符，–分隔符分隔符要检查的数据块分隔符，默认:~ `！ @#$%^&*()_+-= { } |[]\:"；< >？,./ \t

[**Download**](https://github.com/dariusztytko/token-reverser)