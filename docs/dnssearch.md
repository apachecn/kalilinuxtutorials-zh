# Dnssearch:一个子域枚举工具

> 原文：<https://kalilinuxtutorials.com/dnssearch/>

[![Dnssearch : A Subdomain Enumeration Tool](img/8ddd74a7e698b19b397c853470271e5e.png "Dnssearch : A Subdomain Enumeration Tool")](https://1.bp.blogspot.com/-sywyfFtx_lE/XlWSfGhuauI/AAAAAAAAFHU/nOT-1oi06lE2DU8-sw-wkCBtLlPCIlI1ACLcBGAsYHQ/s1600/Logo.png)

**Dnssearch** 是一个子域枚举工具。它接受一个输入域(`**-domain**`参数)和一个单词列表(`**-wordlist**`参数)，然后使用单词列表的行作为子域执行并发 DNS 请求，最终强制顶级域上的每个可用子域。

它支持自定义文件扩展名(`-ext`，默认为`php`)和其他可选参数:

的用法。/dnssearch:
-consumers int
并发消费者的数量。(默认为 8)
-开始枚举的域字符串
基域。
-用于枚举的单词列表字符串
单词列表文件。(默认为“names . txt”)
-A bool
查找 A 记录(默认为真)
-txt bool
查找 TXT 记录(默认为假)
-cname bool
显示 cname 结果(默认为假)

任务管理器按钮禁用器:禁用/重命名任务管理器按钮的简单方法

**编译**

**获取 github.com/evilsocket/dnssearch
CD dnssearch
go build-o dnssearch main . go**

*   **与 Docker** 一起编译使用

docker build -t dnssearch。
docker run-it–RM dnssearch

**演职员表**:西蒙妮·玛格丽特里

[**Download**](https://github.com/evilsocket/dnssearch)