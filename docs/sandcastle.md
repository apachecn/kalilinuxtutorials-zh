# Sandcastle:用于 AWS S3 桶枚举的 Python 脚本

> 原文：<https://kalilinuxtutorials.com/sandcastle/>

[![Sandcastle : A Python Script For AWS S3 Bucket Enumeration](img/edc1c1c23c15fc76eaaa60522abe8642.png "Sandcastle : A Python Script For AWS S3 Bucket Enumeration")](https://1.bp.blogspot.com/-7bz2H6k5fiI/Xos7ncirNFI/AAAAAAAAF2A/y-SYA_tf24g4BNftyKObVVcwRVUjjWgPgCLcBGAsYHQ/s1600/sandcastle.png)

受与 Instacart 的@nickelser 在 HackerOne 上的对话的启发，我优化并发布了 sand castle——一个用于 AWS S3 桶枚举的 Python 脚本，以前被称为 bucketCrawler。

该脚本将目标的名称作为词干参数(例如`**shopify**`)，并遍历存储桶名称排列的文件，如下所示:

-训练
-铲斗
-开发
-附件
-照片
-弹性搜索[…]

**入门**

*   **下面是如何开始:**
    *   克隆此 repo(暂时禁用 PyPi 分发)。
    *   使用目标名称和输入文件运行`**sandcastle.py**`(从这个 repo 中抓取一个例子)
    *   将识别匹配的存储桶排列，并测试读取权限。

**用法:**sand castle . py[-h]-t target Stem[-f input file]
**参数:**
-h，–help 显示此帮助信息并退出
-t targetStem，–target stem
选择一个目标 stem 名称(如' shopify')
-f inputFile，–file input file
选择一个 bucket 置换文件(默认:bucket-
names.txt)

> > S3 桶枚举//发布 v1.2.4 // ysx
> > [*]开始枚举' shopify '，从' bucket-names.txt '中读取 138 行。
> > [+]检查潜在匹配:shopify-content->403
>>调用 ListObjects 操作时出错(AccessDenied):访问被拒绝

**又读-[MSSQLi-DUET:基于 MSSQL 注入的域用户枚举工具](https://kalilinuxtutorials.com/mssql-injection/)**

**状态代码&测试**

| 状态代码 | 定义 | 笔记 |
| --- | --- | --- |
| Four hundred and four | 找不到桶 | 不是分析的目标(默认情况下隐藏) |
| Four hundred and three | 拒绝访问 | 通过 CLI 进行分析的潜在目标 |
| Two hundred | 公众可访问的 | 通过 CLI 进行分析的潜在目标 |

**AWS CLI 命令**

以下是一些有用的 AWS CLI 命令的快速参考:

*   列表文件:`**aws s3 ls s3://bucket-name**`
*   下载文件:`**aws s3 cp s3://bucket-name/<file> <destination>**`
*   上传文件:`**aws s3 cp/mv test-file.txt s3://bucket-name**`
*   移除文件:`**aws s3 rm s3://bucket-name/test-file.txt**`

什么是 S3？

*   来自亚马逊[文档](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html)，使用亚马逊 S3 桶:
*   亚马逊 S3[简单存储服务]是互联网的云存储。上传您的数据(照片、视频、文档等)。)，首先在其中一个 AWS 区域中创建一个 bucket。然后，您可以将任意数量的对象上传到存储桶。
*   在实现方面，桶和对象都是资源，亚马逊 S3 提供 API 让你管理它们。

**结束语**

*   这是我第一个公安项目。《沙堡》是在麻省理工学院许可下出版的。
*   使用鸣谢:
    *   来自名词项目的安德鲁·多恩的城堡(图标)
    *   **谢妮一号(logo 字样)由 Jovanny Lemonad 免费**

[**Download**](https://github.com/0xSearches/sandcastle)