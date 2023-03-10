# HABU——黑客和测试者网络渗透测试工具包

> 原文：<https://kalilinuxtutorials.com/habu-python-network/>

Habu 是一个 python 网络黑客工具包。这个工具的基本功能是帮助完成一些道德黑客和渗透测试的任务。它们中的大多数都与网络相关，对于那些想阅读源代码并从中学习的人来说，这些实现是易于理解的。

当前版本中实现的一些技术有:

*   ARP 中毒
*   ARP 嗅探
*   DHCP 发现
*   DHCP 饥饿
*   陆地攻击
*   SNMP 破解
*   子域识别
*   合成液泛
*   TCP 标志分析
*   TCP ISN 分析
*   TCP 端口扫描
*   社交网络上的用户名检查
*   虚拟主机识别
*   网络技术识别

**也可理解为[SQLMAP–数据库的枚举&来自易受攻击的 Web 表单的用户](https://kalilinuxtutorials.com/sqlmap2/)**

## **哈布安装**

**卡莉 Linux:**

您可以安装为 Kali Linux 创建的软件包。见[此处](https://github.com/portantier/habu/releases)

**Python 包(PyPi):**

Habu 在 PyPi 上，所以可以用 pip 直接安装:

```
$ pip3 install habu
```

### **habu.usercheck:检查社交网络上的用户名**

这个命令检查给定的用户名是否存在于各种社交网络和其他流行的网站上。

```
$ habu.usercheck portantier
{
    "aboutme": "https://about.me/portantier",
    "disqus": "https://disqus.com/by/portantier/",
    "github": "https://github.com/portantier/",
    "ifttt": "https://ifttt.com/p/portantier",
    "lastfm": "https://www.last.fm/user/portantier",
    "medium": "https://medium.com/@portantier",
    "pastebin": "https://pastebin.com/u/portantier",
    "pinterest": "https://in.pinterest.com/portantier/",
    "twitter": "https://twitter.com/portantier",
    "vimeo": "https://vimeo.com/portantier"
}
```

### **habu.jshell:使用 WebSockets 的 JavaScript Shell】**

这是 Habu 中最复杂的命令之一。当您启动它时，会绑定一个端口(默认值:3333)并侦听 HTTP 连接。如果接收到连接，则发送一个 JavaScript 代码，该代码打开一个 WebSocket，该 web socket 可用于向连接的浏览器发送命令。

您可以直接在 shell 中编写命令，或者使用插件，即简单的外部 JavaScript 文件。

使用 habu.jshell 你可以完全控制一个网页浏览器。

**注意:**模块的完整文档将与主文档分开，因为该模块有很多选项和命令。

```
$ habu.jshell 
>>> Listening on 192.168.0.10:3333\. Waiting for a victim connection.
>>> HTTP Request received from 192.168.0.15\. Sending hookjs
>>> Connection from 192.168.0.15
$ _sessions
0 * 192.168.0.15:33432 Mozilla/5.0 (X11; Linux x86_64; rv:57.0) Gecko/20100101 Firefox/57.0
$ _info
{
    "user-agent": "Mozilla/5.0 (X11; Linux x86_64; rv:57.0) Gecko/20100101 Firefox/57.0",
    "location": "http://192.168.0.10:3333/",
    "java-enabled": false,
    "platform": "Linux x86_64",
    "app-code-name": "Mozilla",
    "app-name": "Netscape",
    "app-version": "5.0 (X11)",
    "cookie-enabled": true,
    "language": "es-AR",
    "online": true
}
$ document.location
http://192.168.0.10:3333/
```

### **habu.vhosts:获取一个 IP 地址的 vhosts**

此命令使用 Bing 来查询托管在同一 IP 地址上的网站。

```
$ habu.vhosts www.telefonica.com
www.telefonica.com -> 212.170.36.79
[
    'www.telefonica.es',
    'universitas.telefonica.com',
    'www.telefonica.com',
]
```

### **habu.webid:识别网络技术**

该命令使用 Wappalyzer apps.json 数据库来识别 web 应用程序中使用的技术。

关于 [Wappalyzer](https://github.com/AliasIO/Wappalyzer/) 的更多信息。

**注意:**这个工具只发送一个请求。所以，是隐身而不可疑。

```
$ habu.webid https://woocomerce.com
{
    "Nginx": {
        "categories": [
            "Web Servers"
        ]
    },
    "PHP": {
        "categories": [
            "Programming Languages"
        ]
    },
    "WooCommerce": {
        "categories": [
            "Ecommerce"
        ],
        "version": "6.3.1"
    },
    "WordPress": {
        "categories": [
            "CMS",
            "Blogs"
        ]
    },
}
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/portantier/habu#installation)