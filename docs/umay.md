# Umay:物联网恶意软件相似性分析平台

> 原文：<https://kalilinuxtutorials.com/umay/>

[![](img/87255bef30d924001d2463c993ae0da5.png)](https://blogger.googleusercontent.com/img/a/AVvXsEijJDX23RCOH42WEHiDitXyVud9F3AZJ4w9I5XOUN1BS7_Zpt74AAGaf3xrfAy4mZ4NSaoRdJAamzR8KkZHdLCMvKLLL5I9dbtE20u1DqJpMjtRHHc6g7e1oxbEqEczHeCyF6X7Z5MbCbKOOHeOjRY5nqFZ8RvPGcKkl2PX5cJD1dohaaC0z3jxPJJK=s847)

**Umay** 项目提供基于共享代码的物联网恶意软件相似性分析。它有助于识别与被分析文件共享代码的其他恶意软件。这样，您就有机会了解恶意软件的家族。物联网生态系统中有各种不同架构的设备。在处理多架构问题时，基于静态的方法更有效。该项目使用了 IoTPOT 提供的 1000 个恶意软件二进制文件。radare2 提取每个二进制文件的基本块和函数，并将这些数据的哈希值存储在 SQL 数据库中。从该数据库中查询待分析样本的基本块和函数，并列出所有具有共享代码的恶意软件。

**当前特征**

*   基于共享代码的静态分析。
*   支持 ARM，MIPS，x86-64，i386，PowerPC，m68k，瑞萨 SH。
*   ？

**入门**

**先决条件**

*   Python3+
*   Radare2
    *   R2 管道

**安装**

**git 克隆 https://github . com/mucoze/umay
CD umay**

virtualenv venv

**源 venv/bin/activate**

**pip install-r requirements . txt**

**python manage . py make migrations**

**python manage.py 迁移**

**python manage.py 创建超级用户**

**python m**anage . py runserver

现在，您可以通过浏览器访问 project app。默认:`**127.0.0.1:8000**`

**创建自己的数据集文件**

`**python create_dataset.py samples/**`

给定所有样本所在的目录作为参数，它将为您生成`**dataset.db**`文件。

[**Download**](https://github.com/mucoze/Umay)