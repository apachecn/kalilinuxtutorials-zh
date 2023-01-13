# 诺斯费拉图:Lsass NTLM 认证后门

> 原文：<https://kalilinuxtutorials.com/nosferatu/>

[![](img/3662a0e7b3d0f2e87a84e0257dc6d0c0.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh4qOaCRfY1eSY-bBUMeM88juFR-_ebXvMRiBtGpcO6me1wqqTZwnoXGX_YiSBYmzaMDd-om2mY-Pjq74FzWNrWHHmeYLernnsc9vo43BZTZzm0zt7fVOYwvLgFfdXgVGDJL0SnfglMTnN8XK8paRKMGD6RbMJ3nqrba6Pxgi5gYaMC_e4-RgC4O3NO=s728)

**诺斯费拉图**是 Lsass NTLM 认证后门

**工作原理**

首先，DLL 被注入到`**lsass.exe**`进程中，并将开始挂钩认证 WinAPI 调用。目标功能为`**MsvpPasswordValidate()**`，位于`**NtlmShared.dll**`。为了不被检测到，被挂钩的函数将调用原始函数，并允许正常的身份验证流程。只有在发现认证失败后，钩子才会将实际的 NTLM 散列与后门散列交换出来进行比较。

**用法**

诺斯费拉图必须编译成 64 位 DLL。必须使用具有 SeDebugPrivilege 的 DLL 注入器来注入它。

![](img/18b1cd34035e141e8b92dd4ec1e69871.png)

您可以看到它是使用 Procexp 加载的:

![](img/19515c946f415e4057bca2232a2fefaa.png)

使用 Impacket 的登录示例:

![](img/5cc7b3a0c863ed5684e23463613d7d86.png)[**Download**](https://github.com/kindtime/nosferatu)