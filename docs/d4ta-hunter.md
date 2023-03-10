# D4TA-HUNTER:带有 Kali Linux 的 GUI OSINT 框架

> 原文：<https://kalilinuxtutorials.com/d4ta-hunter/>

[![](img/1c0488690e1bc587f9f989ca33ad9efa.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjsRdDGqOtNNaloryZEaJLpmsPlZOGDt6Pmm48DHHG5uv4KS7bp0iDPthVfWP9E9E-0Obe1VDVaQtAdd6RPdiG5u4Kt3tYX0WeXaQovcF-CqmW9595njq6vFDqS0_svjY9LnrSdhW6DegiCSq_hr26cmfuCjykdDC_0zjxXozT2Nr2_TZ2pBhqGr8QV/s728/D4TA-HUNTER1.png)

**D4TA-HUNTER** 是一款工具，用于自动收集将要接受道德黑客审计的公司员工的信息。

此外，在这个工具中，我们可以通过插入公司的域、员工的电子邮件、子域和服务器的 IP 来在“搜索公司”部分中进行查找。

![](img/719c556194c59efb66af3cd8ef81a8fe.png)

## 获取 API 密钥

在[https://rapidapi.com/rohan-patra/api/breachdirectory](https://rapidapi.com/rohan-patra/api/breachdirectory)上注册

## 安装

git 克隆 https://github.com/micro-joan/D4TA-HUNTER
CD D4TA-HUNTER/
chmod+x run . sh
。/run.sh

在执行应用程序启动程序后，您需要安装所有组件，启动程序将逐个检查，如果没有安装任何组件，它将向您显示安装组件时必须输入的语句:

![](img/e3059735f1631155d4f044836ff3dc79.png)

## 使用

首先，你必须有一个来自 BreachDirectory.org 的免费或付费的 API 密匙，如果你没有的话，搜索一下 D4TA-HUNTER 会为你提供一个如何获得的指南。

一旦你有了 API 密匙，你将能够搜索电子邮件，优势是向你显示所有密码散列的列表，供你复制并粘贴到 D4TA-HUNTER 提供的在线资源之一，以 100 %免费破解密码。

![](img/ca864baf19e21d09de84be69499bdf53.png)

您还可以插入一个公司的域名，D4TA-HUNTER 将搜索员工电子邮件、可能感兴趣的子域以及找到的机器的 IP 地址:

![](img/a32237282ee8571857a2745a299d8a82.png)

## API 和工具

| 服务 | 功能 | 状态 |
| --- | --- | --- |
| BreachDirectory.org | 电子邮件、电话或尼克泄密 | ✅ 🔑 (free plan) |
| 主持人 | 公司的域名和电子邮件 | ✅ Free |
| [碱化](https://github.com/brainfucksec/kalitorify) | Tor 搜索 | ✅ Free |

[Click Here To Download](https://github.com/micro-joan/D4TA-HUNTER)