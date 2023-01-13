# VSHG:GnuPG 的独立插件

> 原文：<https://kalilinuxtutorials.com/vshg-gnu-privacy-guard/>

VSHG 的目标是为 GnuPG 的标准 s2k 密钥导出函数提供一个内存/硬件抗性增强+一个用于**对称**加密的简化接口。它(非常安全的哈希生成器)是 GnuPG ( Gnu 隐私卫士)的一个独立插件。

它是作为一个 shell 脚本编写的，是围绕 Unix/Linux 文件系统和命令设计的。VSHG 使用 **sha384** 和 **Argon2** 哈希函数作为密码，并级联使用**AES-256-CFB**+**cast 5-128-CFB**进行最终加密。

还有一个标准的 **sha384** 迭代次数为 **800** 迭代次数+ **15** & **500** 迭代次数为**argon 21**+**d**

它使用真正随机的 **12 字节盐**。因此，即使您的密码非常弱，它也会加强它，这样您就不必再担心了。

VSHG 使用迭代的最后一个散列作为 Gnupg 的会话密钥。它还为每个文件提供了自动检测功能，因此您不必记住 salt 或迭代次数。

您可以选择使用密钥文件作为身份验证方法。

**又读-[node crypto:NodeJs](https://kalilinuxtutorials.com/nodecrypto-ransomware/)T3 中写的勒索软件**

**为什么 VSHG 这么安全？**

VSHG 为每个加密的文件使用一个真正的随机 salt，所以你的密码至少有 12 个字节。你甚至可以对不同的文件使用两次相同的密码。

让 VSHG 如此安全的是迭代。800 次迭代意味着字符串的输出与其输出进行哈希运算 **800x** 。迭代次数越多，安全性就越高。即使您有正确的密码，但没有正确的迭代次数，它也无法解密。

VSHG 使用一些最先进的内存硬键派生函数，它们是 **Argon2i** 和 **Argon2d** 。已经迭代的密钥将总共通过 argon 2**515**次，并因此确保抵抗密钥导出功能的最大威胁，即:图形处理单元、现场可编程门阵列和专用集成电路( **GPU** 、 **FPEGA** 、 **ASIC** )。

实际的加密是以 Gnupg 中可能的最高安全级别来执行的。

*   string to key(**s2k**)**hash algo**(也就是 Gnupg 的 KDF)从 sha1 加固到 **sha512** 。
*   **s2k 模式**被设置为 **3** ，这意味着应用 8 位 salt，然后进行迭代。
*   将 **s2k 计数**设置为 **65011712** ，这是可能的最高迭代次数。
*   将 **s2k 算法**设置为 **AES256** 和 **CAST5** 级联。
*   AES 256 加密文件被安全删除，因此仅**AES 256(cast 5())加密文件被输出**。

**我为什么要使用 VSHG？**

*   比 GnuPG 核心好用。
*   可以通过将文件夹转换成 Zip 文件来加密它们。
*   没有 VSHG 的人没有机会破解密码。
*   真随机 12 字节 salt
*   可选择的迭代计数。
*   可选择的盐。
*   可选择的密钥文件。
*   真随机密钥文件。
*   非常好的抗侧信道攻击(例如:定时攻击)。
*   非常抵制基于 GPU 的攻击
*   即使使用相对较弱的密码(> 5 个字符)，也能保证安全性(如果您有足够的迭代次数)
*   自动检测盐+每个文件的迭代计数。
*   军用标准 AES-256 加密 gpg 标准 CAST5 加密。
*   使用 gpg s2k 模式 3 + sha512，最大计数为 65011712。
*   安全删除原始文件。

**下载&安装**

**下载为 tarball**

**sudo wget https://github.com/RichardRMatthews/VSHG/archive/1.4.tar.gz
或者克隆库【https://github.com/RichardRMatthews/VSHG.git】git 克隆 T2**

**自己编译**

克隆 https://github.com/neurobin/shc.git
CD SHC
sudo。/SHC-f-r/etc/VSHG/executable/src/VSHG _ 1.4 . sh
sudo gcc/etc/VSHG/executable/src/VSHG _ 1.4 . sh . x . c-O/usr/bin/VSHG
sudo VSHG

**运行**

**须藤 tar-xf VSHG-1.4.tar.gz
须藤 chmod +x VSHG_1.4.sh
须藤。/VSHG_1.4.sh**

[**Download**](https://github.com/RichardRMatthews/VSHG)