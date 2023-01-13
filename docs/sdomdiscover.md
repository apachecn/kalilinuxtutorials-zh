# SDomDiscover:一个易于使用的 Python 工具，用于执行 DNS 侦察

> 原文：<https://kalilinuxtutorials.com/sdomdiscover/>

[![](img/c33564afd722225645cbbe6caf1b1cbb.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjNHXBkj9bh0xXND-6FOXUkfZmmgHMYxdPh3tHW3yy1CCsgxIHtjbCsrwF-jLdh5AGH0YXH5r3gwyW_5JIjwfYl1Au-vnXnX4qScM5sSp09SndRewfVzWNDAQG6Z8en0airOZHfH9FdrZmOZIegjedAyVfcybRdjXd7bz464UaAWhb9_5fwBIgoTVwP/s728/download%20(1).png)

**sdom discover**

这个工具的目的是在侦察过程中帮助臭虫出没者和探险者

如果你想了解更多关于这个工具的信息，你可以在我的博客中阅读我自己的帖子(用西班牙语写的)

## 安装

它可以在任何使用 python3 的系统中使用

您可以使用 pip 轻松安装 AORT:

**pip3 安装 aort**

如果您想从源代码安装它:

**git 克隆 https://github.com/D3Ext/AORT
CD AORT
pip 3 install-r requirements . txt**

一行程序

**git 克隆 https://github.com/D3Ext/AORT&CD AORT&pip 3 install-r requirements . txt&python 3 AORT . py**

## 使用

常见用法

如果安装了 pip3:

**aort**

要查看帮助面板和其他参数

**python3 AORT.py -h**

该工具的主要用途是转储 SSL 证书中的有效域

**python 3 aort . py-d example.com**

用于执行所有的查询和识别

**python 3 aort . py-d domain.com——全部**

## 特征

*   使用被动技术枚举子域

*   大量额外的查询来枚举 DNS

*   域区域转移攻击

*   晶片类型检测

*   子域接管检查器

*   回溯机器支持枚举端点

*   电子邮件收集

## 第三部分

该工具使用不同的服务以不同的方式获取子域

晶片检测器被修改并适应于

所有 DNS 查询都是 100%用 python 编写的

使用带有个人令牌的 Proxycrawl API 收集电子邮件(您可以注册一个免费帐户，使用 100 次)

[**Download**](https://github.com/D3Ext/AORT)