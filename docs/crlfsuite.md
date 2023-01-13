# 快速 CRLF 注射扫描工具

> 原文：<https://kalilinuxtutorials.com/crlfsuite/>

[![](img/29090e7e069b2c34ca4ecfb8b711e25c.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQrzD5LbUAXLplzJGWnlLuGbfqJjzuagdJJpAYNH9YZBd1HSvJHHHfYfe62xVnaDgjazR8zMUPKV9eR1fk9VZVtqutQU7Pjdjvl0wdJy3MYDPQ8guhdfzQ2WR-ojgDIEDlY6S4TNJLvswHNFzVNLDA5FNRe3okRsB8GkOFYI0RQgvEatrX2AqOi8dh/s728/CRLFsuite_logo2.0%20(2).png)

**CRLFsuite** 是一款专门为扫描`**CRLF injection**`而设计的快速工具。

## 装置

**git 克隆 https://github . com/necore/CRL fsuite . git
$ CD CRL fsuite
$ sudo python 3 setup . py install
$ CRL fsuite-h**

## 特征

单一 URL 扫描

✔️多重网址扫描

✔️晶片检测

通过 CRLF 注射的✔️ XSS

✔️ Stdin supported

支持✔️获取和发布方法

竞争

✔️强大有效载荷(晶片规避有效载荷也包括在内)

✔️快速高效扫描，假阳性可忽略不计

## 论据

| 争吵 | 描述 |
| --- | --- |
| -u/–URL | 目标 URL |
| -i/–import-urls | 从文件导入目标 |
| -s/–stdin | 从 stdin 扫描 URL |
| -o/–输出 | 输出文件的路径 |
| -m/–方法 | 请求方法(获取/发布) |
| -d/–数据 | 发布数据 |
| -uA/–用户代理 | 指定用户代理 |
| -To/–超时 | 连接超时 |
| -c/–cookie | 指定 cookies |
| -v/–验证 | 验证 SSL 证书。 |
| -t/–螺纹 | 并发线程数 |
| -sB/–跳过横幅 | 跳过横幅和参数信息 |
| -sP/–show-有效负载 | 显示所有可用的 CRLF 有效负载 |

## 使用

单一 URL 扫描:

**$ crlf suite-u " http://test PHP . vulnweb . com "**

多个 URL 扫描:

**$ crlfsuite -i targets.txt**

来自 stdin:

**$ sub finder-d google.com-silent | httpx-silent | crlf suite-s**

指定 cookies:

**$ crlf suite-u " http://test PHP . vulnweb . com "-cookies " key = val；newkey=newval"**

使用 POST 方法:

**$ crlfsuite-I targets . txt-m POST-d " key = val&new key = new val "**

[**Download**](https://github.com/Nefcore/CRLFsuite)