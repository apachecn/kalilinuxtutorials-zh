# HashCheck:帮助搜索泄漏密码的工具

> 原文：<https://kalilinuxtutorials.com/hashcheck/>

[![HashCheck : Tool To Assist In The Search For Leaked Passwords](img/b7753918da040bcef2d05f4f98f9846a.png "HashCheck : Tool To Assist In The Search For Leaked Passwords")](https://1.bp.blogspot.com/-H6PXfKUjWYU/YNrxYgMwv3I/AAAAAAAAJuI/-AIdrJ7qRWQXcQoOmSIdknrQ-j2y5fYNgCLcBGAsYHQ/s728/HashCheck.png)

HashCheck 是一个项目，旨在帮助搜索泄露的密码，同时使用 k-anonymity 方法保持高度隐私。

为了实现这一点，使用不同服务的 API，只发送我们想要检查的密码的一部分散列，例如，前 5 个字符。

**先决条件**

该项目需要一些库才能工作，要安装它，请使用下面的命令:

**pip 安装要求**

记住 Python 3 是必需的。

**用途**

**passme . py[FUNC][元素]-引擎[引擎] -api_key [API_KEY]**

FUNC:你想要检查的元素的种类，它可以是-h/–hash 或者-p/–password
或者-f/–file 或者-l/–list 或者–help。
元素:“哈希”、“密码”或包含由新行分隔的
哈希或密码列表的文件名。
引擎:你想要使用的 leaks 引擎，默认使用 HIBP(我被 PWN 过了)。
API_KEY:某些引擎的某些功能所必需的 API_KEY。

**功能**

**PASSME_HASH**

主项目函数接收散列密码、要使用的引擎和 API 密钥。

根据接收到的引擎，API 密钥和散列密码都将被发送到一个或另一个函数。

如果您想添加自己的引擎或尚未实现的引擎，只需在这里再添加一个选项。

**passme_hash(hashed_password，engine="HIBP "，API _ key = " 0 ")**

**PASSME_PASSWORD**

这个函数使用 SHA-1 对收到的密码进行哈希处理，并将哈希发送给 passme_hash()函数。

**passme_password(password，engine="HIBP "，API _ key = " 0 ")**

**通行证 _ 文件**

这个函数逐个读取接收到的文件的行来检查每个密码，给出关于接收到的密码的信息以及它是否已经被过滤。

**passme_file(文件名，引擎="HIBP "，API _ key = " 0 ")**

**通行证列表**

这个函数逐个读取接收到的文件的行来检查每个散列，给出关于接收到的散列的信息以及它是否已经被过滤。

**passme_list(文件名，引擎="HIBP "，API _ key = " 0 ")**

**通行证列表**

处理 HIBP(我被 pwned 了吗)API 的函数发送散列的前五个字符，然后将其与完整的散列进行比较，以查看密码/散列是否已被泄露。

**engine_HIBP(hashed_password，engine，api_key)**

**测试**

该项目有一系列的测试来检查其所有功能的正确操作，为此目的，使用了“pytest”库。要运行测试，请使用以下命令安装 pytest:

**pip 安装 pytest**

安装完成后，只需运行“pytest”命令就可以自动运行测试，遇到的任何错误都将由终端返回。

实验室测试的结果如下:

| Python 版本 | 函数哈希 | 功能列表 | 功能密码 | 随机散列 | 随机密码 | 评论 |
| --- | --- | --- | --- | --- | --- | --- |
| Three point nine | 981 号房 | 981 号房 | 981 号房 | 981 号房 | 981 号房 |  |
| Three point eight | 981 号房 | 981 号房 | 981 号房 | 981 号房 | 981 号房 |  |
| Three point seven | 981 号房 | 981 号房 | 981 号房 | 981 号房 | 981 号房 |  |
| Three point six | 981 号房 | 981 号房 | 981 号房 | 981 号房 | 981 号房 |  |
| Three point five | 981 号房 | 981 号房 | 981 号房 | -好的 | -好的 | Random.choice 在 Python 3.5 中不可用//已弃用的 Python 版本 |

[**Download**](https://github.com/Telefonica/HashCheck)