# WSVuls:网站漏洞扫描器检测问题

> 原文：<https://kalilinuxtutorials.com/wsvuls/>

[![](img/ff659953c3f45f210dfbef4e7a9c90ed.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhKXj7KZgC6gjj9v-FRUDkwyDlcG1x7fmoaE87WEpVvdwSvfw3WlMD4p9clsj2qHgTCeYCSVvubG873Wr_ZTiFZiZnUCKKrwjyJqzaW2-4hNcHxHn0z4yPEoRGQcrrKSBaJOGN9Xvi3q_zLWj35rtfC7_6m92pT4Z5JId7IMK11NmrZFWAopxJKTwZ0/s728/68747470733a2f2f692e6962622e636f2f6d4242796d43542f5753562e706e67%20(1).png)

WSVuls 是一个简单而强大的命令行工具，适用于 Linux、Windows 和 macOS。它是为开发人员/测试人员和那些想通过一个命令测试漏洞和分析网站的 It 工作者而设计的。它检测过时的软件版本，不安全的 HTTP 头，冗长和无用的请求

### 为什么是 WSVuls？

WSVuls 可以在搜索时提取以下数据:

##### 云耀斑

*   IP 地址；网络地址
*   港口
*   六角接头
*   协议版本

##### 统计数据

*   第一个字节
*   开始渲染
*   FCP
*   速度指数
*   人员登陆艇(Landing Craft Personnel)
*   CLS
*   技术性贸易壁垒（Technical Barriers to Trade 的缩写）
*   DC 时间
*   DC 请求
*   DC 字节
*   时间
*   要求
*   总字节数

##### Mapper

*   资源
*   请求开始
*   内容类型
*   DNS 查找
*   SSL 协商
*   错误/状态代码

### 码头工人

可以使用 docker 启动 WSVuls

##### 建立形象

**git 克隆 https://github . com/anouaachussaad/wsvuls
CD wsvuls
$ docker build-t wsvuls:latest。**

以交互模式运行 WSVuls 容器

**$ docker run-it-name wsvuls wsvuls:latest-u facebook.com**

## 使用

**扫描、检测并获取特定 url 的统计数据
示例:
从目标 url 获取统计数据:
$ wsvuls stats-u facebook.com
获取地图所有请求:
$ wsvuls stats-u facebook.com-mapper
从 cloudflare 防火墙检测正确的 ip 地址:
$ wsvuls cloud-d facebook.com
默认情况下使用-proxy 绕过限制速率。
可用命令:
stats 获取目标网站的统计数据。
云从 cloudflare 获得正确的数据。
标志:
-h，–wsvuls 的帮助帮助**

[**Download**](https://github.com/anouarbensaad/wsvuls)