# PwnedOrNot : OSINT 工具，用于查找受损电子邮件地址的密码

> 原文：<https://kalilinuxtutorials.com/pwnedornot-passwords-compromised-email/>

PwnedOrNot 是一个查找受损电子邮件地址密码的工具。pwnedOrNot 使用 haveibeenpwned v2 api 来测试电子邮件帐户，并试图在 Pastebin 转储中找到密码。

**特性**

[**havebeenpwned**](https://haveibeenpwned.com/API/v2)提供了大量关于被入侵邮件的信息，以下脚本显示了一些有用的信息:

*   违约名称
*   域名
*   违约日期
*   制造状态
*   验证状态
*   退休状态
*   垃圾邮件状态

有了所有这些信息 **pwnedOrNot** 就可以很容易地找到受损电子邮件的密码，如果转储是可访问的并且包含密码的话。

**又念——[ARDT:Akamai 反射式 DDoS 工具](https://kalilinuxtutorials.com/ardt-akamai-reflective-ddos-tool/)**

#### 测试于

*   Kali Linux 18.2
*   Ubuntu 18.04
*   卡利·网络猎人
*   泰尔穆克

**安装**

Ubuntu/Kali Linux/Nethunter/Termux

**chmod 777 install.sh
。/install.sh**

**用途**

**python 3 pwnedornot . py-h

用法:pwnedornot . py[-h][-e EMAIL][-f FILE][-n][-l]
[-c CHECK]

可选参数:
-h，–help 显示此帮助消息并退出
-e EMAIL，–EMAIL 您要测试的电子邮件地址
-f FILE，–FILE 加载一个具有多个电子邮件地址的文件
-d DOMAIN，，**

**示例**

**检查单个邮件**
python 3 pwnedornot . py-e
或
python 3 pwnedornot . py–Email

**检查多个邮件从文件**
python 3 pwnedornot . py-f
或
python 3 pwnedornot . py–File

**过滤结果为一个域名【例如:adobe.com】 跳过密码转储**
python 3 pwnedornot . py-e-n
或
python 3 pwnedornot . py-f–no Dumps

**获取所有被攻破域的列表**
python 3 pwnedornot . py-l
或
python 3 pwnedornot . py–List

**检查一个域是否被 Pwned**
python

**演示**

[https://www.youtube.com/embed/R_Y_QzVmERA?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/R_Y_QzVmERA?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/thewhiteh4t/pwnedOrNot)