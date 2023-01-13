# log4j-Scan:一个全自动、精确和广泛的扫描器，用于查找易受攻击的 log4j 主机

> 原文：<https://kalilinuxtutorials.com/log4j-scan/>

[![](img/a282e2781720fac68e17f0a5ed4a5060.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiiQNl-AlRyYgcJJHOTvNwpj_rO55lk-zWzICr2oZM_i9fDpmYUk4DfVWkPIXR2j_cgL4U-NJ9VGQWIS0w4taQBOPUN2w8NZ0RA6LVbQz0IHEOLO-54zB_x9YHaBcs1qdA2BleK-LluPpEHUUxEKVc1eUwytyHHapSNrqP4kv7RyJNYiNLwxzEURYOe=s672)

**log4j-scan** 是一款全自动、精确、全面的扫描器，用于查找易受攻击的 log4j 主机。

**特性**

*   支持 URL 列表。
*   模糊超过 60 个 HTTP 请求头(不像以前看到的工具那样只有 3-4 个头)。
*   HTTP POST 数据参数的模糊化。
*   JSON 数据参数的模糊化。
*   支持漏洞发现和验证的 DNS 回调。
*   晶片旁路有效载荷。

**公告**

Log4J v2.15.0 上有一个补丁旁路，允许完全 RCE。FullHunt 增加了对 log4j-scan 的社区支持，以可靠地检测 CVE-2021-45046。如果您在发现和扫描大规模基础架构或应对 Log4J 威胁方面遇到困难，请联系(team@fullhunt.io)。

**描述**

自从 Log4J RCE (CVE-2021-44228)发布以来，我们一直在研究它，并与我们的客户一起努力防止这一漏洞。我们正在开源一个开放的检测和扫描工具，用于发现和模糊 Log4J RCE CVE-2021-44228 漏洞。安全团队应使用它来扫描 Log4J RCE 的基础架构，并测试可能导致代码在组织环境中执行的 WAF 旁路。

它支持开箱即用的 DNS OOB 回调，没有必要设置一个 DNS 回调服务器。

**用途**

**$ python 3 Log4j-scan . py-h
【】CVE-2021-44228——阿帕奇 Log4j RCE 扫描仪
【】full hunt . io 提供的扫描仪——下一代攻击面管理平台。
[]用 FullHunt.io 保护你的外部攻击面
用法:log4j-scan . py[-h][-u URL][-p PROXY][-l used list][–REQUEST-TYPE REQUEST _ TYPE][–HEADERS-FILE HEADERS _ FILE][–run-all-tests][–exclude-user-agent-fuzzing]
[–WAIT-TIME WAF-BYPASS][–CUSTOM-WAF-BYPASS-PAYLOAD CUSTOM _ WAF _ BYPASS _ PAYLOAD][–test-CVE
-p PROXY，–PROXY PROXY
通过代理发送请求
-l USEDLIST，–list used list
检查 URL 列表。
–请求类型 REQUEST_TYPE
请求类型:(get，post)–【默认:get】。
–HEADERS-FILE HEADERS _ FILE
HEADERS fuzzing list-【默认:headers.txt】。
–Run-all-tests 对每个 URL 运行所有可用的测试。
–排除用户代理模糊化
从模糊化中排除用户代理报头–用于绕过对用户代理的弱检查。
–WAIT-TIME WAIT _ TIME
处理完所有 URL 后的等待时间(秒)–【默认值:5】。
–使用晶片旁路有效载荷的晶片旁路扩展扫描。
–CUSTOM-WAF-BYPASS-PAYLOAD CUSTOM _ WAF _ BYPASS _ PAYLOAD
使用自定义 WAF bypass 有效载荷进行测试。
–测试-CVE-2021-45046
使用 CVE-2021-45046 的有效载荷(探测有效载荷)进行测试。
–DNS-CALLBACK-PROVIDER DNS _ CALLBACK _ PROVIDER
DNS 回调提供者(选项:dnslog.cn，interact.sh)–【默认:interact . sh】。
–自定义-dns-回调-主机自定义 _ DNS _ 回调 _ 主机
自定义 DNS 回调主机。
–禁用 http 重定向
禁用 HTTP 重定向。注意:HTTP 重定向很有用，因为它允许有效负载有更高的机会到达易受攻击的系统**。

**扫描单个网址**

**$ python 3 log4j-scan . py-u https://log4j . lab . sec bot . local**

**使用所有请求方法扫描单个 URL:GET、POST (url 编码的形式)、POST (JSON 主体)**

```
$ python3 log4j-scan.py -u https://log4j.lab.secbot.local --run-all-tests

```

**发现 WAF 绕过环境。**

**$ python 3 log4j-scan . py-u https://log4j . lab . sec bot . local–waf-bypass**

**扫描网址列表**

**$ python 3 log4j-scan . py-l URL . txt**

**安装**

**$ pip 3 install-r requirements . txt**

**Docker 支持**

**吉特克隆 https://github.com/fullhunt/log4j-scan.git
CD log4j-scan
sudo docker build-t log4j-scan。
sudo docker run-it–RM log4j-scan
与当前目录中的 URL 列表“URLs . txt”
docker run-it–RM-v $ PWD:/data log4j-scan-l/data/URLs . txt**

[**Download**](https://github.com/fullhunt/log4j-scan)