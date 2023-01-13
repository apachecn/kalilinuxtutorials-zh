# DNSTake:一个快速的工具，用于检查可能导致子域接管的缺失托管 DNS 区域

> 原文：<https://kalilinuxtutorials.com/dnstake/>

[![](img/0d736e6128d15971b354fba22a5a7a62.png)](https://1.bp.blogspot.com/-V9FT_Q-MPlU/YUSkknjqCwI/AAAAAAAAK4Q/Gqg2wK7SSHUQl8-5-94fdaXr3-tX1oJagCLcBGAsYHQ/s1508/4%2B%25281%2529.png)

**DNSTake** 当子域(subdomain.example.com)或域将其权威名称服务器设置为提供商(如 AWS Route 53、Akamai、Microsoft Azure 等)时，就会出现接管漏洞。)但托管区域已被移除或删除。因此，当请求 DNS 记录时，服务器会响应一个`**SERVFAIL**`错误。这使得攻击者能够在正在使用的服务上创建缺失的托管区域，从而控制该(子)域的所有 DNS 记录。

**安装**

**来自双星**

ez 方式！您可以从 releases 页面下载一个预构建的二进制文件，只需解压并运行即可！

**来源**

| **注意:** Go 1.16+编译器要安装&配置好！ |

非常快速和干净！

去安装 github.com/pwnesia/dnstake/cmd/dnstake@latest

#### —或者

从源代码手动构建可执行文件:

git 克隆 https://github.com/pwnesia/dnstake
│CD dnstake/cmd/dnstake
│去构建。
(sudo)mv dn stake/usr/local/bin

**用途**

▄▄▄▄ ▐ ▄。▄▄ ▄▄▄▄▄ ▄▄▄ ▄ •▄ ▄▄▄ .
██▪ ██ •█▌▐█▐█ ▀.•██ ▐█ ▀█ █▌▄▌▪▀▄.▀
▐█ ▐█▌▐█▐▐▌▄▀▀▀█▄▐█.▪▄█▀▀█ ▐▀▀▄ ▐▀▀▪▄
██.██ ██▐█▌▐█▄▪▐█▐█▌ ▐█ ▪▐▌▐█.█▌▐█▄▄▌
▀▀▀▀▀•▀▀█▪▀▀▀▀▀▀▀▀▀▀▀▀▀▀
(c)pwnesia.org—v 0 . 0 . 1
用法:
[stdin]| dn stake[options]
dn stake-t hostname[options]
选项:
-t，–target 定义单个目标主机/列表以检查
-c，–concurrent*设置并发级别(默认值:25)
-s，–静默抑制错误和/或清除输出
-h，–help 显示其帮助*)domain . TLD
dn stake-t hosts . txt
cat hosts . txt | dn stake
sub finder-silent-d domain . TLD | dn stake**

[**Download**](https://github.com/pwnesia/dnstake)