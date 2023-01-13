# fire Master——Firefox 主密码恢复工具

> 原文：<https://kalilinuxtutorials.com/firemaster-password-recovery-tool/>

FireMaster 是有史以来主要的工具，它利用简单的尖端密码恢复技术来恢复您丢失或忽略的 Firefox 主密码。

Firefox 使用主密码来保护所有访问过的站点的登录/密码数据。在主密码被忽略的情况下，在这一点上，没有真正的方法来恢复主密码，客户端将丢失存储在其中的每一个密码。

FireMaster 支持以下 Firefox 主密码恢复技术，

*   字典法
*   混合字典法
*   强力方法
*   基于模式的暴力方法

**也读作 [开膛手约翰——一站式密码审计工具](https://kalilinuxtutorials.com/johnny/)**

## **fire master 如何工作？**

基于模式的系统从本质上减少了恢复时间，尤其是当您回忆起密码的某个部分时。当你失去了主密码，没有真正的方法来恢复它，因为它没有以任何方式存储。

无论客户端何时输入主密码，Firefox 都会利用它来解读与已知字符串相关的加密信息。

如果解密的信息与该已知字符串相匹配，则输入的密码是正确的。FireMaster 使用类似的方法来检查主密码，但方式更加改进。

整个活动是这样的。

*   FireMaster 通过不同的技术动态创建密码。
*   此时，它利用已知的计算方法处理密码的散列。
*   接下来，该密码散列被用于解密已知明文内容的加扰信息(即“密码检查”)。
*   目前，如果解密后的字符串与已知的明文内容匹配(即“密码检查”)，则此时产生的密码就是主密码。

Firefox 将关于加密字符串、salt、计算和重现数据的见解存储在客户机的配置文件注册表中的输入数据库记录 **key3.db** 中。您可以简单地将这个 key3.db 文档复制到各种目录中，并确定与 FireMaster 的比较方式。同样，您可以将这个 key3.db 复制到其他顶级机器上，以便更快地完成恢复任务。

## **如何使用 FireMaster？**

首先，您需要将 **key3.db** 文件复制到临时目录中。稍后，您必须将 FireMaster 的这个目录路径指定为最后一个参数。

以下是一般使用信息

```
Firemaster [-q]
[-d -f <dict_file>]
[-h -f <dict_file> -n <length> -g "charlist" [ -s | -p ] ]
[-b -m <length> -l <length> -c "charlist" -p "pattern" ]
<Firefox_Profile_Path>

Note: With v5.0 onwards, you can specify 'auto' (without quotes) in place of "<Firefox_Profile_Path>" to automatically detect default profile path.
Dictionary Crack Options:
-d  Perform dictionary crack
-f  Dictionary file with words on each line

**Hybrid Crack Options:**

-h  Perform hybrid crack operation using dictionary passwords.
Hybrid crack can find passwords like pass123, 123pass etc
-f Dictionary file with words on each line
-g Group of characters used for generating the strings
-n Maximum length of strings to be generated using above character list
These strings are added to the dictionary word to form the password
-s Suffix the generated characters to the dictionary word(pass123)
-p Prefix the generated characters to the dictionary word(123pass)

**Brute Force Crack Options:**

-b Perform brute force crack
-c Character list used for brute force cracking process
-m [Optional] Specify the minimum length of password
-l Specify the maximum length of password
-p [Optional] Specify the pattern for the password
```

**火神**的例子

| **//字典破解** |
| FireMaster.exe-d-f c:\ dict file . txt auto |
|  |
| **//混合型裂纹** |
| FireMaster.exe-h-f c:\ dict file . txt-n 3-g " 123 "-s auto |
|  |
| **//暴力破解** |
| FireMaster.exe-q-b-m 3-l 10-c " abcdetps 123 " " c:\我的测试\火狐" |
|  |
| **//图案为**的强力破解 |
| FireMaster.exe-q-b-m3-c " abyz 126 "-l 10-p " pa？？f？？123 英寸自动 |
|  |

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://securityxploded.com/firemaster.php)