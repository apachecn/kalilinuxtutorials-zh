# go-Shellcode:Windows 外壳代码运行程序和支持实用程序的存储库

> 原文：<https://kalilinuxtutorials.com/go-shellcode/>

[![RedGhost :  Linux Post Exploitation Framework Designed To Assist Red Teams In Gaining Persistence, Reconnaissance & Leaving No Trace](img/cd1f9d3bd469be653faf4a8d77bbc6cf.png "RedGhost :  Linux Post Exploitation Framework Designed To Assist Red Teams In Gaining Persistence, Reconnaissance & Leaving No Trace")](https://1.bp.blogspot.com/-1yLc5idIQ8I/XS_nnJvqyuI/AAAAAAAABZY/2awztfABrBIzKgblOYmi5s7gWtXZeJvpACLcBGAs/s1600/RedGhost.PNG)

`**Go-Shellcode**`是 Windows 外壳代码运行程序和支持实用程序的存储库。应用程序使用各种 API 调用或技术加载并执行外壳代码。

可用的外壳代码运行程序包括:

**人造纤维**

该应用程序利用来自`**Kernel32.dll**`的 Windows CreateFiber 函数在该应用程序的进程中执行外壳代码。当您想要避免远程进程注入和想要避免调用`**CreateThread**`时，这是非常有用的。这个应用程序**没有**利用`**golang.org/x/sys/windows**`包中的功能。最显著的区别是，这个应用程序自己加载所有必需的 dll 和过程，并使用过程的 Call()函数。

**注意:**我还没有想出退出进程的方法，你必须手动终止它。

可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateFiber.exe .\cmd\CreateFiber\main.go**`

**创建流程**

这个应用程序利用了来自**T0 的 Windows CreateProcess 函数。**进程被创建为挂起状态，更新`**IMAGE_OPTIONAL_HEADER**`结构中的 AddressOfEntryPoint 以执行 childprocess 中的 shellcode，然后进程恢复。这是一种进程空洞化，但是现有的 pe 是**而不是**未映射的，并且 ThreadContext 是**而不是**更新的。提供的外壳代码体系结构(即 x86 或 x64)必须与子进程的体系结构相匹配。

可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateProcess.exe .\cmd\CreateProcess\main.go**`

**CreateProcessWithPipe**

该应用程序利用了来自`Kernel32.dll`的 Windows CreateProcess 函数。该流程在挂起状态下创建，`**IMAGE_OPTIONAL_HEADER**`结构中的 AddressOfEntryPoint 被更新以执行 childprocess 中的 shell 代码，然后该流程被恢复。这是一种进程空洞化，但是现有的 pe 是**而不是**未映射的，并且 ThreadContext 是**而不是**更新的。提供的外壳代码体系结构(即 x86 或 x64)必须与子进程的体系结构相匹配。

该应用程序不同于 CreateProcess，因为它将收集子进程中写入 **STDOUT** 或 **STDERR** 的任何数据，并将其返回给父进程。通过使用 CreatePipe 函数创建一个匿名管道来收集数据，父进程和子进程通过该管道进行通信。当使用 Donut 之类的工具在子进程中以外壳代码的形式执行. NET 程序集并检索所执行程序的输出时，这是非常有用的。以下命令可用于生成与位置无关的外壳代码，以使用 Donut v0.9.3 运行安全带:

`**.\donut.exe -o donut_v0.9.3_Seatbelt.bin -x 2 -c Seatbelt.Program -m Main -p "ARPTable" Seatbelt.exe**`

可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateProcessWithPipe.exe .\cmd\CreateProcessWithPipe\main.go**`

**创建远程线程**

该应用程序利用来自`**Kernel32.dll**`的 Windows CreateRemoteThread 函数在远程进程中执行 shellocde。应用程序要求要注入的目标进程已经在运行。可以在运行时使用`**-pid**`命令行标志提供目标进程标识符(PID)用于测试。通过将`**0**`替换为您的目标 PID，在以下代码行中对 PID 进行硬编码以供操作使用:

`**pid := flag.Int("pid", 0, "Process ID to inject shellcode into")**`

这个应用程序利用了`**golang.org/x/sys/windows**`包中的函数，在可行的情况下，比如`**windows.OpenProcess()**`。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateRemoteThread.exe .\cmd\CreateRemoteThread\main.go**`

**crearemotethreadnative**

该应用程序利用来自`**Kernel32.dll**`的 Windows CreateRemoteThread 函数在远程进程中执行 shellocde。应用程序要求要注入的目标进程已经在运行。可以在运行时使用`**-pid**`命令行标志提供目标进程标识符(PID)用于测试。通过将`**0**`替换为您的目标 PID，在以下代码行中对 PID 进行硬编码以供操作使用:

`**pid := flag.Int("pid", 0, "Process ID to inject shellcode into")**`

这个应用程序**没有**利用`**golang.org/x/sys/windows**`包中的函数。最显著的区别是，这个应用程序自己加载所有必需的 dll 和过程，并使用过程的 Call()函数。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateRemoteThreadNative.exe .\cmd\CreateRemoteThreadNative\main.go**`

**创建线程**

该应用程序利用来自`**Kernel32.dll**`的 Windows CreateThread 函数在该应用程序的进程中执行外壳代码。当您想要避免远程进程注入时，这很有用。这个应用程序在可行的情况下利用了`**golang.org/x/sys/windows**`包中的功能，比如 windows。VirtualAlloc()`。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateThread.exe .\cmd\CreateThread\main.go**`

**CreateThreadNative**

该应用程序利用来自`**Kernel32.dll**`的 Windows CreateThread 函数在该应用程序的进程中执行外壳代码。当您想要避免远程进程注入时，这很有用。这个应用程序**没有**利用`**golang.org/x/sys/windows**`包中的功能。最显著的区别是，这个应用程序自己加载所有必需的 dll 和过程，并使用过程的 Call()函数。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o CreateThreadNative.exe .\cmd\CreateThreadNative\main.go**`

**早鸟**

应用程序利用 Windows CreateProcess 函数创建一个处于挂起状态的进程。一旦子进程被挂起，Windows QueueUserAPC 函数用于将指向分配外壳代码的 UserAPC 添加到子进程中。接下来，调用 ResumeThread，它随后调用未记录的 NtTestAlert 函数，该函数将执行创建的 UserAPC，并依次执行 shell 代码。这很有用，因为外壳代码将在 AV/EDR 能够挂钩函数以支持检测之前执行。参考新发现的“早期鸟”代码注入技术。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**export GOOS=windows GOARCH=amd64;go build -o goEarlyBird.exe cmd\EarlyBird\main.go**`

**【etpcreateetthread】**

该应用程序利用来自`**ntdll.dll**`的 Windows EtwpCreateEtwThread 函数在该应用程序的进程中执行外壳代码。世界的原创作品。当您想要避免远程进程注入时，这很有用。这个应用程序**没有**利用`**golang.org/x/sys/windows**`包中的功能。最显著的区别是，这个应用程序自己加载所有必需的 dll 和过程，并使用过程的 Call()函数。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o EtwpCreateEtwThread.exe .\cmd\EtwpCreateEtwThread\main.go**`

**NtQueueApcThreadEx(本地)**

此应用程序使用未记录的 NtQueueApcThreadEx 在当前进程的当前线程中创建一个“特殊用户 APC”来执行外壳代码。因为外壳代码是在当前进程中加载和执行的，所以是“本地”的。同样的技术也可以用于远程进程。*注意:*这只适用于 Windows 7 或更高版本。参考 APC 系列:用户 APC API。

`**export GOOS=windows GOARCH=amd64;go build -o goNtQueueApcThreadEx-Local.exe cmd\NtQueueApcThreadEx-Local\main.go**`

**【RTL create user thread】**

该应用程序利用来自`**ntdll.dll**`的 Windows RtlCreateUserThread 函数在远程进程中执行 shellocde。应用程序要求要注入的目标进程已经在运行。可以在运行时使用`**-pid**`命令行标志提供目标进程标识符(PID)用于测试。通过将`0`替换为您的目标 PID，在以下代码行中对 PID 进行硬编码以供操作使用:

`**pid := flag.Int("pid", 0, "Process ID to inject shellcode into")**`

这个应用程序**没有**利用`**golang.org/x/sys/windows**`包中的函数。最显著的区别是，这个应用程序自己加载所有必需的 dll 和过程，并使用过程的 Call()函数。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o RtlCreateUserThread.exe .\cmd\RtlCreateUserThread\main.go**`

**系统调用**

该应用程序通过对外壳代码的入口点进行系统调用来执行当前正在运行的进程中的外壳代码。这个应用程序**不**利用 **`golang.org/x/sys/windows`** 包中的函数。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o Syscall.exe .\cmd\Syscall\main.go**`

**UuidFromStringA**

该应用程序利用 Windows UuidFromStringA 函数将外壳代码加载到内存地址，然后调用 EnumSystemLocalesA 函数来执行外壳代码。这种加载和执行外壳代码的方法源自 nccgroup 的 RIFT:analyzing a Lazarus 外壳代码执行方法。对于这个应用程序，内存是在堆上分配的，它不使用 VirtualAlloc。可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o UuidFromString.exe .\cmd\UuidFromString\main.go**`

**ShellcodeUtils**

该应用程序用于转换外壳代码二进制文件。程序依赖于输入文件是一个二进制文件(。bin)，它包含外壳代码的十六进制字节。ShellcodeUtils 可以对你的输入文件进行 base64 编码，也可以进行异或、RC4 或 AES256-GCM 加密。这些工具也可以用来解密文件。

ShellcodeUtils 帮助菜单:

**-base64
Base64 编码输出。可以加密或不加密使用
-i 字符串
二进制文件的输入文件路径
-密钥字符串
加密密钥
-模式字符串
对输入文件执行的操作模式[加密，解密](default)
-nonce 字符串
Nonce，以十六进制表示，用于解密 AES256 输入文件。仅在解密期间使用
-o 字符串
输出文件路径
-salt 字符串
Salt，十六进制，用于通过 Argon2 生成 AES256 32 字节密钥。仅在解密期间使用
-type string
要使用的加密类型【xor、aes256、rc4、null】
-v 启用详细输出**

仅 Base64 编码输入文件并将其保存为文本文件的示例:

**PS C:\Users\bob >。\ shellcodeutils . exe-I C:\ Users \ bob \ calc . bin-o C:\ Users \ bob \ calc . b64 . txt-base64-v
[-]输出目录:C:\ Users \ bob \
[-]输出文件名:calc . b64 . txt
[-]文件内容(十六进制):505152535657556 a605 a 6863616 C 6354594883 EC 28655**

示例使用密钥`**Sh3!1z**`对输入文件进行 XOR 加密，并对输出进行 base64 编码:

**PS C:\Users\bob >。\ shellcodeutils . exe-I C:\ Users \ bob \ calc . bin-o C:\ Users \ bob \ calc . xor . b64 . txt-mode encrypt-type xor-key Sh3！1z-v
[-]输出目录:C:\ Users \ bob \
[-]输出文件名:calc . XOR . b64 . txt
[-]文件内容(十六进制):505152535657556 a 605 a 6863616 C 6354594883 EC 2865488 b 32488 b 7618488 b 761048 ad 488 b 30488 b 7 e 3003551z
[+]输出(十六进制):
03396172672d 0602537 b 5919320450756832d 0841 b 4479 f 16120 b 8572932d 81e 23699 C 32d 8587 baa 4 f 4a 503 f 0 fa a6 d6d 7 be 3473 e 11325296 b 8752 e 5 CD f1 f 36 BC 2851 C。**

示例 AES256-GCM 使用密码`**Sh3!1z**`加密输入文件，不对输出进行 base64 编码:

**PS C:\Users\bob >。\ shellcodeutils . exe-I C:\ Users \ bob \ calc . bin-o C:\ Users \ bob \ calc . AES . bin-mode encrypt-type AES 256-key Sh3！1z-v
[-]输出目录:C:\ Users \ bob \
[-]输出文件名:calc . AES . bin
[-]文件内容(十六进制):505152535657556 a605 a 6863616 C 6354594883 EC 2865488 b 32488 b 7618488 ad 488 b 30488 b 303573 C 881z(十六进制):096 a40 f1 AEF 38 DD 9 b5 d 63284 ACC 19727 C 4420 DD 98 f 21 ea 052112 bef 63 EB 7d 94 a
[+]AES 256 nonce(十六进制):13802153 C4 B2 FB 6 a3 e 545 ff 4
[+]Output(十六进制):
44a 974233 e 37 b 460 DC 2181 b 16846 f 265 e**

AES256 需要一个 32 字节的密钥。该程序使用 Argon2 ID 算法获取由`-key`输入参数提供的密码，并在使用随机生成的 salt 时导出一个 32 字节的密钥。您将需要与 Argon2 算法使用的相同输入密码和 salt，以及与 AES256 算法使用的相同 nonce 来成功解密该文件。或者，解密函数*可以*更新为只使用 32 字节的 Argon2 密钥，而不是输入密码和 salt。

**注:**由操作员决定是只使用生成的 Argon2 密钥，还是使用用于生成密码的密码和 salt。

示例 AES256 解密输入文件:

**PS C:\Users\bob >。\ shellcodeutils . exe-I C:\ Users \ bob \ calc . AES . bin-o C:\ Users \ bob \ calc . AES . decrypted . bin-mode decrypt-type AES 256-key Sh3！1z-nonce 13802153 C4 b 2 FB 6 a3 e 545 ff 4-salt db 6126 D3 AC 640 f 8 AAA 67 CDA 74 b 8 cf 1d 2c 54513 db 7 BF 4 FBE 3422 D1 b 276 af 1367 e-v
[-]输出目录:C:\ Users \ bob \
[-]输出文件名:calc . AES . decrypted . bin【T3[-]文件内容(十六进制):44a 974233 e 37**

可以在 Windows 主机上从项目的根目录使用以下命令编译该应用程序:

`**set GOOS=windows GOARCH=amd64;go build -o ShellcodeUtils.exe .\cmd\ShellcodeUtils\main.go**`