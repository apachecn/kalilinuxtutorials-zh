# SharpRDP:用于认证命令执行的 RDP 应用程序

> 原文：<https://kalilinuxtutorials.com/sharprdp/>

[![SharpRDP : RDP Application For Authenticated Command Execution](img/e603d68e23bb718782e790cbf235807c.png "SharpRDP : RDP Application For Authenticated Command Execution")](https://1.bp.blogspot.com/-ByjfQFbqgQc/XmaIaeWX4lI/AAAAAAAAFWM/9eQQMCvPKsIqw7voZhjhQLmhJKIhR-LegCLcBGAsYHQ/s1600/SharpRDP%25281%2529.png)

SharpRDP 是一个远程桌面协议控制台应用程序，用于认证命令的执行。

**大楼**

若要编译，请在 Visual Studio 中打开该项目，然后生成以供发布。两个 dll 将输出到发布目录，您不需要它们，因为 dll 在程序集中。

如果您不想使用提供的 dll，您需要。NET SDK 来创建 AxMSTSCLib.dll DLL。要创建它，你需要在 mstscax.dll 的 SDK 上运行 aximp。 **`%<SDK dir>%\aximp.exe %windir%\system32\mstscax.dll`。**

项目需要引用这些 dll 来创建互操作 dll。您还需要用 Deflate 压缩 dll，并将它们命名为 AxInterop。MSTSCLib.dll.bin 和 Interop。MSTSCLib.dll.bin

**用途**

常规 RDP 连接和执行
SharpRDP.exe 计算机 name = target . domain command = " C:\ Temp \ file . exe "用户名=域\用户密码=密码

作为 cmd 或 powershell 的子进程的 Exec 程序
SharpRDP.exe 计算机 name = target . domain command = " C:\ Temp \ file . exe " username = domain \ user password = password exec = cmd

使用受限管理模式
SharpRDP.exe 计算机名=目标.域命令="C:\Temp\file.exe "

连接第一个主机驱动器
SharpRDP.exe 计算机 name = domain . target command = " \ ts client \ C \ Temp \ file . exe " username = domain \ user password = password connect drive = true

通过运行对话框提升的执行命令–当前被调试的
SharpRDP.exe 计算机 name = domain . target command = " C:\ Temp \ file . exe " username = domain \ user password = password elevated = winr

执行通过任务管理器提升的命令
SharpRDP.exe 计算机 name = domain . target command = " C:\ Temp \ file . exe \ " username = domain \ user password = password elevated = task mgr

添加网络级身份验证
SharpRDP.exe 计算机名称=域.目标命令="C:\Temp\file.exe\ "用户名=域\用户密码=密码 nla =真

请求接管登录会话
SharpRDP.exe 计算机 name = domain . target command = " C:\ Temp \ file . exe \ "用户名=域\用户密码=密码接管=真

如果在目标上启用了受限管理模式，则不要指定任何凭据，它将使用当前用户上下文。Can 信标中的`**PTH**`或`**make_token**`或 Windows 系统上的`**runas /netonly**`。

所有的执行都从 Windows 的运行对话框开始(Win+R)。将会有一个在`**HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU**`用您执行的命令创建的注册表项。如果你想删除它，你可以使用: [CleanRunMRU:获取或清除 RunMRU 值](https://github.com/0xthirteen/CleanRunMRU)

请记住，如果您执行一个像 msbuild 这样的程序(我肯定还有其他程序)，在进程运行时会弹出一个 cmd 窗口。如果你这样做了，最好的方法可能是迁移这个过程并删除原来的过程。

所需的 dll 被编译到程序集中，并使用应用程序域程序集解析事件。由于 dll 的大小，它们在运行时被压缩和解压缩(因此它们可以满足 beacon 的 1MB 大小限制)。

[**Download**](https://github.com/0xthirteen/SharpRDP)