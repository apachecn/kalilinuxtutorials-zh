# Webdiscover:这个脚本的目的是自动执行 Web 枚举过程并搜索漏洞

> 原文：<https://kalilinuxtutorials.com/webdiscover/>

[![](img/1d1eeb60b69534561cdbe96ab3a06f3b.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhQOxApc6_Bmk--IMWR0yD6gfuuV-SF7-4VazzfB3uProCHhBjHjW6jyDdmJZU97NFUg-R3cST_uXEkHGaSvBdn-HE7sovH39FqM4uNuMLTtcIfHRceQFPld7MGP6Y43xXneoU6ewUhgraojuPTHGfBMGrV3ZEYSFx9f1u35txjDoPIHpz4TYkTXGBh=s728)

**Webdiscover** ，这个脚本的目的是自动执行 web 枚举过程，并搜索漏洞和攻击。

添加的工具(依赖项在脚本执行期间安装):

*   性爱列表
*   ffuf
*   名单
*   dnsrecon
*   子 finder
*   whatweb
*   戈斯皮德
*   核心
*   searchsploit
*   go-exploit b

它创建一个包含扫描输出的目录，如下例所示。

**用途**

先决条件

*   Docker 服务已安装

如果您想自己手工构建容器，git 克隆 repo:

**git 克隆 git @ github . com:v1 n1 v 131 R4/webiscover . git**

然后构建您的 docker 容器

docker build -t webdiscover。

构建容器后，运行以下命令:

**docker run–RM-it-v****/path/to/local/directory:/webdiscoverData web discover**

[**Download**](https://github.com/V1n1v131r4/webdiscover)