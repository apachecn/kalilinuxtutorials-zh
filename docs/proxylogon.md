# 针对 microsoft exchange 的 proxylogon poco 漏洞利用

> 原文：<https://kalilinuxtutorials.com/proxylogon/>

[![ProxyLogon : PoC Exploit for Microsoft Exchange](img/aa10454cea29a12959d869421756509d.png "ProxyLogon : PoC Exploit for Microsoft Exchange")](https://1.bp.blogspot.com/-vbtWTVCQUVg/YF5XeDozI7I/AAAAAAAAIpU/5A-OeDEMQVs7cfK-Eg8gsLGRsoOgEEvXACLcBGAsYHQ/s728/ProxyLogon%25281%2529.png)

**ProxyLogon** 是一款针对微软 exchange 的 PoC 漏洞利用工具。

**如何使用？**

`**python proxylogon.py <name or IP of server> <user@fqdn>**`

**例子**

`**python proxylogon.py primary administrator@lab.local**`

*   如果成功，你将进入一个网络外壳。`**exit**`或`**quit**`退出 webshell(或 ctrl+c)

*   默认情况下，它会创建一个文件`**test.aspx**`。这是可以改变的。

[![](img/4699feee6bcf15fcc229a196d121b23a.png)](https://github.com/hausec/ProxyLogon/blob/main/Images/screenshot.PNG)[**Download**](https://github.com/hausec/ProxyLogon)