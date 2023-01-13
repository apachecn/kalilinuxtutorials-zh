# S3-帐户-搜索:S3 帐户搜索

> 原文：<https://kalilinuxtutorials.com/s3-account-search/>

[![S3-Account-Search : S3 Account Search](img/5804edc25be8aeb65a1eeefdccea41d5.png "S3-Account-Search : S3 Account Search")](https://1.bp.blogspot.com/-FdFRaeI9K6k/YOW8AVDnlcI/AAAAAAAAJ54/Elap_65pP9ItmDT733hZVovWGMShORSMwCLcBGAsYHQ/s728/S3-Account-Search%25281%2529.png)

**S3 账户搜索**工具也能让你找到一个 S3 账户所属的账户 id。

为此，您需要至少拥有以下权限之一:

*   从桶中下载已知文件的权限(`**s3:getObject**`)。
*   允许列出桶中的内容(`**s3:ListBucket**`)。

此外，您将需要一个角色，您可以在您正在检查的存储桶上承担这些权限中的一个

更多的背景资料可以在 Cloudar 博客上找到

**安装**

这个包在 pypi 上可用，例如，您可以使用这些命令中的一个(推荐使用 pipx)

**pipx 安装 S3-账户-搜索
pipx 安装 S3-账户-搜索**

**用法举例**

**#带桶
S3-账户-搜索 arn:AWS:iam::123456789012:role/S3 _ read S3://my-bucket
#带对象
S3-账户-搜索 arn:AWS:iam::123456789012:role/S3 _ read S3://my-bucket/path/to/object . ext
#你也可以省去 S3://
S3-账户-搜索 arn**

**这是如何工作的**

有一个 IAM 策略条件 **`s3:ResourceAccount`** ，用于授予指定(一组)帐户对 S3 的访问权限，但也支持通配符。通过构建正确的模式，并查看哪些模式将导致拒绝或允许，我们可以通过一次发现一个数字来确定帐户 id。

1.  我们验证我们可以使用提供的角色访问对象或存储桶
2.  我们再次承担相同的角色，但是这一次添加了一个策略，限制我们访问以`**0**`开始的帐户中存在的 S3 存储桶。如果我们的访问被允许，我们知道帐户 id 必须以 **`0`开头。**如果请求被拒绝，我们用 **`1`** 作为第一位数字再试一次。我们不断增加，直到我们的请求被允许，我们找到第一个数字
3.  我们对每个数字重复这个过程。使用已经发现的数字作为前缀。例如，如果第一个数字是`**8**`，我们测试以 **`80`、`81`、`82`** 等开始的账户 id。

**开发**

我们用诗歌来管理这个项目

*   克隆此存储库
*   运行`**poetry install**`
*   用`**poetry shell**`(也可以用 **`poetry run $command` )** 激活虚拟环境

**向 pypi 发布新版本**

*   编辑 pyproject.toml 以更新版本号
*   提交版本号提升
*   运行`**poetry publish --build**`
*   推送至 GitHub
*   在 GitHub 中创建新版本

**可能的改进**

我们可以使用类似二分搜索法的算法，而不是一次检查一个数字。以下条件等同于`**s3:ResourceAccount < 500000000000**`

**"条件":{
" string like ":{ " S3:resource account ":[
" 0*"，" 1* ，" 2 *，" 3* ，" 4* "，
}，
}，**

*   类似地，通过并行检查每个位置的多个数字，有可能提高速度(当使用这种方法时，有被 STS 限制速率的小风险)

在实践中，这个工具在大多数情况下应该足够快。

[**Download**](https://github.com/WeAreCloudar/s3-account-search)