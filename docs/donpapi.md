# DonPAPI:远程转储 DPAPI Credz

> 原文：<https://kalilinuxtutorials.com/donpapi/>

[![](img/8bc50c301a862c25f574f4578c699e77.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh31moiawfG0NNArrw3AJ_ZGYLB7xaitSlUnjgYuWKMQA2C-zLFjQ5-lUBm-J3v5NFvvYyZ9AdsX-24U8-Dq6cVFR6-HM0hUmJXHrgtRNhiMqY9RjaXbAYxjzGxiIb6nqDwA78oU4AhPtMemFTiI0HOgDDXfk95oq-HqODfua6gNz-xHaDcGbmk3p6W=s728)

**DonPAPI** 是远程转储 DPAPI Credz。

**DPAPI 转储**

DPAPI 保护许多凭据。

我们的目标是找到这些“安全的”凭据，并使用以下方法检索它们:

*   用户口令
*   DPAPI 备份密钥域
*   本地机器 DPAPI 密钥(保护`**TaskScheduled**` blob)

**当前收集的信息**

*   Windows 凭据(任务计划凭据及更多)
*   Windows 保管库
*   Windows RDP 凭据
*   AdConnect(仍需要手动操作)
*   Wifi 钥匙
*   internet explorer 屏幕元素
*   Chrome cookies 和凭证
*   Firefox cookies 和凭证
*   VNC 密码
*   mRemoteNG 密码(默认配置)

**检查一点合规性**

*   SMB 签名状态
*   审核范围的操作系统/域/主机名/Ip

**作战使用**

使用主机上的本地管理员帐户，我们可以:

*   收集机器保护的 DPAPI 机密
    *   ScheduledTask 将包含配置为运行任务的帐户的明文登录/密码
    *   Wi-Fi 密码
*   为每个用户配置文件提取主密钥的哈希值(主密钥受到用户密码的保护，让我们尝试用 Hashcat 来破解它们)
*   确定谁从哪里连接，以便识别管理员的个人计算机。
*   提取其他非 dpapi 保护的机密(VNC/火狐/mRemoteNG)
*   从 IE、Chrome、Firefox 收集受保护的秘密，并开始接触 Azure 租户。

使用用户密码或域 PVK，我们可以解除对用户 DPAPI 机密的保护。

**例子**

使用管理员帐户转储目标计算机的所有机密:

**DonPAPI.py 域/用户:passw0rd@target**

使用用户的哈希

**don papi . py–hashes:domain/user @ target**

使用 kerberos (-k)和本地身份验证(-local_auth)

**DonPAPI.py -k 域/用户@目标
DonPAPI.py -local_auth 用户@目标**

使用具有 LAPS 密码读取权限的用户

**don papi . py-laps DOM**ain/user:pass w0 rd @ target

还可以向工具提供将在目标上测试的凭证列表。东帕皮会试着用它们来破译万能钥匙。

此凭据文件必须具有以下语法:

**用户 1:通行证 1
用户 2:通行证 2
……**

**don papi . py-credz credz _ file . txt 域/用户:passw0rd@target**

当域管理员用户可用时，可以使用 impacket `dpapi.py`工具转储域备份密钥。

**DP API . py backup key–导出**

这个备份密钥可以用来转储所有域用户的秘密！

**python donpapi . py-pvk domain _ backup key . pvk domain/user:pass w0 rd @ domain _ network _ list**

目标可以是包含目标列表(每行一个)的 IP、IP 范围、CIDR 文件

**Opsec 考虑**

RemoteOps 部分可能会被一些 EDR 人发现。可以使用`**--no_remoteops**`标志禁用它，但这样将不会检索机器 DPAPI 密钥，也不会获取计划任务凭据/Wi-Fi 密码。

**安装**

**git 克隆 https://github.com/login-securite/DonPAPI.git
CD don papi
python 3-m pip install-r requirements . txt
python 3 don papi . py**

[**Download**](https://github.com/login-securite/DonPAPI)