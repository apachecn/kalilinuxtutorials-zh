# AES Finder:在运行的进程中查找 AES 密钥的实用程序

> 原文：<https://kalilinuxtutorials.com/aes-finder/>

[![AES Finder : Utility To Find AES Keys In Running Processes](img/4336922fb136d99470216e02fd652a73.png "AES Finder : Utility To Find AES Keys In Running Processes")](https://1.bp.blogspot.com/--nluKtQmlsc/X2iXH3iWsJI/AAAAAAAAHkQ/wZUgCeRyHakYmyrSiMM3dAps0cawC0b-QCLcBGAsYHQ/s728/h92%25281%2529.png)

**AES Finder** 是一个在运行进程内存中查找 AES 密钥的实用程序。适用于 128、192 和 256 位密钥。

**用途**

在 Visual Studio 2013 中打开`**aes-finder.sln**`解决方案编译源代码。或者使用 gcc/clang:

**g++-O3-March = native-fomit-frame-pointer AES-finder . CPP-o AES-finder**

要搜索 id = 123 的进程中的键，请执行以下命令:

**aes-finder.exe-123**

要在任何名为 chrome.exe 的进程中搜索关键字，请执行以下操作:

aes-finder.exe·chrome.exe

现在您可以看到在您最喜欢的应用程序中使用了哪种 AES 密钥！

**腻子**

**C:>aes-finder.exe putty.exe
搜索 PID 2180…
【0016 c904】找到 AES-256 加密密钥:000102030405060708090 a 0 b 0 C 0d 0 e 0 f 101112131415161718191 a1 B1 C1 D1 e 1 f
【0016 C9 f 4】找到 AES-256 解密密钥:0001020300**

**Dropbox**

c:> AES-finder . exe dropbox.exe
搜索 PID 2204…
【00 F5 DDE 8】找到 AES-128 加密密钥:e73c 856 f 10 e 56d 8 de 0510 e 964 e 71 b 33
…许多相同的密钥
【0363 a708】找到 AES-128 加密密钥:e73c 856 f 10 e 56d 8 de 0510 e 964 e 71 b 33
【03710 a 24 找到 AES-128 加密密钥:0e 7484 bb 0230 b 137 EB 582 BAE 6 ea 17 e 09
【03884 a 28】找到 AES-128 加密密钥:0e 7484 bb 0230 b 137 EB 582 BAE 6 ea 17 e 09
【03892330】找到 AES-256 加密密钥:8843 f 5b 83 b 0b 88 ffefcdc 4 a 6 FB 1 dbece 找到 AES-256 加密密钥:BBC 3 ede 28857 b 90389452846 E4 b 80 ca 5 e 262 ef 57 ce 918 ce 17 c 89 b 6598993 FAA 4
【039 E1 a 24】找到 AES-128 加密密钥:afde 7 f5a 3184111 f 877 f 0 E8 b 61 f 85 ad 8
【039 E1 c 40】找到 AES-125

**铬合金**

c:> AES-finder . exe chrome.exe
搜索 PID 1792…
【08d 8302 c】找到 AES-256 解密密钥:c 73159441 a 23 df 68 b 292 a 666 a 082418048 a 844813 dfe 8636126 e 875204813291
【08d 8326 c】找到 AES-256 加密密钥:a85f 4333 找到 AES-128 解密密钥:ce 3 be 55 b 440620 be 4 aa 73 e 33 c 325456 f
【0907422 c】找到 AES-128 加密密钥:1954 a 522 cf 12287 a 245d 66786d 78 bb a5
【0907446 c】找到 AES-128 解密密钥:7972 ca 805 c 44 bacc 6a 70691 a 606d

**Python + PyCrypto**

c:>从 Crypto 启动 python -c”。密码导入 AESa=AES.new('\x42'*24，AES。MODE _ ECB)；input()"

C:>aes-finder.exe python.exe
搜索 PID 264…
【00b 84074】找到 AES-192 加密密钥:424242424242424242424242424242424242424242424242424242
【00b 84164】找到 AES-192 解密密钥:4242424242424242424242

**Linux 上的 SSHD**

$须藤。/aes-finder sshd
搜索 PID 3307 …
搜索 PID 10428 …
搜索 PID 10430…
【0x 7 fc 39 b 3132d 0】找到 AES-128 加密密钥:df 435 cfcd 8830 df 858203 c 0 ad 2d b 51 ca
【0x7fc 39 b 313450】找到 AES-128 加密密钥:0ad 922797 ABA 3070

**OS X 苹果电脑上的 iTunes**

$须藤。/aes-finder iTunes
搜索 PID 40912…
【0x 7 Fe 073 e 7 DD 3 c】找到 AES-128 加密密钥:743554 FB 48 b 78d 29 ad 73 FBD 231373982
【0x 7 Fe 073 e 7 de 00】找到 AES-128 加密密钥:743554 FB 48 b 78d 29 ad 73 FBD 231373982
【0x 7 Fe

**注释**

*   不适用于白盒 AES 密钥
*   32 位二进制只能在 32 位进程中搜索，64 位二进制可以在 32 位和 64 位进程中搜索
*   “加密密钥”是指该密钥可用于加密或解密
*   “解密密钥”意味着该密钥很可能仅用于解密
*   在 Linux 上至少需要 3.2 版内核(process_vm_readv syscall)

[**Download**](https://github.com/mmozeiko/aes-finder)