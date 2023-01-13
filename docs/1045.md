# HashCobra:哈希破解工具

> 原文：<https://kalilinuxtutorials.com/hashcobra-hash-cracking-tool/>

[![HashCobra : Hash Cracking Tool](img/7583a869b4917ad76cf8277774878622.png "HashCobra : Hash Cracking Tool")](https://1.bp.blogspot.com/-sOotYc9cFkg/XfI4hQDLkKI/AAAAAAAAD7g/dl2q8qyNYGcXep-H-x9azyhEJvU-R7C5gCLcBGAsYHQ/s1600/HasCobra%25281%2529.png)

**HashCobra** 是一个使用新方法破解哈希的工具。借助彩虹表的概念，这个工具从单词表中生成彩虹表，以极大地优化破解过程。

**$。/hash cobra-H**
–= =[hash obra by sepehrdad]= =–

**用法:**
hash obra-o<opr>【选项】|【misc】

**选项:**
-a<alg>–哈希算法【默认:MD5】
–？列出可用算法
-c<alg>-压缩算法【默认:zstd】
-?要列出可用算法
-h <哈希>-哈希破解
-r <路径>-彩虹表路径【默认:hash cobra . db】
-d<路径>-字典文件路径
-o<opr>-操作要做
–？列出可用操作
**Misc:**
-V–显示版本
-H–显示帮助
**示例:**
**#从 rock you . txt**
$ hash cobra-o Create-d rock you . txt

**#从 darkc 0 de . lst**
$ has 创建不压缩的 md5 彩虹表

**也可阅读-[re conpi:一个轻量级的侦察工具，执行广泛的扫描](https://kalilinuxtutorials.com/reconpi-recon-tool-performs-extensive-scanning/)**

**支持的哈希算法**

*   黑色 2b-160
*   黑色 2b-256
*   黑色 2b-384
*   黑色 2b-512
*   黑色 2s-128
*   blake2s-160
*   布莱克 2s-224
*   布莱克 2s-256
*   md2
*   md4
*   讯息摘要 5
*   sha1
*   sha224
*   sha256
*   sha384
*   sha512
*   sha3-224
*   sha3-256
*   sha3-384
*   sha3-512
*   凯克 224 号
*   凯克 256 号
*   keccak-384 型飞机
*   keccak-512 型飞机
*   ripemd-128
*   ripemd-160
*   ripemd-256
*   ripemd-320
*   漩涡
*   老虎

**支持的压缩算法**

*   zstd
*   时髦的
*   zlib
*   bzip2
*   lz4
*   lz4hc

**大楼**

**$ make**

**安装**

**$ make 安装**

**免责声明**

该软件仅供教育使用！如果您参与任何非法活动，作者对此不承担任何责任。使用本软件即表示您同意这些条款。

[**Download**](https://github.com/sepehrdaddev/hashcobra)