# PSPKIAudit:用于审核 Active Directory 证书服务(AD CS)的 PowerShell 工具包

> 原文：<https://kalilinuxtutorials.com/pspkiaudit/>

[![](img/cf47c985074cd020769db4da638ec6e2.png)](https://1.bp.blogspot.com/-gsyqnf83ZIE/YS9euUZEg0I/AAAAAAAAKms/SMNZLC56fgg-DsZrx8EjD8Q0DxiYIP49ACLcBGAsYHQ/s809/download%2B%25281%2529.png)

**PSPKIAudit** 是一个用于审计活动目录证书服务(AD CS)的 PowerShell 工具包。

它建立在 PKISolution 的 PSPKI 工具包(微软公共许可证)之上。这个 repo 包含一个比 PSGallery(见`**PSPKI**`目录)中可用的更新版本的 PSPKI。vadims Podans(PSP ki 的创建者)慷慨地提供了这个版本，因为它包含了几个 bug 的补丁。

**本自述文件仅作为一个起点，有关完整的详细信息和防御指南，请参见“认证二手车”白皮书。**

该模块包含以下主要功能:

1.  invoke-PKI audit–审核当前林的 AD CS 设置，主要分析 CA 服务器和发布的模板，寻找潜在的权限提升机会。
2.  get-cert request-通过查询 CA 的数据库来检查 CA 颁发的证书。主要目的是发现可能滥用了证书模板权限提升漏洞的证书请求。此外，如果用户或计算机受到危害，事故响应者可以使用它来查找 CA 服务器向受到危害的用户/计算机颁发的证书(该证书应被撤销)。

**警告:**这个代码是测试版！我们相信`**Invoke-PKIAudit**`不会影响环境，因为它查询的数据量非常有限。我们还没有针对典型的 CA 服务器工作负载对`**Get-CertRequest**`进行严格的测试。`**Get-CertRequest**`直接查询 CA 的数据库，可能需要处理数千个结果，这可能会影响性能。

如果没有结果，这并不能保证您的环境是安全的！！

我们也不能保证我们的缓解建议将使您的环境安全或不会中断运营！

您有责任与您的 Active Directory/PKI/体系结构团队讨论，以确定适合您环境的最佳缓解措施。

如果代码中断，或者我们遗漏了什么，请提交问题或请求进行修复！

*   设置
*   审核 AD CS 错误配置
    *   输出说明
    *   es C1–错误配置的证书模板
    *   es C2–错误配置的证书模板
    *   es C3–错误配置的注册代理模板
    *   ESC4 易受攻击的证书模板访问控制
    *   es C5–易受攻击的 PKI AD 对象访问控制
    *   ESC 6–EDITF _ attributesubjectaltname 2
    *   ESC7 易受攻击的证书颁发机构访问控制
    *   ESC 8–NTLM 中继到 AD CS HTTP 端点
    *   杂项-显式映射
*   培训现有的已颁发证书请求

**设置**

**要求**

*   使用提升的 PowerShell 提示符安装以下内容:

*   RSAT 的**证书服务**和**活动目录**功能。使用以下命令安装:

**Get-windows capability-Online-Name " Rsat。* " | where Name-match " certificate services | ActiveDirectory " | Add-windows capability-Online**

**导入**

下载模块，将其解压缩到一个文件夹中。然后，使用以下命令导入模块:

**CD PSP kiaudit
Get-child item-Recurse | Unblock-File
导入-模块。\PSPKIAudit.psm1**

**审核 AD CS 错误配置**

运行`**Invoke-PKIAudit [-CAComputerName CA.DOMAIN.COM | -CAName X-Y-Z]**`将运行现有 AD CS 环境的所有审核检查，包括枚举各种证书颁发机构和证书模板设置。

任何错误配置(ESC1-8)都将作为属性显示在 CA/template 结果中，以识别发现的特定错误配置。

如果您想要更改用于测试注册/访问控制的组/用户，请修改`**Invoke-PKIAudit.ps1**`顶部的`**$CommonLowprivPrincipals**`正则表达式

如果要将所有 CA 信息导出到 csv，请运行:`**Get-AuditCertificateAuthority [-CAComputerName CA.DOMAIN.COM | -CAName X-Y-Z] | Export-Csv -NoTypeInformation CAs.csv**`

如果您想要将所有已发布的模板信息导出到 csv(不仅仅是易受攻击的模板)，请运行:`**Get-AuditCertificateTemplate [-CAComputerName CA.DOMAIN.COM | -CAName X-Y-Z] | Export-Csv -NoTypeInformation templates.csv**`

**输出解释**

输出有两个主要部分，关于发现的 ca 的详细信息和关于潜在易受攻击的模板的详细信息。

对于证书颁发机构结果:

| 证书颁发机构属性 | 描述 |
| --- | --- |
| 计算机名称 | CA 运行的系统。 |
| 卡纳梅 | CA 的名称。 |
| 配置字符串 | 完整的计算机\CA_NAME 配置字符串。 |
| IsRoot | 如果 CA 是根 CA。 |
| AllowsUserSuppliedSans | 如果 CA 设置了`EDITF_ATTRIBUTESUBJECTALTNAME2`标志。 |
| 漏洞 ACL | CA 是否有易受攻击的 ACL 设置。 |
| 注册校长 | 在 CA 级别拥有`Enroll`特权的主体。 |
| 注册结束点 | CA 的 web 服务注册端点。 |
| NTLMEnrollmentEndpoints | 启用了 NTLM 的 CA 的 web 服务注册端点。 |
| 抑郁症辅助核查表 | 完整的访问控制信息。 |
| 错误配置 | ESCX 指示存在的特定错误配置(如果有)。 |

对于证书模板结果:

| 财产 | 描述 |
| --- | --- |
| 加拿大 | 发布模板的完整 CA config string(null 表示未发布)。 |
| 名字 | 模板名称。 |
| 模式转换 | 模板的模式版本(1/2/3)。 |
| 似…的 | 模板的唯一对象标识符。 |
| 漏洞模板 ACL | 如果模板具有易受攻击的 ACL 设置，则为 True。 |
| 低 PrivCanEnroll | 如果低特权用户可以在模板中注册，则为 True。 |
| 注册供应商主题 | 如果`CT_FLAG_ENROLLEE_SUPPLIES_SUBJECT`标志存在，则为真(即用户可以提供任意 San)。 |
| 增强型 KeyUsage | 模板中启用的使用 eku。 |
| hasauthentaicationeku | 如果模板具有允许身份验证的 EKU，则为 True。 |
| HasDangerousEku | 如果模板有一个“危险的”(任何用途或空)EKU，则为 True。 |
| 注册代理模板 | 如果模板具有“证书申请代理”EKU，则为 True。 |
| CAManagerApproval | 如果注册需要经理批准，则为真。 |
| 发布要求 | 授权签名信息。 |
| 有效期 | 证书的有效期。 |
| 更新期 | 证书的续订期。 |
| 物主 | 拥有证书的主体。 |
| 抑郁症辅助核查表 | 完整的访问控制信息。 |
| 错误配置 | ESCX 指示存在的特定错误配置(如果有)。 |

**ESC 1–错误配置的证书模板**

**详情**

当满足以下条件时，会出现这种权限提升情况:

1.  **企业 CA 授予低特权用户注册权限。**企业 CA 的配置必须允许低权限用户申请证书。有关更多详细信息，请参见白皮书开头的“背景–注册”部分。
2.  **经理批准被禁用。**此设置要求拥有证书“管理员”权限的用户在颁发证书之前审查和批准所请求的证书。有关更多详细信息，请参见白皮书开头的“背景–发行要求”部分。
3.  不需要授权签名。该设置要求任何 CSR 由现有的授权证书签名。有关更多详细信息，请参见白皮书开头的“背景–发布要求”部分。
4.  **一个过于宽松的证书模板安全描述符向低特权用户授予证书注册权限。**拥有证书注册权限允许低特权攻击者请求并获得基于模板的证书。通过证书模板 AD 对象的安全描述符授予注册权限。
5.  **证书模板定义了启用认证的 eku。**适用的 eku 包括客户端身份验证(OID 1.3.6.1.5.5.7.3.2)、PKINIT 客户端身份验证(OID 1.3.6.1.5.2.3.4)或智能卡登录(OID 1.3.6.1.4.1.311.20.2.2)。
6.  **证书模板允许申请人在 CSR 中指定 subjectAltName (SAN)。**如果请求者可以在 CSR 中指定 SAN，则请求者可以作为任何人(例如，域管理员用户)请求证书。证书模板的 AD 对象指定请求者是否可以在其 mspki-certificate-name-flag 属性中指定 SAN。mspki-certificate-name-flag 属性是位掩码，并且如果 CT _ FLAG _ enrolled _ SUPPLIES _ SUBJECT 标志存在，则请求者可以指定 SAN。

**TL；DR** 这种情况意味着没有权限的用户可以请求一个用于域认证的证书，在这里他们可以指定一个任意的别名(比如域管理员)。这可以为提升的用户(如域管理员)生成一个工作证书！

**例子**

**【！潜在易受攻击的证书模板:
CA:DC . the shire . local \ the shire-DC-CA
Name:ESC 1 Template
schema version:2
OID:ESC 1 Template(1 . 3 . 6 . 1 . 4 . 1 . 21 . 8)。56661 . 86868666667
有效期:1 年
续期:6 周
所有者:the shire \ local admin
DACL:NT AUTHORITY \ Authenticated Users(允许)–Read
the shire \ Domain Admins(允许)–Read，Write，Enroll
the shire \ Domain Users(允许)–Enroll
the shire \ Enterprise Admins(允许)–Read，Write，Enroll
THESHIRE\localadmin(允许)–Read，Write
错误配置:ESC1**

**缓解措施**

有几个选择。首先，在证书模板控制台(certtmpl.msc)中右键单击受影响的证书模板，然后单击“属性”

1.  通过“主题名称”删除 CT _ FLAG _ enroller _ SUPPLIES _ SUBJECT 标志，取消选中“在请求中提供”。
    *   这可以防止 CSR 中任意的 SAN 规范。除非模板真的需要别名，否则这可能是最好的解决办法。
2.  通过“扩展”->“应用程序策略”删除“客户端验证”和/或“智能卡登录”eku。
    *   这将阻止使用此模板进行域身份验证。
3.  启用“颁发要求”中的**“CA 证书管理员批准”**。
    *   这会将对此模板的请求放入“待定请求”队列中，该队列必须由证书管理员手动批准。
4.  启用“签发要求”中的**授权签名**(如果您知道自己在做什么)。
    *   这将强制 CSR 由注册代理证书共同签名。
5.  取消低权限用户通过“安全”注册该模板的能力，并取消相应的**注册**权限。

**ESC 2–错误配置的证书模板**

**详情**

当满足以下条件时，会出现这种权限提升情况:

1.  **企业 CA 授予低特权用户注册权限。**细节与 ESC1 中的相同。
2.  **经理批准被禁用。**细节与 ESC1 中的相同。
3.  不需要授权签名。细节与 ESC1 中的相同。
4.  **一个过于宽松的证书模板安全描述符向低特权用户授予证书注册权限。**细节与 ESC1 中的相同。
5.  **证书模板定义了任何目的 EKU 或无 EKU。**任何用途(OID 2.5.29.37.0)都可用于(惊喜！)任何用途，包括客户端认证。如果未指定 eku(即，pkiextendedkeyusage 为空或属性不存在),则该证书相当于从属 CA 证书，可用于任何用途。

**TL；DR** 这非常类似于 ESC1，但是对于任何目的或无 EKU，CT _ FLAG _ enroller _ SUPPLIES _ SUBJECT 标志不需要存在。

**例子**

**【！潜在易受攻击的证书模板:
CA:DC . the shire . local \ the shire-DC-CA
名称:ESC 2 Template
schema version:2
OID:ESC 2 模板(1 . 3 . 6 . 1 . 4 . 1 . 21 . 8)。56667 . 86868668667
有效期:1 年
续期:6 周
所有者:the shire \ local admin
DACL:NT AUTHORITY \ Authenticated Users(允许)–Read
the shire \ Domain Admins(允许)–Read，Write，Enroll
the shire \ Domain Users(允许)–Enroll
the shire \ Enterprise Admins(允许)–Read，Write，Enroll
THESHIRE\localadmin(允许)–Read，Write
错误配置:ESC2**

**缓解措施**

有几个选择。首先，在证书模板控制台(certtmpl.msc)中右键单击受影响的证书模板，然后单击“属性”

1.  取消低权限用户通过“安全”注册该模板的能力，并取消相应的**注册**权限。
    *   这可能是最好的解决办法，因为这些敏感的 eku 不应该提供给低特权用户！
2.  启用“颁发要求”中的**“CA 证书管理员批准”**。
    *   这会将对此模板的请求放入“待定请求”队列中，该队列必须由证书管理员手动批准。
3.  启用“签发要求”中的**授权签名**(如果您知道自己在做什么)。
    *   这将强制 CSR 由注册代理证书共同签名。

**ESC3–错误配置的注册代理模板**

**详情**

当满足以下条件时，会出现这种权限提升情况:

1.  **企业 CA 授予低特权用户注册权限。**细节与 ESC1 中的相同。
2.  **经理批准被禁用。**细节与 ESC1 中的相同。
3.  不需要授权签名。细节与 ESC1 中的相同。
4.  **一个过于宽松的证书模板安全描述符向低特权用户授予证书注册权限。**细节与 ESC1 中的相同。
5.  **证书模板定义了证书申请代理 EKU。**证书申请代理 EKU (OID 1.3.6.1.4.1.311.20.2.1)允许委托人代表另一个用户注册*另一个*证书模板。
6.  **CA 上未实施注册代理限制。**

**TL；DR** 拥有证书请求(又名注册)代理证书的人可以代表域中的任何用户注册其他证书，用于任何需要适当的“授权签名/应用程序策略”发布要求的模式版本 1 模板或模式版本 2+模板，除非在 CA 级别实施了“注册代理限制”。

**例子**

**【！潜在易受攻击的证书模板:
CA:DC . the shire . local \ the shire-DC-CA
名称:ESC 3 Template
schema version:2
OID:ESC 3 模板(1 . 3 . 6 . 1 . 4 . 1 . 21 . 8)。56667 . 86868686667
有效期:1 年
续期:6 周
所有者:the shire \ local admin
DACL:NT AUTHORITY \ Authenticated Users(允许)–Read
the shire \ Domain Admins(允许)–Read，Write，Enroll
the shire \ Domain Users(允许)–Enroll
the shire \ Enterprise Admins(允许)–Read，Write，Enroll
THESHIRE\localadmin(允许)–Read，Write
错误配置:ESC3**

**缓解措施**

有几个选择。首先，在证书模板控制台(certtmpl.msc)中右键单击受影响的证书模板，然后单击“属性”

1.  取消低权限用户通过“安全”注册该模板的能力，并取消相应的**注册**权限。
    *   这可能是最好的解决方案，因为低特权用户不应该使用这种敏感的 EKU！
2.  启用“颁发要求”中的**“CA 证书管理员批准”**。
    *   这会将对此模板的请求放入“待定请求”队列中，该队列必须由证书管理员手动批准。

您还可以通过证书颁发机构控制台(certsrv.msc)实现“注册代理限制”。在受影响的 CA 上，右键单击 CA 名称，然后单击“属性”->“注册代理”。这里有更多关于这种方法的信息。

**ESC 4–易受攻击的证书模板访问控制**

**详情**

证书模板是 Active Directory 中的安全对象，这意味着它们有一个安全描述符，指定哪些 Active Directory 主体对模板有特定的权限。具有易受攻击的访问控制的模板授予非预期主体修改模板中设置的能力。通过修改权限，攻击者可以设置易受攻击的 eku(es C1-es C3)，翻转 CT _ FLAG _ enrolled ee _ SUPPLIES _ SUBJECT(es C1)等设置，和/或删除经理批准或授权签名等“发布要求”。

**例子**

**【！潜在易受攻击的证书模板:
CA:DC . the shire . local \ the shire-DC-CA
Name:ESC 4 Template
schema version:2
OID:ESC 4 Template(1 . 3 . 6 . 1 . 4 . 1 . 21 . 8)。58661 . 86868666667
有效期:1 年
续期:6 周
所有者:the shire \ local admin
DACL:NT AUTHORITY \ Authenticated Users(Allow)–读、写
the shire \ Domain Admins(Allow)–读、写、注册
the shire \ Domain Users(Allow)–读、注册
the shire \ Enterprise Admins(Allow)–读、写、注册
the shire \ local admin(Allow)–读、写
错误配置:ESC4**

**缓解措施**

在证书模板控制台(certtmpl.msc)中右键单击受影响的证书模板，然后单击“属性”。

转到“安全”并删除易受攻击的访问控制条目。

**ESC 5–易受攻击的 PKI AD 对象访问控制**

**详情**

证书模板和证书颁发机构本身之外的许多对象会对整个 AD CS 系统产生安全影响。

这些可能性包括(但不限于):

*   CA 服务器的 AD 计算机对象(即，通过 RBCD 妥协)
*   CA 服务器的 RPC/DCOM 服务器
*   与 PKI 相关的 AD 对象。容器中的任何后代 AD 对象或容器 CN =公钥服务，CN =服务，CN =配置，DC=，DC=(例如，证书模板容器、认证机构容器、NTAuthCertificates 对象等。)

*由于这种特定错误配置的范围很广，我们目前并不在该工具包中默认检查 ESC5。*

CA 服务器本身的访问路径可以在当前的 BloodHound 集合中找到。

CA 服务器的 RPC/DCOM 服务器安全性需要手动分析。

以下命令输出用户列表以及用户对 PKI 相关 AD 对象的控制/编辑权限。

**$ Controllers = Get-AuditPKIADObjectControllers
Format-PKIAdObjectControllers $ Controllers**

确保结果中的所有主体绝对需要列出的权限。通常情况下，非第 0 层帐户(无论是低特权用户/组还是低特权非 AD 服务器管理员)控制着与 PKI 相关的 AD 对象。

**例子**

**the shire \ Cert Publishers(S-1-5-21-3022474190-4230777124-3051344698-517)
generic call CN = the shire-DC-CA，CN =证书颁发机构，CN =公钥服务，CN =服务，CN =配置，DC=THESHIRE，DC =本地
generic call CN = AIA，CN =公钥服务，CN =服务，CN =配置，DC=THESHIRE**

**缓解措施**

对于配置对象，通过 Active Directory 用户和计算机( *dsa.msc* )或 ADSIEdit ( *adsiedit.msc* )删除任何易受攻击的访问控制条目。

**ESC 6–EDITF _ attributesubjectaltname 2**

**详情**

如果在证书颁发机构的配置中翻转了**EDITF _ attributesubjectaltname 2**标志，*任何*证书请求都可以指定任意主题替代名称(San)。这意味着任何为域身份验证配置的模板，如果也允许非特权用户注册(例如，默认的**用户**模板)，都可能被滥用来获取允许我们作为域管理员(或任何其他活动用户/机器)进行身份验证的证书。

**在您的环境中绝对不要设置此设置。**

**例子**

**= = = Certificate Authority = = =
computer name:DC . the shire . local
can name:the shire-DC-CA
config string:DC . the shire . local \ the shire-DC-CA
is root:True
allowusersuppliedsans:True
VulnerableACL:False
enrollment principals:the shire \ Domain Users
the shire \ Domain Computers
the shire \ cert manager
the shire \ cert min
Enroll
the shire \ Domain Computers(Allow)–Enroll
the shire \ Enterprise Admins(Allow)–manage ca，manage certificates
the shire \ cert manager(Allow)–manage certificates，Enroll
the shire \ cert min(Allow)–manage ca，Enroll
the shire \ nested 3(Allow)–manage certificates，Enroll
错误配置:ESC6
！ ]以上 CA 配置错误！
…(snip)…
【！在这个 CA 上设置的下列模板可能有漏洞:
CA:DC . the shire . local \ the shire-DC-CA
Name:User
schema version:1
OID:1 . 3 . 6 . 1 . 1 . 21 . 8 . 203030366667
有效期:1 年
续期:6 周
所有者:the shire \ Enterprise Admins
DACL:NT AUTHORITY \ Authenticated Users(Allow)–读取
the shire \ Domain Admins(Allow)–读取、写入、注册
the shire \ Domain Users(Allow)–读取、注册
the shire \ Enterprise Admins(Allow)–读取、写入、注册
错误配置:**

**缓解措施**

立即删除此标志，并使用针对 CA 服务器的提升权限从 PowerShell 提示符重新启动受影响的证书颁发机构:

**PS C:>certutil-config " CA _ HOST \ CA _ NAME "-setreg policy \ edit flags-EDITF _ attributesubjectaltname 2
PS C:>Get-Service-computer NAME CA _ HOST certsvc | Restart-Service-Force**

**ESC 7–易受攻击的认证机构访问控制**

**明细**

除了证书模板之外，证书颁发机构本身也有一组保护各种 CA 操作的权限。可以从 certsrv.msc 访问这些权限，右键单击 CA，选择属性，然后切换到安全选项卡。

有两种权限是安全敏感的，如果非预期主体拥有它们，它们将是危险的:

*   **ManageCA** (又名“CA 管理员”)—允许管理性 CA 操作，包括(远程)翻转 EDITF_ATTRIBUTESUBJECTALTNAME2 位，产生 ESC6。
*   **ManageCertificates** (又名“证书管理员/官员”)—允许委托人批准待定的证书请求，取消“管理员批准”的颁发要求/保护

**例子**

**= = = Certificate Authority = = =
computer name:DC . the shire . local
can name:the shire-DC-CA
config string:DC . the shire . local \ the shire-DC-CA
is root:True
allowusersuppliedsans:False
VulnerableACL:True
enrollment principals:the shire \ Domain Users
the shire \ Domain Computers
the shire \ cert manager
the shire \ cert min
Enroll
THESHIRE\Do** 主计算机(允许)–Enroll
**the shire \ Enterprise Admins(允许)–manage ca，manage certificates
the shire \ cert manager(允许)–manage certificates，Enroll
THESHIRE\certadmin(允许)–manage ca，Enroll
THESHIRE\Nested3(允许)–manage certificates，Enroll
错误配置:ESC7
[！ ]以上 CA 配置错误！**

**缓解措施**

在受影响的 CA 上打开证书颁发机构控制台(certsrv.msc ),右键单击 CA 名称，然后单击“属性”。

转到“安全”并删除易受攻击的访问控制条目。

**ESC 8–NTLM 中继到 AD CS HTTP 端点**

**注意:**PSP kiaudit 中的这一特定检查仅检查 NTLM 是否存在于任何已发布的注册端点。*它不会检查这些支持 NTLM 的端点是否存在身份验证的扩展保护，因此可能会出现误报！*

**详情**

AD CS 通过管理员可以安装的其他 AD CS 服务器角色支持多种基于 HTTP 的注册方法。这些基于 HTTP 的证书注册接口都容易受到 NTLM 中继攻击。

使用 NTLM 中继，被入侵机器上的攻击者可以模拟任何入站 NTLM 身份验证的 AD 帐户。在模拟受害者帐户时，攻击者可以访问这些 web 界面，并根据用户或机器证书模板请求客户端身份验证证书。

**例子**

**= = = Certificate Authority = = =
computer name:DC . the shire . local
can name:the shire-DC-CA
config string:DC . the shire . local \ the shire-DC-CA
is root:True
allowusersuppliedsans:False
VulnerableACL:False
enrollment principals:the shire \ Domain Users
the shire \ Domain Computers
the shire \ cert manager
the shire \ cert min
Enroll
the shire \ Domain Computers(Allow)–Enroll
the shire \ Enterprise Admins(Allow)–manage ca，manage certificates
the shire \ cert manager(Allow)–manage certificates，Enroll
the shire \ cert min(Allow)–manage ca，Enroll
the shire \ nested 3(Allow)–manage certificates，Enroll
错误配置:ESC8
！ ]以上 CA 配置错误！**

**缓解措施**

请删除 HTTP(S)注册端点，禁用端点的 NTLM，或者启用身份验证的扩展保护。请参见白皮书中的**强化 AD CS HTTP 端点–预防 ENT8** 了解更多详情。

**杂项–显式映射**

对于某些情况，另一种可能的缓解方法是强制证书的显式映射。这将禁止在对 Active Directory 进行身份验证时在证书中使用备用 San。

对于 Kerberos，设置**HKEY _ LOCAL _ MACHINE \ SYSTEM \ current control set \ Services \ Kdc！将 SubjectAltName** 键设置为 00000000 会强制进行显式映射。KB4043463 有更多细节。

禁用 SChannel 的显式映射并没有真正的文档，但是基于我们的研究设置 0x1 或 0x2 到**HKEY _ LOCAL _ MACHINE \ current Control set \ Control \ security providers \ SChannel！CertificateMappingMethods** 密钥似乎阻止了 San，但还需要更多的测试。

**对现有颁发的证书请求进行分类**

**警告:**该功能已经在大型环境中进行了最低限度的测试！

**注意:**请参阅白皮书中的“监控用户/机器证书注册-检测 1”以了解更多信息以及如何使用 certutil 执行这些搜索。

如果您想要检查现有的已颁发证书请求，例如查看是否有任何请求指定了任意 San，或者是针对特定模板/由特定主体请求的,`**Get-CertRequest [-CAComputerName COMPUTER.DOMAIN.COM | -CAName X-Y-Z]**`函数构建于各种 PSPKI 函数之上，以提供更多上下文信息。

具体而言，为域中每个当前颁发的证书提取原始证书签名请求(CSR ),以及特定信息(即，是否指定了 SAN、请求者名称/机器/进程等。)是从丰富 CSR 对象的请求中构造的。

以下标志可能很有用:

| 旗 | 描述 |
| --- | --- |
| **-哈桑** | 仅返回已颁发的证书，该证书具有请求中指定的使用者替代名称。 |
| **-请求者域\用户** | 仅返回特定请求用户的已颁发证书请求。 |
| **-模板 TEMPLATE_NAME** | 仅返回指定模板名称的已颁发证书请求。 |

要将所有颁发的证书请求导出到 csv，请使用 **`Get-CertRequest | Export-CSV -NoTypeInformation requests.csv`。**

以下是一个结果条目示例，显示了使用 Certify 指定主题备用名称(s an)的情况:

CA:DC . the shire . local**\ the shire-DC-CA
request id:4602
request ername:the shire \ Cody
request machine name:dev . the shire . local
request process name:Certify.exe
subject altnames extension:
subject altnames at trib:Administrator
序列号:55000011 fab 00000011 fa
证书模板
请求日期:2021 年 6 月 3 日下午 5:54:51
开始日期:2021 年 6 月 3 日下午 5:44:51
结束日期:2022 年 6 月 3 日下午 5:44:51
CA:DC . the shire . local \ the shire-DC-CA
请求 ID : 4603
请求者名称:THESHIRE\cody
请求者机器名称:dev.theshire.local**

`**SubjectAltNamesExtension**`属性意味着 x509 SubjectAlternativeNames 扩展用于指定 SAN，对于带有`**CT_FLAG_ENROLLEE_SUPPLIES_SUBJECT**`标志的模板会发生这种情况。`**SubjectAltNamesAttrib**`属性意味着使用了 x509 名称/值对，这在设置了`**EDITF_ATTRIBUTESUBJECTALTNAME2**` CA 标志的情况下指定 SAN 时会发生。

可以使用 PSPKI 的 Revoke-Certificate 功能撤销现有的已颁发证书:

`**PS C:\> Get-CertificationAuthority <CAName> | Get-IssuedRequest -RequestID <X> | Revoke-Certificate -Reason "KeyCompromise"**`

-Reason 的适用值为“密钥泄露”、“不正确”和“未指定”。

[**Download**](https://github.com/GhostPack/PSPKIAudit)