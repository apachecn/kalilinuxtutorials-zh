# DNS diag–DNS 诊断和性能测量工具

> 原文：<https://kalilinuxtutorials.com/dnsdiag/>

Dnsdiag 是一个 DNS 诊断和性能测量工具。有没有想过你的 ISP 是否劫持了你的 DNS 流量？有没有发现你的 DNS 响应有任何不当行为？曾经被重定向到错误的地址，怀疑你的域名系统有问题吗？在这里，我们有一套工具来执行对您的 DNS 请求和响应的基本审计，以确保您的 DNS 按照您的预期工作。

您可以使用`dnsping`测量任意给定 DNS 服务器对任意请求的响应时间。就像传统的 ping 实用程序一样，它为 DNS 请求提供了类似的功能。

您还可以跟踪您的 DNS 请求到达目的地的路径，以确保它没有被重定向或劫持。这可以通过使用`dnstraceroute`比较发送到同一域名系统服务器的不同域名系统查询，并观察路径之间是否有任何差异来实现。

`dnseval`评估多个 DNS 解析器，帮助您选择最适合您网络的 DNS 服务器。虽然强烈建议使用您自己的 DNS 解析器，并且不要相信任何第三方 DNS 服务器，但是如果您需要为您的网络选择最佳 DNS 转发器，`dnseval`允许您从性能(延迟)和可靠性(损失)的角度比较不同的 DNS 服务器。

**也可解读为**[**dex 2 jar——与 Android 协同工作的工具。dex & Java。类文件**](https://kalilinuxtutorials.com/dex2jar-android-java/)

## **Dnsdiag 要求**

*   Python3
*   dnspython
*   cymruwhois

## **安装**

有几种方法可以使用这个工具集。然而，总是推荐使用源代码。

## **来自源代码**

1.  您可以签出这个 git repo 及其子模块

```
git clone https://github.com/farrokhi/dnsdiag.git
cd dnsdiag
pip3 install -r requirements.txt
```

2.  您也可以使用 pip 来安装该软件包:

```
pip3 install dnsdiag
```

## **Dnsping**

dnsping 通过发送给定次数的任意 DNS 查询来 ping DNS 解析程序:

```
% ./dnsping.py -c 3 -t AAAA -s 8.8.8.8 dnsdiag.org
dnsping.py DNS: 8.8.8.8:53, hostname: dnsdiag.org, rdatatype: AAAA
4 bytes from 8.8.8.8: seq=0   time=123.509 ms
4 bytes from 8.8.8.8: seq=1   time=115.726 ms
4 bytes from 8.8.8.8: seq=2   time=117.351 ms

--- 8.8.8.8 dnsping statistics ---
3 requests transmitted, 3 responses received,   0% lost
min=115.726 ms, avg=118.862 ms, max=123.509 ms, stddev=4.105 ms
```

这个脚本计算最小、最大和平均响应时间以及抖动(stddev)

## **Dnstraceroute**

dnstraceroute 是一个 traceroute 实用程序，用于计算 DNS 请求到达目的地的路径。您可能希望将其与实际的网络跟踪路由进行比较，并确保您的 DNS 流量没有被路由到任何不需要的路径。

```
% ./dnstraceroute.py --expert -C -t A -s 8.8.4.4 facebook.com
dnstraceroute.py DNS: 8.8.4.4:53, hostname: facebook.com, rdatatype: A
1	192.168.0.1 (192.168.0.1) 1 ms
2	192.168.28.177 (192.168.28.177) 4 ms
3	192.168.0.1 (192.168.0.1) 693 ms
4	172.19.4.17 (172.19.4.17) 3 ms
5	google-public-dns-b.google.com (8.8.4.4) 8 ms

=== Expert Hints ===
 [*] public DNS server is next to a private IP address (possible hijacking)
```

使用`--expert`将指示 dnstraceroute 打印专家提示(例如可能的 DNS 流量劫持的警告)。

## **Dnseval**

dnseval 是一个批量 ping 实用程序，它可以向给定的 DNS 服务器列表发送任意 DNS 查询。该脚本用于同时比较多个 DNS 服务器的响应时间:

```
% ./dnseval.py -t AAAA -f public-servers.txt -c10 yahoo.com
server           avg(ms)     min(ms)     max(ms)     stddev(ms)  lost(%)  ttl     flags
------------------------------------------------------------------------------------------------------
8.8.8.8          270.791     215.599     307.498     40.630      %0       298     QR -- -- RD RA -- --
8.8.4.4          222.955     171.753     307.251     60.481      %10      291     QR -- -- RD RA -- --
ns.ripe.net      174.855     160.949     187.458     10.099      %0       289     QR -- -- RD RA -- --
4.2.2.1          172.798     163.892     189.918     7.823       %0       287     QR -- -- RD RA -- --
4.2.2.2          178.594     169.158     184.696     5.067       %0       285     QR -- -- RD RA -- --
4.2.2.3          153.574     138.509     173.439     12.015      %0       284     QR -- -- RD RA -- --
4.2.2.4          153.182     141.023     162.323     6.700       %0       282     QR -- -- RD RA -- --
4.2.2.5          154.840     141.557     163.889     7.195       %0       281     QR -- -- RD RA -- --
209.244.0.3      156.270     147.320     161.365     3.958       %0       279     QR -- -- RD RA -- --
209.244.0.4      159.329     151.283     163.726     3.958       %0       278     QR -- -- RD RA -- --
195.46.39.39     171.098     163.612     181.147     5.067       %0       276     QR -- -- RD RA -- --
195.46.39.40     175.335     160.920     185.618     8.726       %0       274     QR -- -- RD RA -- --
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/farrokhi/dnsdiag) **信用:巴巴克·法鲁克希**