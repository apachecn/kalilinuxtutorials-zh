# SecLists:安全测试人员的安全评估指南

> 原文：<https://kalilinuxtutorials.com/seclists-security-testers/>

SecLists 是安全测试人员的伴侣。它是安全评估期间使用的多种类型列表的集合，集中在一个位置。列表类型包括用户名、密码、URL、敏感数据模式、模糊负载、web 外壳等等。

目标是使安全测试人员能够将这个存储库拖到一个新的测试箱上，并访问可能需要的每种类型的列表。

**又读: [DCOMrade:枚举易受攻击的 DCOM 应用的 Powershell 脚本](https://kalilinuxtutorials.com/dcomrade-powershell-dcom-applications/)**

**安装**

**Zip**

**wget-c https://github . com/danielmiessler/sec lists/archive/master . zip-O sec list . zip \
&&unzip sec list . zip \
&&RM-f sec list . zip**

**Git(小号)**

**git 克隆–深度 1 https://github.com/danielmiessler/SecLists.git**

**Git(完成)**

git 克隆 git @ github . com:danielmiessler/sec lists . git

**Kali Linux(工具页)**

**apt -y 安装安全列表**

跟我说话

下载此存储库可能会导致您的防病毒或防恶意软件发出误报警报，文件路径应列入白名单。Seclists 或 FuzzDB 中没有任何内容会损害您的计算机，但是不建议将这些文件存储在服务器或其他重要系统上，因为存在本地文件包含攻击的风险。

**鸣谢:** [**丹尼尔·米斯勒**](https://danielmiessler.com/) **，** [**杰森·哈德克斯**](http://www.securityaegis.com) **，**[**g 0 TMI 1k**](https://twitter.com/g0tmi1k)**。**

[**Download**](https://github.com/danielmiessler/SecLists)