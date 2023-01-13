# FlashSploit:基于 ATtiny85 的 HID 攻击的利用框架

> 原文：<https://kalilinuxtutorials.com/flashsploit/>

[![FlashSploit : Exploitation Framework For ATtiny85 Based HID Attacks](img/2636a011d80613b5b5c245c68d3b2a21.png "FlashSploit : Exploitation Framework For ATtiny85 Based HID Attacks")](https://4.bp.blogspot.com/-rIsNo7VHIUA/XObJ3xkVbfI/AAAAAAAAAc8/P0SgWWlGQUkFBcg_GOoHocSTXUUxjPr2ACLcBGAs/s1600/Flashsploit-1%25281%2529.png)

**Flashsploit** 是一个利用 ATtiny85 HID 设备(如 Digispark USB 开发板)进行攻击的利用框架，Flashsploit 生成 Arduino IDE 兼容(。ino)脚本，然后在脚本需要时在 Metasploit-Framework 中启动一个侦听器，概括地说:使用自动化 msfconsole 自动生成脚本。

**窗户**

**数据泄露**

*   提取所有 WiFi 密码并上传一个 XML 到 SFTP 服务器| YouTube:

[![](img/953ae67ebc6068356de434623a0b25ad.png)](https://www.youtube.com/watch?v=N8vR69Qqz60)

*   提取目标系统的网络配置信息并上传到 SFTP 服务器| YouTube:

[![](img/efdc21e74a7024deed8ed5f1994b9971.png)](https://www.youtube.com/watch?v=I2loDe3Kqaw)

*   使用 Mimikatz 提取密码和其他重要信息，并上传到 SFTP 服务器| YouTube:

[![](img/aee49ea816082799956887af650dabfd.png)](https://www.youtube.com/watch?v=puxPviIoITo)

**亦读-[阴谋诡计核心:发现你的攻击面](https://kalilinuxtutorials.com/intrigue-core-external-attack/)**

**反向炮弹**

*   通过滥用 Microsoft HTML Apps (mshta)获得反向外壳| YouTube:

[![](img/0d334b9dc73f2ce268e8efde6eef5363.png)](https://www.youtube.com/watch?v=4DsEMGsZB94)

*   通过滥用证书颁发机构实用程序(certutil)获得反向外壳
*   通过滥用 Windows 脚本主机(csript)获得反向外壳
*   通过滥用 Windows Installer (msiexec)获得反向外壳
*   通过滥用 Microsoft Register Server Utility(regsvr 32)获得反向外壳

**杂项**

*   更改目标机器的壁纸| YouTube:

[![](img/e28019e416484c1370123f90c211e9f0.png)](https://www.youtube.com/watch?v=pBz3fG2S8f4)

*   使用. bat 脚本使 Windows 不响应(100% CPU 和 RAM 使用率)

[![](img/6d92d4bd475f21532ca68be428ed50a2.png)](https://www.youtube.com/watch?v=nCLVaGsIQOE)

*   放下并执行你选择的文件，也许是勒索软件？😉
*   禁用目标计算机上的 Windows Defender 服务

[![](img/e6c68f241da4af94d2c8312c027f6bc1.png)](https://www.youtube.com/watch?v=1tSQ7A5obHk)

**测试于**

*   卡利 Linux 2019.2
*   BlackArch Linux

**依赖关系**

Flashsploit 依赖于 4 个软件包，这些软件包通常预安装在主要的 Pentest 操作系统中:

*   Metasploit 框架
*   python3
*   science for the people 为人类服务的科学
*   服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

如果你认为我还应该做一个安装脚本，打开一个问题。

**用法**

**git 克隆 https://github . com/thewhite 4t/flashspleet . git
CD flashspleet
python 3 flashspleet . py**

[**Download**](https://github.com/thewhiteh4t/flashsploit)