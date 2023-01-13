# Spring4Shell-Scan:用于查找 Spring4Shell 的全自动、可靠且精确的扫描器

> 原文：<https://kalilinuxtutorials.com/spring4shell/>

[![](img/75a2549b4a7311195aeaaf502599ffec.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs2MuDECxtBggRi87z8yWxGxw6RVOWXtibmDK83ZqANLBpvDoVyzpl7rN-2_nyDCJntIkWn8hOjPfmWf8qlQaQRsgJebOVJmRAwmMXodytNbOfXEaFbiICBveY53tuEz6h6jLK9qWO717BNAmo44P5saQazgXaB2SX9KjryKilQVnbNISb1NRMr1ik/s728/1%20(1).png)

**Spring4Shell-Scan** 是一款全自动、可靠、准确的扫描器，用于查找 Spring4Shell 和 Spring Cloud RCE 漏洞。

# 特征

*   支持 URL 列表。
*   Fuzzing for 多个新的 Spring4Shell 有效载荷(以前看到的工具只使用 1-2 个变体)。
*   HTTP GET 和 POST 方法的模糊化。
*   发现漏洞后自动验证。
*   随机化和非侵入式有效载荷。
*   晶片旁路有效载荷。

# 描述

自发布以来，FullHunt 一直在研究 Spring4Shell RCE 这一关键漏洞。我们与客户合作，扫描他们环境中的 Spring4Shell 和 Spring Cloud RCE 漏洞。

我们正在开源一个开放检测扫描工具，用于发现 Spring4Shell (CVE-2022-22965)和 Spring Cloud RCE (CVE-2022-22963)漏洞。安全团队应使用它来扫描他们的基础架构，以及测试 WAF 旁路，从而成功利用组织的环境。

如果您的组织需要帮助，请直接联系(fullhunt.io 的团队),进行全面的攻击面发现和 Spring4Shell 漏洞扫描。

## 使用

**$。/spring 4 shell-scan . py-h
[]CVE-2022-22965–spring 4 shell RCE 扫描仪
[]由 FullHunt.io 提供的扫描仪–下一代攻击面管理平台。
[]使用 FullHunt.io 保护您的外部攻击面
用法:spring 4 shell-scan . py[-h][-u URL][-p PROXY][-l used list][–PAYLOADS-FILE PAYLOADS _ FILE][–waf-bypass][–REQUEST-TYPE REQUEST _ TYPE][–test-CVE-2022-22963]
可选参数:
-h，–help 显示此帮助消息并退出
-u URL，–URL URL 检查单个 URL。
-p PROXY，–PROXY PROXY
通过代理发送请求
-l USEDLIST，–list used list
检查 URL 列表。
–有效载荷-文件有效载荷 _ 文件
有效载荷文件-【默认值:payloads.txt】。
–使用晶片旁路有效载荷的晶片旁路扩展扫描。
–请求类型 REQUEST_TYPE
请求类型:(get，post，all)–【默认:all】。
–测试-CVE-2022-22963
测试 CVE-2022-22963(春云 RCE)。**

## 扫描单个 URL

**$ python 3 spring 4 shell-scan . py-u https://spring 4 shell . lab . sec bot . local**

## 发现 WAF 绕过环境

**$ python 3 spring 4 shell-scan . py-u https://spring 4 shell . lab . sec bot . local–waf-bypass**

## 扫描 URL 列表

**$ python 3 spring 4 shell-scan . py-l URLs . txt**

## **包括对 RCE 春云的检查(CVE-2022-22963)**

**$ python 3 spring 4 shell-scan . py-l URLs . txt–test-CVE-2022-22963**

## 装置

**$ pip 3 install-r requirements . txt**

## 码头支持

git 克隆 https://github.com/fullhunt/spring4shell-scan.git
CD spring 4 shell-scan
sudo docker build-t spring 4 shell-scan。
sudo docker run-it–RM spring 4 shell-scan
当前目录下的 URL 列表“URLs . txt】docker run-it–RM-v $ PWD:/data spring 4 shell-scan-l/data/URLs . txt

[**Download**](https://github.com/fullhunt/spring4shell-scan)