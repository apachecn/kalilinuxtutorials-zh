# SharpSpray : Active Directory 密码喷射工具。自动获取用户列表并避免潜在的锁定

> 原文：<https://kalilinuxtutorials.com/sharpspray/>

[![](img/dbe342581ee9427b2d661f1d5c6e20a2.png)](https://1.bp.blogspot.com/-Wm1ZcPBd-tk/YVSSHZFnSMI/AAAAAAAAK_A/D8q5X86UYy8UFbNv94rTHsOy2JpmaJgcwCLcBGAsYHQ/s679/images%2B%25281%2529.png)

**SharpSpray** 是一个具有增强和额外功能的域密码 Spray 的 C#端口。该工具使用 LDAP 协议与域 active directory 服务进行通信。

**特色**

*   可以在域上下文内外操作。
*   从喷洒中排除域禁用帐户。
*   自动从 Active directory 收集域用户。
*   通过在一次锁定尝试中排除帐户来避免潜在的锁定。
*   通过自动收集域锁定观察窗口设置来避免潜在的锁定。
*   与域细粒度密码策略兼容。
*   为用户定制 LDAP 过滤器，例如(description= *admin* )
*   每次身份验证尝试之间的延迟秒数。
*   每次身份验证尝试之间的抖动。
*   支持单个密码或密码列表。
*   单一文件控制台应用程序。

**用法**

**命令行参数**

**SharpSpray.exe–帮助
-v，–详细显示详细消息。
-u(可选)用户名列表文件路径。如果未指定，这将自动从活动目录中获取
。
-p 将用于执行密码喷洒的单个密码。
-k，–pl(可选)密码列表文件路径。
-d(可选)指定一个域名。
-m 如果从位于域上下文之外的主机进行喷射，请使用此选项。
-q，–选中选项“m”OutsideDomain 时需要 DC-IP
-x 尝试从用户列表中排除禁用的帐户
(选项-m 不支持)
-z 在 1 次尝试内排除帐户
锁定(选项-m 不支持)
-f 用户自定义 LDAP 过滤器，例如，"(description =*admin*)"
-o 输出结果的文件。
-w 不中继域锁定观察窗口设置，使用此特定值。(默认 32 分钟)
-s(可选)每次身份验证尝试之间的延迟秒数。
-j(可选)以秒为单位的抖动。
–强制启动，不要求确认。
–Get-users-list 从活动目录中获取域用户列表。
–show-examples 从活动目录中获取域用户列表。
–Show-args 显示命令行参数
–帮助显示** **该帮助屏幕。**

**用法举例**

**SharpSpray.exe-v-x-z–pl password . txt
SharpSpray.exe-x-z-u users . txt–pl PS swd . txt
SharpSpray.exe-x-z-u users . txt-p Passw0rd！
SharpSpray.exe-x-z-s 3-j 1-u users . txt-k PS swd . txt-o spreaded . txt
SharpSpray.exe-w 32-m-d DC-1 . local–DC-IP 10 . 10 . 20 . 20-u users . txt–pl PS swd . txt
SharpSpray.exe-w 32-s 3-j 1-m-d DC-1 . local–DC-IP 10 . 10 . 20 . 20-u users . txt–pl\ sharps pray . exe–get-users-list | Out-File-Encoding ascii users . txt**

**仅从活动目录中获取用户列表**

以下命令将获取域用户并将列表打印到控制台。

**SharpSpray.exe-x-z–获取用户列表
-x:从用户列表中排除禁用的帐户。
-z:排除 1 次锁定尝试内的帐户。**

[**Download**](https://github.com/iomoath/SharpSpray)