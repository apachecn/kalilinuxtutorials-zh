# DNSDmpstr:DnsDumpster & hacker target 的非官方 API 和客户端

> 原文：<https://kalilinuxtutorials.com/dnsdmpstr-dnsdumpster-hackertarget/>

DNSDmpstr 是 DNS [Dumpster](https://dnsdumpster.com/) 和 HackerTarget.com[IP 工具的非官方 API 和客户端。](https://hackertarget.com/ip-tools/)

DNS dumpster 是一个免费的域研究工具，可以发现与某个域相关的主机。从攻击者的角度寻找可见的主机是安全评估过程的重要部分。

**也可阅读-[Metaforge:一个通过标签过滤的 OSINT 元数据分析工具&创建报告](https://kalilinuxtutorials.com/metaforge/)**

**安装**

**git 克隆 https://github.com/zeropwn/dnsdmpstr
CD dnsdmpstr
pip 3 install-r requirements . txt
chmod+x ddump . py**

**用途**

作为命令行实用工具

**target = " hacker one . com "
python 3 ddump . py-u＄target–all**

**扩展使用**

**用法:ddump . py[-h][-U][-A][-r][-d][-DD][–links][–headers][–all]
可选参数:
-h，–help 显示此帮助消息并退出
-u 目标域
-a 主机搜索(dns A 记录查找)
-r 反向 DNS 查找(接受 IP、IP 范围或域名)
-d dns 查找
-dd 经典 DNS 转储格式【t**

**作为图书馆**

**导入 dnsdmpstr
target = " hacker one . com "
dnsdump = dnsdmpstr()
print(JSON . dumps(dnsdump . dump(target)，indent = 1))
print(dnsdump . hostsearch(target))
print(dnsdump . reversedns(target))
print(dnsdump . dnslookup(target))
print(dnsdump . page links(target))
print(dnsdump . httpheaded)。**

[**Download**](https://github.com/zeropwn/dnsdmpstr)