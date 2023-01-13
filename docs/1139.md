# S3enum:用于 Pentesters 的快速亚马逊 S3 桶枚举工具

> 原文：<https://kalilinuxtutorials.com/s3enum/>

[![S3enum : Fast Amazon S3 Bucket Enumeration Tool For Pentesters](img/a435300c4b5134d0256f941c476516bc.png "S3enum : Fast Amazon S3 Bucket Enumeration Tool For Pentesters")](https://1.bp.blogspot.com/-kmO0qKQK54U/XjtNjw-XZgI/AAAAAAAAEuE/EP-AeqU2QugEAFnu2VNsPA_ODx3iQOx5QCLcBGAsYHQ/s1600/S3%25281%2529.png)

S3enum 是一个工具，用于枚举目标的亚马逊 S3 桶。它速度很快，利用 DNS 而不是 HTTP，这意味着请求不会直接命中 AWS。

**出发**

去找 github.com/koenrh/s3enum

**也可阅读-[Python asub fuscate:混淆一个 Python 脚本&附带的外壳代码](https://kalilinuxtutorials.com/pythonaesobfuscate-obfuscates-a-python-script-accompanying-shellcode/)**

**用途**

您需要指定目标的基本名称(例如`hackerone`)和一个单词列表。您可以使用这个存储库中的示例`wordlist.txt`文件，或者从其他地方获得一个单词列表。或者，您可以指定线程的数量(默认为 10)。

**$ S3 enum–word list examples/word list . txt–suffix list examples/suffix list . txt–threads 10 hacker one

hacker one
hacker one-attachment
hacker one-attachments
hacker one-static
hacker one-upload**

默认情况下，`s3enum`将使用在`/etc/resolv.conf`中指定的名称服务器。或者，您可以使用`--nameserver`选项指定一个不同的名称服务器。此外，你可以同时测试多个名字。

**S3 enum \
–wordlist examples/wordlist . txt \
–suffixlist examples/suffixlist . txt \
–name server 1.1.1.1 \
hacker one h1 rofl copter**

[**Download**](https://github.com/koenrh/s3enum)