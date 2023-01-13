# Kerberos ast:Kerberos ast 攻击-纯 Python-

> 原文：<https://kalilinuxtutorials.com/kerberoast/>

[![](img/00b2707312aa65a2ed72aaeb63adef7e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgUe2CUSMsU480pQCpY3QX7XF9W7qxvTFlf0du0fCj76gxXB9Ewb7AkzNKXQuPx1sg1a87Mhe3CT9G4igujaIRN7q99LExwXlNawQTFag1CL3HC6BQ2sZlzw0-losEpdGOTcwmK94cdFZSOR9kPifsSv2gQPXP_mww_J8uURgb73GPJ7rHYWNCKJDef=s760)

**Kerberos ast**攻击工具包——纯 python

**安装**

**pip3 安装 Kerberos ast**

**先决条件**

Python 3.6 参见 requirements.txt

**为不耐烦的**

重要提示:LDAP 和 Kerberos 可接受的目标 url 格式如下:
**`<ldap_connection_url>`:`<protocol>+<auth-type>://<domain>\<user>:<password>@<ip_or_hostname>/?<param1>=<value1>`
`<kerberos_connection_url>`:`<protocol>+<auth-type>://<domain>\<user>:<password>@<ip_or_hostname>/?<param1>=<value1>`**

步骤-与 SSPI-: `**kerberoast auto <DC_ip>**`

步骤-未使用 SSPI:

*   通过 LDAP
    `**kerberoast ldap all <ldap_connection_url> -o ldapenum**`查找易受攻击的用户
*   在`**ldapenum_asrep_users.txt**`文件中对用户使用 ASREP bake
    `**kerberoast asreproast <DC_ip> -t ldapenum_asrep_users.txt**`
*   使用 SPN 烤兑用户在`**ldapenum_spn_users.txt**`文件
    中`**kerberoast spnroast <kerberos_connection_url> -t ldapenum_spn_users.txt**`
*   用 hashcat 破解 SPN 烘焙和 ASPREP 烘焙输出

**命令**

**ldap**

此命令组用于通过 LDAP 枚举潜在易受攻击的用户。

**指挥结构**

`**kerberoast ldap <type> <ldap_connection_url> <options>**`

`**Type**`:支持列举三种类型的用户

*   `**spn**`枚举设置了`**servicePrincipalName**`属性的用户。
*   `asrep`列举在其 UAC 属性中设置了`**DONT_REQ_PREAUTH**`标志的用户。
*   开始上面提到的所有枚举。

`**ldap_connection_url**`:以 msldap url 格式指定用户凭证和目标服务器(参见帮助)

**`options` :
`-o`** :输出文件基础名

**蛮**

该命令通过强制 kerberos 服务使用可能的候选用户名来执行用户名枚举

**指挥结构**

`**kerberoast brute <realm> <dc_ip> <targets> <options>**`

`**realm**`:Kerberos 领域通常看起来像`**COMPANY.corp**`
`**dc_ip**`:域控制器的 IP 或主机名
`**targets**`:包含可能的候选用户名
`**options**`的文件的路径:
`**-o**`:输出文件基本名称

**asreproast**

该命令用于执行重播攻击

**指挥结构**

`**kerberoast asreproast <dc_ip> <options>**`

`**dc_ip**`:域控制器
`**options**`的 IP 或主机名:
`**-r**`:指定要使用的 kerberos 领域。它会覆盖所有其他领域信息。
`**-o**`:输出文件基名
`**-t**`:包含对
`**-u**`进行攻击的用户名的文件路径:指定要攻击的用户。格式是`<username>`或`<username>@<realm>`，但是在第一种情况下，必须使用`-**r**`选项来指定领域

**spnroast**

该命令用于执行 SPNroast(又名 kerberoast)攻击。

**指挥结构**

`**kerberoast spnroast <kerberos_connection_url> <options>**`

**`kerberos_connection_url` :** 以 kerberos URL 格式指定用户凭证和目标服务器(参见帮助)

`**options**` :
`**-r**`:指定要使用的 kerberos 领域。它会覆盖所有其他领域信息。
`**-o**`:输出文件基名
`**-t**`:包含对
`**-u**`进行攻击的用户名的文件路径:指定攻击的用户。格式是`**<username>**`或`**<username>@<realm>**`，但是在第一种情况下，必须使用`**-r**`选项来指定领域

[**Download**](https://github.com/skelsec/kerberoast)