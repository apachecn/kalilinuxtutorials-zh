# nax si:NGINX 的 WAF

> 原文：<https://kalilinuxtutorials.com/naxsi-waf-nginx/>

NAXSI 是 NGINX 开源、高性能、低规则维护的 WAF。NAXSI 表示 Nginx 反 XSS 和 SQL 注入。

从技术上讲，它是一个第三方 nginx 模块，可以作为一个包用于许多类 UNIX 平台。

默认情况下，该模块读取包含网站漏洞中 99%已知模式的简单(可读)规则的一个小子集。例如，

非常简单，这些模式可能匹配合法的查询，Naxsi 的管理员有责任添加将合法行为列入白名单的特定规则。

管理员既可以通过分析 nginx 的错误日志来手动添加白名单，也可以(建议)从强化自动学习阶段开始项目，该阶段将自动生成关于网站行为的白名单规则。

简而言之，Naxsi 的行为就像一个默认丢弃的防火墙，唯一的任务是添加目标网站正常工作所需的接受规则。

**也读作——[PYWhatCMS——非官方的 WhatCMS API 包](https://kalilinuxtutorials.com/pywhatcms-unofficial-api-package/)**

**为什么不一样？**

与大多数 Web 应用程序防火墙相反，Naxsi 不依赖于防病毒软件之类的签名库，因此不能被“未知”攻击模式绕过。Naxsi 是免费软件(如在 freedom 中)和免费使用(如在免费啤酒中)。

它靠什么运行？

Naxsi 应该兼容任何 nginx 版本。

它依赖于 **libpcre** 的 regexp 支持，据报道在 **NetBSD、FreeBSD、OpenBSD、Debian、Ubuntu 和 CentOS:** 上运行良好

[Download](https://github.com/nbs-system/naxsi)