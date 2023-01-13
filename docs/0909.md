# Penta:自动化 pentest 的开源一体化 CLI 工具

> 原文：<https://kalilinuxtutorials.com/penta-open-source-cli-automate-pentesting/>

[![Penta : Open Source All-In-One CLI Tool To Automate Pentesting](img/dd6d932c2aaa35cbd8d0b4082ae3072d.png "Penta : Open Source All-In-One CLI Tool To Automate Pentesting")](https://1.bp.blogspot.com/-eEK2fKAI09A/XZ2txE3XREI/AAAAAAAAC3Q/_hPQHzih5xEgu80JVfb_R2Xxtl3nzzYVgCLcBGAsYHQ/s1600/logo_penta%25281%2529.png)

Penta 是使用 Python3 的 Pentest 自动化工具。它提供了 metasploit 和 nexpose 等高级功能来提取特定服务器上的漏洞信息。

![](img/ec77095b6e2042c4b9f8a213a2bf0190.png)

**安装**

**安装要求**

penta 需要以下软件包。

*   Python3.7
*   pipenv

解决 python 包的依赖性。

**$ pipenv 安装**

如果你不喜欢 pipenv…

**$ pip install-r requirements . txt**

**也读作-[ThreadBoat:程序使用线程执行劫持将本机外壳代码注入标准 Win32 应用程序](https://kalilinuxtutorials.com/threadboat-thread-execution-hijacking/)**

**用法**

**$ pipenv 运行开始**

如果你不喜欢 pipenv…

**$ python penta/penta.py**

**用法:列表选项**

**$ pipenv run start -h**
用法:Penta . py[-h][-TARGET TARGET][-PORTS PORTS][-PROXY PROXY]

**Penta 是 Pentest 自动化工具** 
**可选参数:** -h，–help 显示此帮助消息并退出
-target TARGET 指定目标 IP /域
-ports 请指定目标端口，用逗号分隔。
默认值:21，22，25，80，110，443，8080
-代理代理代理[IP:PORT]

**用法:主菜单**

===菜单列表= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
0–退出
1–端口扫描默认值:21，22，25，80，110，443，8080
2–Nmap&vuln 扫描
3–检查 HTTP 选项方法
4–抓取 DNS 服务器信息
5–shod an 主机搜索
6–FTP 匿名连接
SSH 连接

*   端口扫描
    检查目标端口。支持日志输出。
*   Nmap
    使用 Nmap 通过其他方式检查端口
*   检查 HTTP 选项方法
    以检查目标的方法(如 GET、POST)。
*   抓取 DNS 服务器信息
    以显示关于 DNS 服务器的信息。
*   Shodan 主机搜索从 Shodan 收集主机服务信息。请求 [Shodan API 键](https://developer.shodan.io/)启用该功能。
*   FTP 与 anonymous 连接，检查它是否在端口 21 激活了匿名访问。FTP 用户可以使用纯文本登录协议(通常是用户名和密码格式)验证自己，但是如果服务器配置允许，他们可以匿名连接。如果管理员允许匿名登录的 FTP 连接，任何人都可以登录到服务器。
*   SSH connect with Brute Force 检查 SSH 连接以使用暴力扫描。字典数据在`data/dict`里。

[Download](https://github.com/takuzoo3868/penta)