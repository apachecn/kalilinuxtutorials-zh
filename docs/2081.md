# PEzor:开源外壳代码和 PE 打包器

> 原文：<https://kalilinuxtutorials.com/pezor/>

[![](img/8ccc987443e9d21fe2f301b4a900950d.png)](https://1.bp.blogspot.com/-6CkljDEa9og/YTGfTV0MboI/AAAAAAAAKpw/FSSfejfAPSkOffA53x7_wabYr6S-zYEtACLcBGAsYHQ/s728/52384994.png)

PEzor 是一个开源的外壳代码和 PE 打包器。

**安装**

`**install.sh**`设计用于 Kali Linux 发行版。

**$ git 克隆 https://github.com/phra/PEzor.git
$ CD PEzor
$ sudo bash install . sh
$ bash PEzor . sh-h**

**从 v2.x.x 升级**

必须更新变量`**PATH**`才能使用 Donut 的特定提交！检查更新的`**install.sh**`脚本。

**用法**

*   `**PEzor -h**`
*   `**PEzor <EXECUTABLE> [donut args...]**`
*   `**PEzor <SHELLCODE>**`

## `**PEzor help**`

显示 PEzor 的帮助

**用法
$ PEzor 帮助**

## `**PEzor <EXECUTABLE>**`

将提供的可执行文件打包成一个新的

**用法
$ PEzor[OPTIONS…][donut args…]
# PEzor[OPTIONS…][donut args…]
选项
-h 显示用法和退出
-32 强制 32 位可执行文件
-64 强制 64 位可执行文件
-调试生成调试版本
-脱钩用户-登陆挂钩移除
-反调试添加反调试检查
-系统调用使用原始系统调用[仅限 64 位文本部分，而不是。数据
-rx 为外壳代码分配 rx 内存
-在同一线程中自行执行外壳代码
-SDK =指定的版本使用。NET Framework 版本(2、4、4.5(默认))
-sleep=N 在解包外壳代码前休眠 N 秒
-format=FORMAT 输出指定格式的结果(exe、dll、reflective-dll、service-exe、service-dll、dotnet、dotnet-createsection、dot NET-pinvoke)
【donut args…】可执行文件打包后，可以传递额外的 Donut args， 如-z 2
例
# 64 位(自注入 RWX)
$ pezor . sh-unhook-anti debug-text-self-sleep = 120 mimikatz/x64/mimikatz . exe-z 2-p ' " log c:\ users \ public \ Mimi . out " " token::whoami " " exit " '
# 64 位(自注入 RX)
$ pezor . sh-unhook-anti debug
$ pezor . sh-format = BOF mimikatz/x64/mimikatz . exe-z 2-p ' " log c:\ users \ public \ Mimi . out " " token::whoami " " exit " '
# 64 位(信标对象文件 w/clean up)
$ pezor . sh-format = BOF-clean up mimikatz/x64/mimikatz . exe-z 2-p ' " log c:\ users \ public \ Mimi . out " " token::whoami
$ pezor . sh-format = service-dll mimikatz/x64/mimikatz . exe-z 2-p ' " log c:\ users \ public \ Mimi . out " " token::whoami " " exit " '
# 64 位(dot net)
$ pezor . sh-format = dot net-sleep = 120 mimikatz/x64/mimikatz . exe-z 2-p ' " log c:\ users \ public \ Mimi . out " " token 32 位(Win32 API:VirtualAlloc/WriteMemoryProcess/CreateRemoteThread)
$ pezor . sh-SGN-unhook-anti debug-text-sleep = 120 mimikatz/Win32/mimikatz . exe-z 2
# 32 位(Win32 API:VirtualAlloc/WriteMemoryProcess/CreateRemoteThread)以及甜甜圈的参数
$ pezor . sh-SGN-unhook-anti debug-text-sleep = 1**

## `**PEzor <SHELLCODE>**`

将提供的外壳代码打包成可执行文件

**用法
$ PEzor < -32|-64 >【选项…】
选项
-h 显示用法并退出
-32 强制 32 位可执行文件
-64 强制 64 位可执行文件
-调试生成调试版本
-脱钩用户-登陆挂钩移除
-反调试添加反调试检查
-系统调用使用原始系统调用[仅限 64 位][仅限 Windows 10]
文本部分，而不是。数据
-rx 为 shellcode 分配 rx 内存
-在同一个线程中自行执行 shellcode【需要 RX shellcode，与-sgn 不兼容】
-sleep=N 在解包 shellcode 之前休眠 N 秒
-format=FORMAT 输出指定格式的结果(exe、dll、reflective-dll、service-exe、service-dll、dotnet、dotnet-createsection、 dotnet-pinvoke)
示例
# 64 位(自注入 RWX)
$ pezor . sh shell code . bin
# 64 位(自注入 RX)
$ pezor . sh-unhook-anti debug-text-self-RX-sleep = 120 shell code . bin
# 64 位(自注入)
$ pezor . sh-unhook-anti debug-text-self
$ pezor . sh-format = BOF-clean up shellcode . bin
# 64 位(反射 dll)
$ pezor . sh-format =反射 dll shellcode.bin
# 64 位(service exe)
$ pezor . sh-format = service-exe shellcode . bin
# 64 位(service dll)
$ pezor . sh-format = service-dll shellcode . bin**

[**Download**](https://github.com/phra/PEzor)