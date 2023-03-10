# r locals:Linux 启动分析器

> 原文：<https://kalilinuxtutorials.com/rclocals/>

[![](img/18b48dcb0567d02d16519a611884fa89.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgp6xhcXjJ2gCLWhFjIspSw3LrrtdxXa9Qf-CgcGRTaOHu8GMeYek65iza3QQQpLNNDok7Gxtf1li-OpO6nH2kgucgE1uIjO8V3poTYjfBk2KHYS7RDV8zkW_xCZ9l0IBONxa_HOXJHuKSB0gyKuwh0_6qZF5l4DofWPISY6thH9uFHrQ1JAoHT-3E5=s679)

r locals 的灵感来自于 Sysinternals 的“自动运行”, r locals 分析所有 Linux 启动的可能性来寻找后门，还执行进程完整性验证，扫描 DLL 注入的进程等等

## 涵盖的事物:

**列出系统信任的 GPG 密钥**

**已安装的软件包**

**文件完整性**

**进程完整性**(不属于任何已安装软件包的进程中加载的进程和库)

**名称被盗用的进程**(使用 prctl()在/bin/ps 中更改名称的进程)

**CRON 条目**

**RC 文件**

**X 系统启动文件**

**活动系统 d 单位**

**系统定时器单元**

**tmpfiles.d**

**流连忘返的用户**

**用法**

仅针对可疑信息:

# python 3 r locals . py–分类

有关详细信息:

#python3 rclocals.py –all

**截图**

![](img/70db9c11b293429b1555c99e7a8b9b22.png)![](img/c10a421645502f8673e9e6a5b277937b.png)![](img/0b7eaf90bd48962123099e41264329fe.png)![](img/5ffedda4c69c05065cadcf0d4fd03ff5.png)[**Download**](https://github.com/YJesus/RCLocals)