# 哈希克星 3.0 版:在几秒钟内破解哈希

> 原文：<https://kalilinuxtutorials.com/hash-buster-v3-0/>

[![Hash-Buster v3.0 : Crack Hashes In Seconds](img/30256e9312b77082227d35f3f1817532.png "Hash-Buster v3.0 : Crack Hashes In Seconds")](https://1.bp.blogspot.com/-r23SO0HzqWo/YPmJ_28uW2I/AAAAAAAAKKc/yBWaKpZ1d9YOOjuVMv6zx6v6e5skOGIHQCLcBGAsYHQ/s728/1%2B%25281%2529.png)

**Hash-Buster v3.0** 是一款在几秒钟内破解哈希的工具。

**特性**

*   自动哈希类型识别
*   支持 MD5、SHA1、SHA256、SHA384 和 SHA512
*   可以从文件中提取和破解哈希
*   可以从一个目录中递归地找到哈希值
*   多线程

**安装&使用**

**注意:** Hash Buster 与 python2 不兼容，请改用 python3 运行。此外，Hash-Buster 使用一些 API 进行哈希查找，如果您有妄想症，请查看源代码。

Hash-Buster 可以直接从 python 脚本运行，但是我强烈建议你用`**make install**`安装它

安装完成后，您将能够使用`**buster**`命令访问它。

**破解单个哈希**

您不需要指定哈希类型。哈希巴斯特将在 3 秒钟内识别并 ***破解*** 它。

**用法:** `**buster -s <hash>**`

**从目录中查找哈希**

是的，只要指定一个目录，Hash Buster 就会遍历其中的所有文件和目录，寻找散列。

**用法:** `**buster -d /root/Documents**`

**破解文件中的哈希值**

哈希巴斯特可以找到你的哈希，即使它们存储在这样的文件中

**simple @ Gmail . com:21232 f 297 a 57 a5a 743894 a 0 E4 a 801 fc 3
{ " JSON @ Gmail . com ":" d 033 e 22 AE 348 aeb 5660 fc 2140 AEC 35850 C4 da 997 "}
surronded bytext 8 c 6976 e5b 5410415 bde 908 BD 4d dee 15 DFB 167 a9 c 873 fc 4 bb 8**

**用法:** `**buster -f /root/hashes.txt**`

**指定线程数**

当您通过并行请求来处理大量散列时，多线程会令人难以置信地降低整体速度。

**用法:** `**buster -f /root/hashes.txt -t 10**`

[**Download**](https://github.com/s0md3v/Hash-Buster)