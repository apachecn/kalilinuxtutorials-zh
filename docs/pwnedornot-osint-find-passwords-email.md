# PwnedOrNot : OSINT 工具，用于查找受损电子邮件地址的密码

> 原文：<https://kalilinuxtutorials.com/pwnedornot-osint-find-passwords-email/>

[![PwnedOrNot : OSINT Tool To Find Passwords For Compromised Email Addresses](img/3cfe03114504b4a74dbb16fce82e5013.png "PwnedOrNot : OSINT Tool To Find Passwords For Compromised Email Addresses")](https://1.bp.blogspot.com/-7_GWsCs5Jsw/XVr2AwGTxHI/AAAAAAAACEs/D9O6F9Jt9FoN3jgg0dv_vEtgTVXEJ1Y1wCLcBGAs/s1600/New.png)

**pwnedOrNot** 使用[**have been pwned**](https://haveibeenpwned.com/API/v3)v2 API 测试电子邮件账户，并试图在 **Pastebin 转储**中找到**密码**。[**havebeenpwned**](https://haveibeenpwned.com/API/v3)提供了大量关于被入侵邮件的信息，以下脚本显示了一些有用的信息:

*   违约名称
*   域名
*   违约日期
*   制造状态
*   验证状态
*   退休状态
*   垃圾邮件状态

有了所有这些信息，如果转储可以访问并且包含密码，它就可以很容易地找到受损电子邮件的密码

**在**上测试

*   **卡莉 Linux 2019.1**
*   **BlackArch Linux**
*   **Ubuntu 18.04**
*   **卡利网猎人**
*   **Termux**

**也可理解为-[Iris:WinDbg 扩展，用于显示 Windows 进程缓解](https://kalilinuxtutorials.com/iris-windbg-extension/)**

**安装**

**Ubuntu/Kali Linux/Nethunter/Termux**

**git 克隆 https://github.com/thewhiteh4t/pwnedOrNot.git
CD pwnedOrNot
pip 3 安装请求**

**BlackArch Linux**

**吃豆人-S pwnedornot**

**更新**

**cd pwnedOrNot
git pull**

**用途**

**python 3 pwnedornot . py-h** 
**用法:**pwnedornot . py[-h][-e EMAIL][-f FILE][-d DOMAIN][-n][-l]
[-c CHECK]

**可选参数:** -h，–help 显示此帮助消息并退出
-e EMAIL，–EMAIL 您要测试的电子邮件地址
-f FILE，–FILE –no dump 仅检查违规信息并跳过密码转储
-l，–List 获取所有 pwned 域的列表
-c 检查， –检查检查检查您的域名是否被 pwned

**== >示例** 
**== >检查单个电子邮件** python 3 pwnedornot . py-e
**= = =
)或**python 3 pwnedornot . py–Email

=>**从文件中检查多个电子邮件**

python 3 pwnedornot . py-e-d
= =>**或**
python 3 pwnedornot . py-f–Domain

= =>**仅获取违规信息，跳过密码转储**
python 3 pwnedornot . py-e-n
= =>**或**
python 3 pwnedornot . py-n

**视频教程**

[https://www.youtube.com/embed/R_Y_QzVmERA?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/R_Y_QzVmERA?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/thewhiteh4t/pwnedOrNot)