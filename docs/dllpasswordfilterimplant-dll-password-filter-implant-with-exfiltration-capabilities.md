# DLLPasswordFilterImplant:具有渗透功能的 DLL 密码过滤器植入

> 原文：<https://kalilinuxtutorials.com/dllpasswordfilterimplant-dll-password-filter-implant-with-exfiltration-capabilities/>

[![DLLPasswordFilterImplant : DLL Password Filter Implant With Exfiltration Capabilities](img/cd4128abec6042046298a13febe4aa04.png "DLLPasswordFilterImplant : DLL Password Filter Implant With Exfiltration Capabilities")](https://1.bp.blogspot.com/-urB9nCb59CQ/XlWOvVcUlLI/AAAAAAAAFG0/-MOrl0JAY6EBvQgtNwuBreQJTjZNuEzZgCLcBGAsYHQ/s1600/Password.png)

DLLPasswordFilterImplant 是一个定制的密码过滤器 DLL，允许捕获用户的凭证。域中的每个密码更改事件都会触发已注册的 DLL，以便在 Active Directory (AD)中成功更改用户名和新密码值之前对其进行解密。

有关密码过滤器的更多信息，请查阅 Microsoft 文档。

**安装**

1.  要在系统上安装密码过滤器，请执行以下操作:

*   为目标体系结构创建 DLL。对于 32 位系统，以 32 位编译；对于 64 位系统，以 64 位编译。
*   将 DLL 复制到 Windows 安装目录。(默认文件夹:\Windows\System32)
*   通过更新以下注册表项来注册密码过滤器:

**HKEY _ LOCAL _ MACHINE \ SYSTEM \ current Control set \ Control \ Lsa**

*   如果 **`Notification Packages`** 子项存在，则将 DLL 的名称(“DLLPasswordFilterImplant”如果您没有重命名它)添加到现有的值数据中。不要覆盖现有值。
    如果子项不存在，则创建它并将 DLL 的名称(如果没有重命名，则为“DLLPasswordFilterImplant ”)添加到值数据中。**注意:**在`**Notification Packages**`子项中添加 DLL 名称时，不要包括`.dll`扩展名。

*   配置用于加密凭据的公钥。

**KEY=key.pem
#生成一个 RSA 密钥并转储其公钥。保留私钥用于解密
OpenSSL genrsa-out $ KEY 2048

#准备 Windows 注册表项。
echo 'Windows 注册表编辑器 5.00 版'>addkey . reg
echo>>addkey . reg
echo '[HKEY _ LOCAL _ MACHINE \ SYSTEM \ current Control set \ Control \ Lsa]'>>addkey . reg

#如果 python2 不存在，则使用 python。
echo " key = hex:$(OpenSSL RSA-in $ key-pubout | sed-e '/^-/d' | base64-d | python 2-c ' import sys；打印(“，”。加入(["{:02x} "。format(ord(b))for b in sys . stdin . read()]))')">>addkey . reg**

*   然后可以运行`**addKey.reg**`文件将原始公钥添加到注册表中。请注意，由于消息填充，使用非对称加密会显著增加要泄漏的数据的大小。可能需要进行一些改进来减少数据开销。
*   重启系统[来源](https://msdn.microsoft.com/en-us/library/windows/desktop/ms721766(v=vs.85).aspx)

1.  要注册 DNS 过滤的密钥和域:

*   转到以下注册表项:

**HKEY _ LOCAL _ MACHINE \ SYSTEM \ current Control set \ Control \ Lsa**

*   创建一个名为“Domain”的字符串类型子项。在该子项的值中指定您的域。您的域必须以“.”开头。(示例值:" . yourdomain.com ")

**也读作-[Rabid:解码各种 BigIP Cookies 的工具](https://kalilinuxtutorials.com/rabid/)**

**解密**

加密的数据使用 OAEP 填充，可以按如下方式解密:

**#将拼接的十六进制字符串转换为原始字节。
xxd-r-p exfilied . hex>raw . bin
#使用私钥解密。
OpenSSL rsautl-decrypt-oaep-inkey $ KEY-in raw . bin-out decrypted . txt**

**卸载**

要完全删除系统的密码过滤器，请执行以下操作:

*   通过更新以下注册表项来注销密码筛选器:

**HKEY _ LOCAL _ MACHINE SYSTEM \ current Control set \ Control \ Lsa**

*   在 Notification Packages 子项中，删除现有值数据的 DLL 名称。不要删除其他现有值。
*   重启系统
*   在 Windows 安装目录(默认文件夹:\Windows\System32)中，找到密码过滤器 DLL(" dllpasswordfilterplant。DLL "如果你没有重命名它)并删除文件。

**DNS 过滤服务器**

在`**scripts/**`中提供了一个简单的 DNS 服务器来接收被过滤的数据。运行`**pip install -r scripts/requirement.txt**`，最好在虚拟环境下运行。然后为它提供一个. PEM 编码的私有密钥和可选的输出文件(默认为`**creds.txt**`)来输出凭证。

目前，DNS 服务器不支持并发密码更改，仅作为概念验证。为服务器增加健壮性的拉请求非常受欢迎。

**告诫**

*   删除植入需要首先禁用它，然后重新启动 Windows。

**兼容性**

工作于:

*   Windows 7 主机(x64)
*   Windows 10 主机(x64)
*   Windows Server 2008 DCs (x64)
*   Windows Server 2012 DCs (x64)
*   Windows Server 2016 DCs (x64)

密码过滤器仅在上面列出的系统上进行测试。

**调试**

这里有一些工具可以帮助你调试 DLL(如果需要的话):

*   [流程浏览器](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
*   [依赖行者](http://www.dependencywalker.com/)

[**Download**](https://github.com/GoSecure/DLLPasswordFilterImplant)