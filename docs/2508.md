# linWinPwn:一个 Bash 脚本，它自动化了许多活动目录枚举和漏洞检查

> 原文：<https://kalilinuxtutorials.com/linwinpwn/>

[![](img/6d5cf1f05e6d5f812848fb8358957ad4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1dTKAEKE2a9H0lEdbjr8EZ3zm8ghjN1TYTFdAaLMbzu5SZWJjiQlnn-T0cvBWbBo3CmVdAXUMtUYdOkxerferkBVtJF5_drU69D1QB8qXmuQ7cnrO2FhXUj1e8Qyy6HD20zvCgV9e4-nENuTWCI6cX72t9iUi4bnv6KG-sYLiREHqGtjGvIuDUGD-/s728/download.png)

linWinPwn 是一个 bash 脚本，它自动执行许多活动目录枚举和漏洞检查。该脚本利用并依赖于许多工具，包括:impacket、bloodhound、crackmapexec、ldapdomaindump、lsassy、smbmap、kerbrute、adidnsdump。

## 设置

Git 克隆存储库并使脚本可执行

**git 克隆 https://github . com/lefay jey/linwinwn
CD linwinwn；chmod+x linwinwn . sh**

使用`**install.sh**`脚本在 Kali 机器上安装需求

**chmod +x install.sh
sudo。/install.sh**

在非 Kali 机器上，改为运行`**install_nonkali.sh**`脚本

**chmod+x install _ non kali . sh
sudo。/install_nonkali.sh**

如果您遇到 DNS 问题或时间同步错误，运行带有`**-d**`的`**configure.sh**`脚本进行 DNS 更新，带有`**-n**`的脚本进行 NTP 同步

*警告:脚本将更新/etc/resolv.conf*

**chmod +x configure.sh
sudo。/configure.sh -t -d -n**

## 使用

### 模块

linWinPwn 脚本包含 4 个模块，可以单独使用也可以同时使用。

**默认(最快):ad_enum，kerberos** (可选:仅使用`**-O**`运行 OPSEC 安全检查)

**。/linWinPwn.sh -d -u -p -t -o**

**用户模块:ad_enum、kerberos、scan_shares、vuln_checks、mssql_enum**

**。/linwinpwn . sh-M user-d-u-p-t-o**

**所有模块:ad_enum、kerberos、scan_shares、vuln_checks、mssql_enum、pwd_dump**

**。/linwinpwn . sh-M all-d-u-p-t-o**

**模块 ad_enum:** 活动目录枚举

**。/linwinpwn . sh-M ad _ enum-d-u-p-t-o**

## 用例

对于所描述的每种情况，linWinPwn 脚本执行不同的检查，如下所示。

**案例 1:未经认证**

*   模块 ad_enum
    *   摆脱暴力
    *   用户枚举
    *   ldapdomaindump 匿名枚举
    *   检查是否强制 ldap 签名，检查 LDAP 中继
*   模块 kerberos
    *   槽杆用户喷雾
    *   使用收集的用户列表重新发布(并使用开膛手约翰和 rockyou 单词列表破解哈希)
*   模块扫描 _ 共享
    *   SMB 在已识别的服务器上共享匿名枚举
*   模块漏洞检查
    *   已识别服务器上 WebDav 和后台打印程序服务的枚举
    *   检查 zerologon、petitpotam、nopac 的弱点

**。/linWinPwn.sh -M user -t**

**情况 2:标准账户(使用密码、NTLM 哈希或 Kerberos 票据)**

*   使用 adidnsdump 提取 DNS
*   模块 ad_enum
    *   警犬数据收集
    *   ldapdomaindump 枚举
    *   委托信息提取
    *   GPP 密码提取
    *   使用 certify 提取 ADC 信息
    *   检查是否强制 ldap 签名，检查 LDAP 中继
    *   提取用户的 MachineAccountQuota、密码策略和包含“pass”的用户描述
    *   LAPS 和 gMSA 转储
*   模块 kerberos
    *   kerbrute user=pass 枚举
    *   作为重写(以及使用开膛手约翰和 rockyou 单词表来破解散列)
    *   Kerberoasting 认证(以及使用开膛手约翰和 rockyou 单词表破解散列)
*   模块扫描 _ 共享
    *   所有域服务器上的 SMB 共享枚举
*   模块漏洞检查
    *   所有域服务器上的 WebDav 和后台打印程序服务的枚举
    *   检查 zerologon、petitpotam、nopac 的弱点
*   模块 mssql_enum
    *   检查 mssql 权限提升路径

**。/linWinPwn.sh -M user -d -u -p -t**

**情况 3:管理员账户(使用密码、NTLM 散列或 Kerberos 票据)**

*   所有“标准用户”检查
*   模块 pwd_dump
    *   secretsdump 在所有域服务器上或在提供的带有`**-S**`的服务器列表上
    *   lsassy on 在所有域服务器上或在提供的服务器列表上，带有`**-S**`

**。/linwinpwn . sh-M all-d-u-p-t-S**

[**Download**](https://github.com/lefayjey/linWinPwn)