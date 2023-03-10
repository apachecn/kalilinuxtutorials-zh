# Cryptr:一个使用 OpenSSL 加密和解密文件的简单 Shell 实用程序

> 原文：<https://kalilinuxtutorials.com/cryptr-encrypting-decrypting/>

[![Cryptr : A Simple Shell Utility For Encrypting & Decrypting Files Using OpenSSL](img/53a0a5c9291d9528a3a8a94c476810cd.png "Cryptr : A Simple Shell Utility For Encrypting & Decrypting Files Using OpenSSL")](https://1.bp.blogspot.com/-9koAPccQRPE/XRTufQJ1rUI/AAAAAAAABDk/tPb5NdGhiWwHZdzLuLudcwuFexkSbEM6gCLcBGAs/s1600/Encrypting%2BAnd%2BDecrypting.png)

Cryptr 是一个简单的 shell 实用程序，使用 OpenSSL 对文件进行加密和解密。

**安装**

git 克隆 https://github . com/nodesocket/crypt . git
ln-s " $ pwd "/crypt/crypt . bash/usr/local/bin/crypt

**猛击标签完成**

将`**tools/cryptr-bash-completion.bash**`添加到选项卡完成文件目录中。

**API/命令**

**加密**

**加密<文件>–使用 OpenSSL AES-256 密码块链接加密文件。将加密文件写出** ***(密文)*** **追加** `**.aes**` **扩展名。**

➜密码器 encrypt。/secret-file
输入 aes-256-cbc 加密密码:
验证–输入 aes-256-cbc 加密密码:

**➜ls-alh**
-rw-r–r–1 用户组 1.0G Oct 1 13:33 秘密文件
-rw-r–r–1 用户组 1.0G Oct 1 13:34 秘密文件. aes

您可以选择使用`CRYPTR_PASSWORD`环境变量定义加密时使用的密码。这使得非交互式/批处理操作成为可能。

➜cryptr _ password = a eo7s 9 ssqycpchor 47n cryptr encrypt。/秘密文件

**也可阅读-[Red ghost:旨在协助 Red 团队的 Linux Post 开发框架](https://kalilinuxtutorials.com/redghost-linux-post-exploitation/)**

**解密**

解密<file.aes>–使用 OpenSSL AES-256 密码块链接解密加密文件。将解密后的文件写出*(明文)*去掉`.aes`扩展名。</file.aes>

**➜ls-alh** -rw-r–r–1 用户组 1.0G Oct 1 13:34 secret-file.aes

➜解密。/secret-file.aes
输入 aes-256-cbc 解密密码:

**➜ls-alh** -rw-r–r–1 用户组 1.0G Oct 1 13:35 秘密文件
-rw-r–r–1 用户组 1.0G Oct 1 13:34 秘密文件. aes

您可以选择使用`CRYPTR_PASSWORD`环境变量定义解密时使用的密码。这使得非交互式/批处理操作成为可能。

➜cryptr _ password = a1 eo7s 9 ssqycpchor 47n cryptr decrypt。/secret-file.aes

**帮助**

帮助–显示帮助

```
➜ cryptr 帮助
用法:cryptr 命令**<command-specific-options></command-specific-options>
<command-specific-options>加密<</command-specific-options> `file` <command-specific-options>> <file>加密文件</file></command-specific-options>
<command-specific-options><file>解密<file.aes><</file.aes></file></command-specific-options>`file.aes`<command-specific-options><file><file.aes>>解密加密文件</file.aes></file></command-specific-options>
<command-specific-options><file><file.aes></file.aes></file></command-specific-options>
```

**版本**

版本–显示当前版本

**加密版本**
加密 2.1.1

**默认**

默认–显示当前版本和帮助

```
➜ cryptr cryptr 2.1.1
用法:cryptr 命令**<command-specific-options></command-specific-options> **<command-specific-options>加密</command-specific-options> `<file>` <command-specific-options><file>加密文件</file></command-specific-options>
<command-specific-options><file>解密</file></command-specific-options><command-specific-options><file><file.aes>解密加密文件</file.aes></file>
<command-specific-options><file><file.aes>帮助显示帮助</file.aes></file></command-specific-options></command-specific-options>
```


 ****版本控制**

为了发布周期的透明性和洞察力，也为了努力保持向后兼容性，cryptr 将在语义版本指南下维护。

版本将按照以下格式进行编号:

`**<major>.<minor>.<patch>**`

并按照以下指导原则进行构建:

*   打破向后兼容性会破坏主要版本(并重置次要版本和补丁)
*   不破坏向后兼容性的新增加的内容会影响次要内容(并重置补丁)
*   错误修复和杂项变化颠簸的补丁

有关语义版本的更多信息，请访问[http://semver.org/](http://semver.org/)。

**执照&合法**

版权 2019 贾斯汀·凯勒

根据 Apache 许可证 2.0 版许可(“许可证”)；除非符合许可证的规定，否则您不得使用本文件。您可以从以下网址获得许可证的副本

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

除非适用法律要求或书面同意，根据许可证分发的软件按“原样”分发，没有任何种类的明示或暗示的保证或条件。请参阅许可证，了解许可证下管理权限和限制的特定语言。

[**Download**](https://github.com/nodesocket/cryptr)**