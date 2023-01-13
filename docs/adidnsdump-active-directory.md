# Adidnsdump : Active Directory 集成 DNS 转储工具

> 原文：<https://kalilinuxtutorials.com/adidnsdump-active-directory/>

[![Adidnsdump : Active Directory Integrated DNS Dump Tool](img/2fc8c476ddde54feacc0569fa24d840b.png "Adidnsdump : Active Directory Integrated DNS Dump Tool")](https://4.bp.blogspot.com/-robQXoRFH24/XMy1VUXAH3I/AAAAAAAAAFc/lRBCZaYvnPMpZ8BopOb5J6R8FjM8_I7TQCLcBGAs/s1600/Active%2BDirectory.png)

**Adidnsdump** 工具是一个 Active Directory 集成的 DNS 转储工具，可由任何经过身份验证的用户使用。

默认情况下，Active Directory 中的任何用户都可以枚举域或林 DNS 区域中的所有 DNS 记录，类似于区域传送。

该工具支持枚举和导出区域中的所有 DNS 记录，用于内部网络的重新定位。

**安装和使用**

您可以通过 pip 安装该工具，或者从 git 安装该工具以获得最新版本:

git 克隆 https://github.com/dirkjanm/adidnsdump
CD adidnsdump
pip 安装。

**或**

**pip 安装 git+https://github . com/dirkjanm/adidnsdump # egg = adidnsdump**

**又读:[evillipy:用于创建恶意的 MS Office 文档](https://kalilinuxtutorials.com/evilclippy-malicious-ms-office-documents/)**

该工具需要**碰撞**和 **dnspython** 才能运行。虽然该工具适用于 Python 2 和 3，但 Python 3 支持要求您安装 impacket。

安装会将命令添加到您的**路径**中。如需帮助，请尝试**adidnsdump-h。**该工具既可以直接从网络使用，也可以通过 proxychains 植入使用。如果使用 proxychains，请确保指定了**–DNS-TCP**选项。

[Download](https://github.com/dirkjanm/adidnsdump)