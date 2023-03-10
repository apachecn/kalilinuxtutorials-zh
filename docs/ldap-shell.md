# LDAP shell : AD ACL 滥用

> 原文：<https://kalilinuxtutorials.com/ldap-shell/>

[![](img/8ced400dd9d0889a8e4f21cd4f4cd0c5.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilO6VTnQ3Wa4eaZUsgu2l-Rz5B_sRRlbspA4gUUID4MkDEMzMpPYR4aJ3uo2RZ5NjCsonobHdX_bT9QkAcdE5BdArw_1wCypppGmeh7MdAE9ae4Y3dV_o_S6MLxBBXOdohGJ_73ivXT4Id44INQLvAFCDyeX4Ws8DvdFis7UHJn9ww_LicFs41aAv4/s728/h92%20(1).png)

**LDAP shell** 资源库包含一个继承自 ldap_shell 的小工具。

## 装置

这些工具仅与 Python 3.5+兼容。从 GitHub 克隆存储库，安装依赖项，然后就可以开始了:

**git 克隆 https://github.com/z-Riocool/ldap_shell.git
CD LDAP _ shell
python 3 setup . py 安装**

## 使用

### 连接选项

**LDAP _ shell domain.local/user:password
LDAP _ shell domain.local/user:password-DC-IP 192 . 168 . 1 . 2
LDAP _ shell domain.local/user-哈希 aad3b 435 b 51404 eeaad3b 435 b 51404 ee:aad3b 435 b 51404 eeaad3b 435 b 51404 e 1
export krb 5 cc name =/home/user/ticket . ccache
LDAP _ shell-k-no-pass domain.local/user【T5**

## 功能

**获取信息
转储–转储域。
搜索查询[属性，]–按名称、distinguishedName 和 sAMAccountName 搜索用户和组。
get_user_groups 用户–检索该用户所属的所有组。
get_group_users 组–检索组的所有成员。
get _ laps _ password computer–检索与给定计算机(sAMAccountName)相关联的 LAPS 密码。
Get _ maq user–获取当前用户的 ms-DS-machineaccountoquota。
滥用 ACL
add_user_to_group 用户组–将用户添加到组中。
del_user_from_group 用户组–从组中删除用户。
change _ password user[password]–尝试更改给定用户的密码。需要 LDAPS。
set_rbcd 目标被授权者–授予被授权者(sAMAccountName)对目标(sAMAccountName)执行 rbcd 的能力。
Clear _ rbcd target–清除基于资源的约束委托配置信息。
set_dcsync 用户–如果您对域对象具有写访问权限，请将 DS-Replication 权限分配给所选用户。
del_dcsync 用户–删除所选用户的 DS-复制权限。
set_genericall 目标被授权者–将给定目标对象(sAMAccountName)的完全控制权授予被授权者(sAMAccountName)。
set_owner 目标被授权者–滥用 WriteOwner 权限。
dacl _ Modify–修改 ACE(添加/删除)。用法:修改 ACE 的目标、被授权者、添加/删除和掩码名称或对象类型。
set_dontreqpreauth 用户真/假–将不需要预认证标志设置为真或假。
get _ NTLM user–Shadow Credentials 方法滥用 GenericAll、GenericWrite 和 AllExtendedRights 权限
Write _ gpo _ dacl user GPO sid–为给定用户向 GPO 写入完全控制 ACE。必须用{}将 gpoSID 括起来。
Misc
add _ computer computer[password]–使用指定的密码将一台新计算机添加到域中。需要 LDAPS。
del _ computer computer–从域中删除一台新计算机。
添加用户新用户[父用户]–创建新用户。
Disable _ account user–禁用用户的帐户。
Enable _ account user–启用用户的帐户。
退出–终止本次会话。**

[**Download**](https://github.com/PShlyundin/ldap_shell)