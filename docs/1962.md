# WFH : Windows 功能猎人 2021

> 原文：<https://kalilinuxtutorials.com/wfh/>

[![WFH : Windows Feature Hunter](img/95cd4084deb66efa835725f13d59f9e6.png "WFH : Windows Feature Hunter")](https://1.bp.blogspot.com/-zfF6tM6xLU8/YOppZZGVGOI/AAAAAAAAJ80/bozMEwh1wvsIoviqbe_cffW6cds0jusHgCLcBGAsYHQ/s1035/7_Qdndix2CQKI-C1oV5ASBUY6T8P5E9X2BofAUScOls.png)

**Windows Feature Hunter(WFH)**是一个概念验证 python 脚本，它使用 Frida(一个动态工具套件)来帮助识别 Windows 可执行文件中的常见“漏洞”或“功能”。WFH 目前有能力大规模自动识别潜在的动态链接库(DLL)侧加载和组件对象模型(COM)劫持机会。

DLL 侧加载利用 Windows 并行(WinSXS)程序集从并行(SXS)列表中加载恶意 DLL。COM 劫持允许对手通过劫持 COM 引用和关系来插入可代替合法软件执行的恶意代码。WFH 将打印潜在漏洞，并编写一个包含目标 Windows 可执行文件中潜在漏洞的 CSV 文件。

**安装**

**pip install-r requirements . txt**

**帮助**

PS C:\Tools\WFH > python。\wfh.py -h
用法:wfh.py [-h] -t T [T …] -m {dll，com} [-v] [-timeout 超时]
Windows 功能猎人
可选参数:
-h，–帮助显示此帮助消息并退出
-t T [T …]，-targets T [T …]
目标 Windows 可执行文件列表
-m {dll，com}，-mode {dll，com}
潜在可识别的漏洞【T9 -Frida instrumentation 的详细输出
-time out Frida instrumentation 的超时超时值
示例用法
注意:建议将目标二进制文件复制到与 wfh 相同的目录中，用于标识 DLL 侧加载
DLL 侧加载标识(Single):python wfh . py-t . \ mspaint . exe-m DLL
DLL 侧加载标识(Verbose):python wfh . py-t . \ mspaint . exe-m DLL-v
DLL 侧加载标识(超时 30s \charmap.exe -m dll
COM 劫持识别(Single):python wfh . py-t " C:\ Program Files \ Internet Explorer \ ie xplore . exe "-m COM
COM 劫持识别(Verbose):python wfh . py-t " C:\ Program Files \ Internet Explorer \ ie xplore . exe "-m COM-v
COM 劫持识别(超时 60s):python wfh . py-t " C:\ Program Files \ Internet Explorer \ ie xplore . exe "-m COM-COM

**用途**

**DLL 侧向加载识别**

首先，您需要将想要分析的二进制文件复制到与 wfh 相同的目录中

**PS C:\Tools\WFH >复制 C:\ Windows \ System32 \ ms paint . exe。
PS C:\Tools\WFH >复制 C:\ Windows \ System32 \ charmap . exe。
PS C:\Tools\WFH > dir
目录:C:\Tools\WFH
模式 LastWriteTime 长度名称
————————————
d——5/14/2021 下午 2:12。2021 年 5 月 6 日下午 2 点 39 分。gitignore
-a—- 12/7/2019 凌晨 2:09 198656 charmap.exe
-a—-5/18/2021 上午 7:39 6603 loadlibrary . js
-a—-4/7/2021 下午 12:48 988160 mspaint.exe
-a—-5/18/2021 上午 7:53 8705 readme . MD
-a**

现在，您可以对二进制文件运行 wfh 来识别 dll 侧加载机会

PS C:\Tools\WFH > python。\wfh.py -t * -m dll
运行 Frida 对抗 charmap.exe
[+]潜在 DllMain 侧加载:LoadLibraryW，LPCWSTR:MSFTEDIT.dll
[+]潜在 DllMain 侧加载:LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE
[ *]将原始 Frida 检测写入 charmap.exe-raw.log [* ]将潜在 DLL 侧加载写入 charmap.exe-sideload.log
运行 Frida 对抗 mspaint.exe【T8 LPCSTR: GdiplusStartup
[+]潜在的 DllMain 侧加载:LoadLibraryW，LPCWSTR:MSFTEDIT.dll
[+]潜在的 DllMain 侧加载:LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE
[ *]将原始 Frida 检测写入 mspaint.exe-raw.log [* ]将潜在的 DLL 侧加载写入 ms paint . exe-side load . log
[*]将 DLL 结果写入 dll_results。 \dll_results.csv
可执行文件，WinAPI，dll，entry point/WinAPI Args
charmap . exe，LoadLibraryW，LPCWSTR:MSFTEDIT.DLL
charmap . exe，LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE
mspaint.exe，LoadLibraryExW，LPCWSTR:gdiplus.dll，dwFlags : NONE
mspaint.exe，GetProcAddress，hModule : C:\WINDOWS\WinSxS\amd

如果您喜欢更详细的输出，您可以使用“-v”来查看来自 Frida 检测 Windows API 调用的每条消息。您还可以在原始日志文件中查看此输出。

PS C:\Tools\WFH > python。\wfh.py -t * -m dll -v
运行弗里达对阵 charmap.exe
{ ' type ':' send '，' payload': 'LoadLibraryW，LPCWSTR: MSFTEDIT。DLL'}
{'type': 'send '，' payload': 'LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE'}
[+]潜在的 DllMain 侧加载:LoadLibraryW，LPCWSTR:MSFTEDIT.DLL
[+]潜在的 DllMain 侧加载:LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE
[ *]将原始的 Frida 检测写入 charmap.exe-raw.log [* ]将潜在的 DLL 侧加载到 charmap . exe-中 DLL'}
{'type': 'send '，' payload': 'LoadLibraryExW，LPCWSTR:MSFTEDIT.DLL，dwFlags : NONE'}
[+]潜在的 DllMain 侧装:LoadLibraryExW，LPCWSTR:gdiplus.dll，dwFlags : NONE
[-]潜在的 DllExport 侧装:GetProcAddress，hModule:C:\ WINDOWS \ WinSxS \ amd64 _ Microsoft . WINDOWS . gdiplus _ 6595 b 64144 cf1 df _ 1.1

**COM 劫持识别**

PS C:\Tools\WFH > python。\ wfh . py-t " C:\ Program Files \ Internet Explorer \ ie xplore . exe "-m com
针对 C:\ Program Files \ Internet Explorer \ ie xplore . exe
[+]潜在的 COM 劫持:Path:HKEY _ LOCAL _ MACHINE \ Software \ Classes \ CLSID { 0 E5 aae 11-A475-4c 5b-AB00-c66de 400274 e } \ inprocserver 32，lpValueName : null，Type : REG_EXPAND_SZ，Value:% 1Storage.dll
[+]潜在的 COM 劫持:Path:HKEY _ class _ ROOT \ CLSID { 1fd 49718-1d 00-4b 19-AF5F-070 af 6 D5 d 4c } \ in proc server 32，lpValueName : null，Type : REG_SZ，Value:C:\ Program Files(x86)\微软\ Edge \ Application \ 90 . 0 . 818 . 62 \ BHO \ ie _ to _ Edge _ bho _ 64 . dll
[*]写 raw Frida\ ie xplore . exe-raw . log[*]正在将潜在的 COM 劫持写入。\ ie xplore . exe-com jacking . log
[*]将 dll 结果写入 com jacking _ results . CSV

**用例**

**原生 Windows 签名二进制文件**

将所有本机 Windows 签名二进制文件复制到 wfh 目录

**Get-child item c:\-File | ForEach-Object { if($ _-match '。+?{Get-AuthenticodeSignature $_。全名} } |其中{$_。iso binary } | ForEach-Object { Copy-Item $ _。路径。}**

寻找 DLL 侧加载的机会

**python wfh.py -t * -m dll**

寻找劫持通讯器的机会

**python wfh.py -t * -m com**

[**Download**](https://github.com/ConsciousHacker/WFH)