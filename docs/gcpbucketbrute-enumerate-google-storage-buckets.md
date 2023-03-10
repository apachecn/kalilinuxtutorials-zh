# GCPBucketBrute:枚举 Google 存储桶的脚本

> 原文：<https://kalilinuxtutorials.com/gcpbucketbrute-enumerate-google-storage-buckets/>

[![GCPBucketBrute  : A Script To Enumerate Google Storage Buckets](img/d4e0f667ba6942ff6ec8a37e9548ecd6.png "GCPBucketBrute  : A Script To Enumerate Google Storage Buckets")](https://1.bp.blogspot.com/-AY_Bazpuf-Q/XcqfmYy64KI/AAAAAAAADZY/97Uh6dPjblYS42uU2iaTrJjFLWm7mH2ZgCLcBGAsYHQ/s1600/Google%2BStorage%2BBuckets%25281%2529.png)

gcpbucketbrut 是一个脚本，用于枚举 Google 存储桶，确定您对它们拥有什么访问权限，以及确定它们是否可以被提升权限。

*   该脚本(可选)接受 GCP 用户/服务帐户凭据和关键字。
*   然后，将从该关键字生成一个排列列表，该列表将用于扫描具有这些名称的 Google 存储桶的存在。
*   如果提供了凭据，大多数枚举仍将在未经身份验证的情况下执行，但是对于通过未经身份验证的枚举发现的任何存储桶，它将尝试使用 TestIamPermissions API 和提供的凭据来枚举存储桶权限。这将有助于找到经过身份验证时可访问的存储桶，而在未经身份验证时则不能。
*   不管是否提供了凭据，脚本都会在未经身份验证的情况下尝试使用 TestIamPermissions API 枚举 bucket 权限。这意味着，如果您不输入凭据，您将只看到未经身份验证的用户所拥有的特权，但是如果您输入凭据，您将看到经过身份验证的用户与未经身份验证的用户相比所拥有的访问权限。
*   **警告:**如果提供了凭据，您的用户名可能会在您发现的任何存储桶的访问日志中泄露。

**TL；灾难恢复摘要**

*   给定一个关键字，这个脚本根据该关键字生成的一些排列来枚举 Google 存储桶。
*   然后，将输出任何发现的桶。
*   然后，将输出您被授予的对任何发现的存储桶的任何权限(如果有的话)。
*   然后，该脚本将检查这些特权以进行特权提升(storage.buckets.setIamPolicy ),并将输出任何感兴趣的内容(如公共可列表、公共可写、认证可列表、特权提升等)。

**要求**

*   Linux/OS X
    *   Windows 仅适用于未经验证的扫描。脚本使用子流程模块的方式有问题，因为它在使用经过身份验证的 Google 客户端时会失败。
*   Python3
*   Pip3

**安装**

$ **git 克隆 https://github.com/RhinoSecurityLabs/GCPBucketBrute.git** $**CD gcpbucketbrut/** $**pip 3 install-r requirements . txt 或 python 3-m pip install-r requirements . txt**

**用途**

首先，确定要用于用户帐户、服务帐户或未经身份验证的帐户之间的枚举的身份验证类型。如果您使用服务帐户，请通过`**-f**` **/** `**--service-account-credential-file-path**`参数提供私钥的文件路径。

如果您使用的是用户帐户，请不要提供身份验证参数。然后，系统会提示您输入用户帐户的访问令牌，以访问 GCP API。如果你想扫描完全未经认证，通过`**-u**` **/** `**--unauthenticated**`参数隐藏认证提示。

*   在完全未经验证的情况下，使用关键字“test”扫描存储桶:

**python 3 gcpbucketbrut . py-k test-u**

*   使用服务帐户进行身份验证时，使用关键字“test”扫描存储桶(私钥存储在../sa-priv-key.pem)，将结果输出到当前目录下的 out.txt:

**python 3 gcpbucketbrut . py-k test-f../sa-priv-key.pem -o ./out.txt**

*   使用关键字“test”扫描存储桶，使用用户帐户访问令牌，用 10 个子流程而不是 5 个子流程运行:

**python 3 gcpbucketbrut . py-k test-s 10**

**可用参数**

*   `**-k**`**/**
    *   此参数用于指定使用什么关键字来生成置换。这些排列将在谷歌存储中被搜索。
*   `**--check**`
    *   该参数与`**-k**` **/** `**--keyword**`互斥，接受单个字符串。它允许您检查您对特定存储桶的权限，而不是基于关键字生成排列列表。这可以重复以检查几个桶。鸣谢: [@BBerastegui](https://github.com/BBerastegui)
*   `**--check-list**`****
    *   这个论点与`**-k**` **/** `**--keyword**`和`--check`是互斥的。它允许您检查文件中一系列存储桶的权限。它们应该在文本文件中每行列出一个。要从标准输入中读取，传递`-`作为文件名。
*   `**-s**`**/**
    *   此参数指定有多少子进程将用于桶枚举。默认值是 5，这个值设置得越高，枚举的速度就越快，但是每秒发送给 Google 的请求数会增加。这些本质上是线程，但是脚本使用子进程而不是线程来并行执行。
*   `**-f**`**/**
    *   此参数用于指定 GCP 服务帐户的私钥文件的路径，您要使用该帐户向 Google Storage 进行身份验证。这是可选的。如果您希望使用访问令牌，请省略此参数，系统会提示您输入令牌，因此不会将其保存到命令行历史记录中。更多信息请点击这里:[https://Google-auth . readthe docs . io/en/latest/user-guide . html # service-account-private-key-files](https://google-auth.readthedocs.io/en/latest/user-guide.html#service-account-private-key-files)还有这里:[https://Google-auth . readthe docs . io/en/latest/user-guide . html # user-credentials](https://google-auth.readthedocs.io/en/latest/user-guide.html#user-credentials)
*   `**-u**`**/**
    *   此参数强制进行未经身份验证的枚举。使用此标志，将不会提示您输入凭据，也不会检查有效的存储桶是否有经过身份验证的权限。
*   `**-o**`**/**`**--out-file**`****
    *   此参数允许您指定要将结果输出到的日志文件的(相对或绝对)文件路径。如果该文件尚不存在，将创建该文件；如果该文件已经存在，将向其追加内容。

[**Download**](https://github.com/RhinoSecurityLabs/GCPBucketBrute)