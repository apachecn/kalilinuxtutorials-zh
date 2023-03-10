# SharpHook : Tool Tath 使用各种 API 钩子来给我们想要的凭证

> 原文：<https://kalilinuxtutorials.com/sharphook/>

[![SharpHook : Tool Tath Uses Various API Hooks In Order To Give Us The Desired Credentials](img/06d09775402733bab2d69f47fc9d0696.png "SharpHook : Tool Tath Uses Various API Hooks In Order To Give Us The Desired Credentials")](https://1.bp.blogspot.com/-HdIUCy3HMjQ/YN626NSXadI/AAAAAAAAJxo/3n4UUd6dcrM2ObJtDlxPRmk79qVdYY66gCLcBGAsYHQ/s1033/2.png)

SharpHook 受到了 [SharpRDPThief 项目](https://github.com/passthehashbrowns/SharpRDPThief)的启发，它使用了各种 API 挂钩来给我们提供想要的凭证。

在后台，它使用 EasyHook 项目，一旦所需的进程启动并运行，SharpHook 将自动将其依赖项注入目标进程，然后，它将通过 EasyHook 的 IPC 服务器向我们发送凭证。

**支持的流程**

| 过程 | API 调用 | 描述 | 进步 |
| --- | --- | --- | --- |
| 远程桌面连接 | `**CredUnPackAuthenticationBufferW**` | 这将挂钩到 mstsc，应该给你用户名，密码和远程 ip | 完成的 |
| runas | `**CreateProcessWithLogonW**` | 这将挂钩到 runas，应该给你用户名，密码和域名 | 完成的 |
| powershell | `**CreateProcessWithLogonW**` | 这将挂钩到 powershell，并在用户输入不同的凭据时为您提供命令输出。例如**–`Start-Process cmd -Credential X`** | 完成的 |
| 煤矿管理局 | `**RtlInitUnicodeStringEx**` | 这应该挂钩到 cmd，然后将能够过滤关键字，如:PsExec，密码等.. | 进行中–崩溃 cmd idk 为什么 |
| mobaxterm(mobaxterm) | `**CharUpperBuffA**` | 这将挂钩到 MobaXterm，并应该给你 SSH 和 RDP 登录的凭证 | 进行中——这是一个 32 位进程的问题，并且 [Fody](https://github.com/Fody/Costura) 不工作。**作为一种变通方法，你可以将项目编译为 x86，它会工作得很好** |
| 浏览器(UAC 提示) | `**CredUnPackAuthenticationBufferW**` | 这将挂钩到资源管理器，并应该给你用户名，密码和域名从 UAC 提示 | 进行中——UAC 表示拒绝访问可能是完整性等级问题 |

[**Download**](https://github.com/IlanKalendarov/SharpHook)