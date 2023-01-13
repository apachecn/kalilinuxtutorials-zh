# Metabigor:智能工具，但没有 API 密钥

> 原文：<https://kalilinuxtutorials.com/metabigor/>

[![Metabigor : Intelligence Tool But Without API Key](img/54c5bc3bc712f6933821a5c1564aaa86.png "Metabigor : Intelligence Tool But Without API Key")](https://1.bp.blogspot.com/-zOyAvKVOTFI/XlCa_BD6NNI/AAAAAAAAFEI/5IPDGyOS6H8OGOcGZ3w2MshYFJhkzLXagCLcBGAsYHQ/s1600/New%25281%2529.png)

Metabigor 是一个智能工具，它的目标是完成更多的任务，但没有任何 API 键。

**安装**

**去 github.com/j3ssie/metabigor 吧**

**主要特点**

*   发现目标的 IP 地址。
*   在 IP 目标上运行 masscan 和 nmap 的包装程序。
*   在一些搜索引擎上从命令行搜索。

**演示**

[![](img/02afacb31fa53a519ea6358dfe56746d.png)](https://asciinema.org/a/301745)

**也读-[Go Spider:用 Go](https://kalilinuxtutorials.com/gospider/) 写的快速网络蜘蛛 **

**示例命令**

**#公司/组织的发现 IP**
echo " company " | metabigor net–org-o/tmp/result . txt
**# ASN 的发现 IP**
echo " ASN 1111 " | metabigor net–ASN-o/tmp/result . txt
cat list _ of _ ASNs | metabigor net–ASN-o/tmp/result . txt
**#在子网的端口 443 上运行 mass can** metabigor scan–detail-o/tmp/result . txt
**# fofa 上的搜索结果**
echo ' title = " rabbit MQ Management " ' | metabigor search-x-v-o/tmp/result . txt

**免责声明**

该工具仅用于教育目的。你要对自己的行为负责。如果你在使用这个软件时搞砸了一些事情或者违反了任何法律，那是你的错，而且仅仅是你的错。

**鸣谢:**[flat icon](https://www.flaticon.com/free-icon/metabolism_1774457)by[freepik](https://www.flaticon.com/authors/freepik)

[**Download**](https://github.com/j3ssie/metabigor)