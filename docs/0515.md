# Pocsuite3:开源远程漏洞测试框架

> 原文：<https://kalilinuxtutorials.com/pocsuite3-open-sourced-remote-vulnerability/>

Pocsuite3 是由 Knownsec 404 团队开发的开源远程漏洞测试框架。

它配备了一个强大的概念验证引擎，为最终渗透测试人员和安全研究人员提供了许多强大的功能。

**特性**

*   PoC 脚本可以以不同的方式在`attack`、`verify`、`shell`模式下运行
*   插件生态系统
*   从任何地方动态加载 PoC 脚本(本地文件、redis、数据库、Seebug …)
*   从任何地方加载多目标(CIDR，本地文件，redis，数据库，Zoomeye，Shodan …)
*   结果可以轻松导出
*   动态补丁和挂钩请求
*   命令行工具和 python 包导入都可以使用
*   IPV6 支持
*   全局 HTTP/HTTPS/SOCKS 代理支持
*   供 PoC 脚本使用的简单 spider API
*   与 [Seebug](https://www.seebug.org/) 集成(用于从 Seebug 网站加载 PoC)
*   与 [ZoomEye](https://www.zoomeye.org/) 整合(从 ZoomEye `Dork`加载目标)
*   与[庄丹](https://www.shodan.io/)整合(从庄丹`Dork`加载目标)
*   与 [Ceye](http://ceye.io/) 集成(用于验证盲 DNS 和 HTTP 请求)
*   用 ide 友好地调试 PoC 脚本
*   更多…

**也读作——[混沌:允许生成有效载荷的 PoC&控制远程操作系统](https://kalilinuxtutorials.com/chaos-poc/)**

**截图**

**pocsuite3 控制台模式**

**pocsuite3 外壳模式**

**pocsuit 3 从 Seebug 加载 PoC**

**pocsuite3 从 ZoomEye 加载多目标**

**pocsuite3 从 Shodan 加载多目标**

**要求**

Python 3.4+
在 Linux、Windows、Mac OSX、BSD 上运行

**安装**

干笑着道:

**$ pip 安装 pocsuite3**

或者单击此处下载最新的源 zip 包并解压缩

**$ wget https://github.com/knownsec/pocsuite3/archive/master.zip
$ unzip master . zip**

该软件的最新版本可从 http://pocsuite.org 获得

**免责声明**

未经双方事先同意，使用 pocsuite 攻击目标是非法的。pocsuite 仅用于安全测试目的。

[**Download**](https://github.com/knownsec/pocsuite3)