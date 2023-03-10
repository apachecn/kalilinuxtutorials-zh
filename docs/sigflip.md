# SigFlip:一个修补验证码签名的 PE 文件的工具

> 原文：<https://kalilinuxtutorials.com/sigflip/>

[![](img/47b75a903dd54745e16e6c7bee15ef7e.png)](https://1.bp.blogspot.com/-hWYthRqSpFY/YTGqLnoX7jI/AAAAAAAAKqA/tHBUyECnkUoosjOYUi4mROtrvz_U7_r0gCLcBGAsYHQ/s728/38071830%2B%25281%2529.png)

**SigFlip** 是一款修补 authenticode 签名的 PE 文件(exe、dll、sys..等等)，换句话说，您可以通过嵌入数据(即外壳代码)来更改 PE 文件校验和/哈希，而不会破坏文件签名、完整性检查或 PE 文件功能。

SigInject 加密并将外壳代码注入到 PE 文件的[WIN_CERTIFICATE]证书表中，加密密钥被打印出来供基本的 BOF/C/C#加载程序(SigLoader)使用，SigInject 保存对修改后的 PE 文件的更改，并保持其签名和证书的有效性不变。

SigLoader 是一个基本的加载程序，它将 SigInject 创建的修改后的 PE 文件路径和解密密钥作为参数，然后提取和解密嵌入的外壳代码，以便与选择的外壳代码注入一起使用。

SigFlip 将检查 PE 哈希是否成功更改，并在端点针对这种常见的错误配置进行加固的情况下正常检查并退出。(查看“详细信息”部分)。

快速提示: SigFlip、SigInject 和 SigLoader 作为 BOF 脚本和。NET 程序集，唯一的区别是 SigInject 功能是作为 SigFlip (-i)的一部分实现的，以防您选择使用。NET 工件而不是 BOF。

**为什么？**

它可以主要用于持续、横向移动或代码/命令执行，并且可以帮助:

*   应用程序白名单会绕过，在不破坏签名的情况下更改 PE 文件哈希(msbuild.exe 用于 ex)。
*   绕过依赖特定 LOLBINs 哈希的 EDRs 进行恶意代码/命令执行检测。
*   使用不同的哈希加载签名的驱动程序，可能有助于规避任何 EDRs 使用预定义的哈希列表来监视常见的易受攻击的签名驱动程序。
*   将加密的外壳代码嵌入到签名的 PE 文件中，并使用您喜欢的 stager (sigloader)来解析、解密、加载和执行它。
*   端点安全供应商倾向于将签名的 PE 文件归类为良性文件，嵌入您的未签名代码(外壳代码..等等。)会使检测/标记变得有点困难。
*   绕过主要依赖默认 WinVerifyTrust 进行签名验证的端点安全供应商。
*   改进 OPSEC 并挑战仅依赖典型签名验证实用程序(如 signtool、sigcheck、Get-AuthenticodeSignature)的防御者..以验证 PE 文件的 authenticoode 签名。

**用法&举例**

**编译/编译**

本项目不提供预编译的 BOF，可以使用 Mingw-w64 对**进行编译。NET** 用 VS 或者 csc.exe 编译。NET 项目(SigFlip，SigLoader)，对于 **BOF** 检查步骤如下；

*   `➜ **i686-w64-mingw32-gcc -c sigflip.c -o sigflip.x86.o**`
*   `➜ **x86_64-w64-mingw32-gcc -c sigflip.c -o sigflip.x64.o**`
*   `➜ **x86_64-w64-mingw32-gcc -c SigLoader/sigloader.c -o sigloader.x64.o**`
*   `➜ **i686-w64-mingw32-gcc -c SigLoader/sigloader.c -o sigloader.x86.o**`

确保所有目标文件都与 sigflip.cna 位于同一目录，然后将 sigflip.cna 脚本加载到 cobalt strike。

**快速提示:**预编译的 BOF 已经过测试，并与 mingw-64 v8.0.0_3、**兼容，使用 mingw-64 > = v9 可能会工作，但可能会使主动信标崩溃**，请查看 https://github.com/med0x2e/SigFlip/issues/2 了解更多详细信息。

**钴击**

*   **执行-组装**
    *   `**execute-assembly SigFlip.exe -h**`
    *   `**execute-assembly SigLoader -h**`
*   **BOF**
    *   为了与 cobalt strike 一起使用，一旦加载 SigFlip.cna 脚本，将注册两个新命令；SigFlip 和 SigInject，然后如下使用；
        *   改变一个 PE 文件(DLL，EXE，SYS，OCX..不破坏签名或证书有效性的散列:
            *   `**SigFlip "<PE\_FILE\_PATH>" "<OUTPUT\_PE\_FILE\_PATH (with extension)>"**`
        *   SigInject:加密外壳代码并将其注入 PE 文件的[WIN_CERTIFICATE]证书表中，加密密钥被打印出来供基本 C/C#加载程序使用，并保持签名和证书的有效性不变:
            *   `**SigInject "<PE\_FILE\_PATH> <OUTPUT\_PE\_FILE\_PATH (with extension)>" "<SHELLCODE\_FILE>"**`
        *   SigLoader:从 SigInject 创建的 PE 文件中加载加密的外壳代码，然后使用 Early Bird queueuserapc 将 sc 生成/注入到牺牲进程中，外壳代码注入逻辑可以定制，也可以替换为任何其他代码注入技术:
            *   `**SigLoader <PE_FILE_PATH_WITH_SH> <DECRYPTION_KEY> <SPAWNTO_PROCESS_PATH> <PARENT_PROCESS_ID>**`
*   **例题**
    *   BOF:
        *   将随机数据注入 msbuild.exe(又名位翻转 msbuild . exe):
            *   `**SigFlip "C:\Windows\Microsoft.NET\Framework\v4.0.30319\msbuild.exe" "C:\lolbins\modified-msbuild.exe"**`
        *   将外壳代码注入 kernel32.dll(参数顺序不同&确保记下解密密钥):
            *   `**SigInject "C:\Windows\System32\kernel32.dll" "C:\random\modified-kernel32.dll" "C:\shellcode\cobaltstrike_or_msf_shellcode.bin"**`
            *   `**Sigloader "C:\random\modified-kernel32.dll" "DECRYPTION_KEY" "C:\Windows\System32\werfault.exe" 6300**`
    *   执行-汇编:
        *   将随机数据注入 msbuild.exe:
            *   `**execute-assembly SigFlip.exe -b C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe -o C:\Temp\MSBuild.exe**`
        *   将外壳代码注入 kernel32.dll(参数顺序不同&确保记下解密密钥):
            *   `**execute-assembly SigFlip.exe -i C:\Windows\System32\kernel32.dll -s C:\Temp\x86shellcode.bin -o C:\Temp\kernel32.dll -e TestSecretKey**`
            *   `**execute-assembly SigLoader.exe -f C:\Temp\modified-kernel32.dll -e TestSecretKey -pid 2354**`

**详情**

这是 APT#10 在多个活动或入侵设置中使用的一种已知技术。

**Authenticode 数字签名？**

Authenticode 是一种 Microsoft 代码签名技术，用于标识 Authenticode 签名软件的发行者。Authenticode 还验证软件自签名和发布以来未被篡改。

**它是如何工作的？**

Microsoft 主要依靠 Authenticode 签名格式来验证 PE 二进制文件的完整性和来源，根据 Authenticode 可移植可执行格式规范，Authenticode 签名可以“嵌入”在 Windows PE 文件中，位置由可选标头数据目录中的证书表条目指定。当 Authenticode 用于对 Windows PE 文件进行签名时，计算文件的 Authenticode 哈希值的算法会排除某些 PE 字段。当在文件中嵌入签名时，**签名过程可以修改这些字段，而不会影响文件的散列值**。这些字段如下:* *校验和、证书表 RVA、证书表大小和证书表的**属性**。属性证书表包含 PKCS #7 SignedData 结构，该结构包含 PE 文件的**哈希值**、由软件发行商的私钥创建的**签名**以及将软件发行商的签名密钥绑定到合法实体的 **X.509 v3 证书**。

通俗地说，我们可以在验证码散列计算中修改或嵌入数据到字段中，而不用担心破坏验证码签名和文件完整性检查。

关于此类排除字段的更多详细信息:

*   证书表 RVA 和大小:一个签名的 PE 文件可选头结构包含一组数据目录，包括安全目录**IMAGE _ DIRECTORY _ ENTRY _ SECURITY**ENTRY，它有两个字段， **RVA** 和**大小**。
    *   RVA:属性证书表的文件偏移量(不是内存偏移量)。
    *   大小:属性证书表大小。
*   属性证书表:封装了签名和证书的数据结构 **WIN_CERTIFICATE** ，具有以下字段:
    *   `**dwLength**`:证书表尺寸。
    *   `**wRevision**`:`**WIN_CERTIFICATE**`的“修订版”。
    *   `**wCertificateType**`:封装的证书数据的种类。
    *   `**bCertificate**`:实际证书数据。对于`**WIN_CERT_TYPE_PKCS_SIGNED_DATA**`，这是上面提到的 PKCS#7 `**SignedData**`结构(包含 PE 哈希值、签名和 x.509 证书)，这正是 SigFlip 嵌入 randm 随机数据或外壳代码的地方。

考虑到所有这些，现在 SifFlip 做了以下工作:

*   检查系统配置
*   加载 PE 文件和验证 PE 文件签名和计算 Sha1 哈希
*   获取“e_lfanew”偏移量(指向 PE 文件头-> IMAGE_NT_HEADERS)
*   从 IMAGE_NT_HEADERS 获取 IMAGE_OPTIONAL_HEADER
*   从 IMAGE_OPTIONAL_HEADER 获取 IMAGE_DATA_DIRECTORY
*   获取 IMAGE_DIRECTORY_ENTRY_SECURITY 字段，并检索属性证书表(WIN_CERTIFICATE)的 RVA 和大小。
*   通过用选择的额外字节(随机/外壳代码)填充证书表来修补 PE 文件 blob。
*   更新可选头-> IMAGE _ DIRECTORY _ ENTRY _ SECURITY 数据目录大小
*   更新 WIN_CERTIFICATE(证书表)dwLength
*   生成新的 PE 校验和并更新它。(可选报头校验和)
*   用新的大小保存最终的 PE。
*   验证修改的 PE 文件签名

第一步是确认系统是否配置错误，允许将外壳代码填充和注入到 authenticode 签名的 PE 文件中，因此需要执行以下健全性检查:

*   检查是否未安装 MS13-098 修复程序(KB2893294)，请记住**它可以安装，但注册表项未正确设置，这会使修补程序无用**
*   检查注册表项
    *   X86:
        *   检查注册表项“HKLM:\软件\ Microsoft \ Cryptography \ Wintrust \ Config”是否不可用
            *   ->如果可用，则检查“EnableCertPaddingCheck”注册表值是否不可用
    *   X64:
        *   检查注册表项“HKLM:\ Software \ wow 6432 node \ Microsoft \ Cryptography \ Wintrust \ Config”是否不可用
            *   ->如果可用，则检查“EnableCertPaddingCheck”注册表值是否不可用。

#### 当修改后的 PE 作为模块加载到自己的地址空间或者其他进程的地址空间时，为什么不能读取注入的数据？

Windows 加载程序不将证书数据加载到进程地址空间，这就是为什么您需要自定义加载程序来提取数据(如外壳代码)并使用它(例如:SigLoader)。这也应该解释了为什么**IMAGE _ DIRECTORY _ ENTRY _ SECURITY**data 目录条目 RVA 是文件偏移而不是典型的内存偏移。

[**Download**](https://github.com/med0x2e/SigFlip)