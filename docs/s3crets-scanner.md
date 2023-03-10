# S3Crets 扫描仪:搜寻上传到公共 S3 桶的秘密

> 原文：<https://kalilinuxtutorials.com/s3crets-scanner/>

[![](img/7aacf2131305a6e88700db7de56a9d34.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAzrBXe8ApdzbYCkQwcgIILnnSRCGSKqE6ym-sDP35VZuO4LrUz8ZYLOJTnxDNyvvgwo_2E4jyWmAKjzETEWTagoINk30JvUIhb1U-P_FqDgonsxlr6uBUz7CSizFGwrm8-pRYoQD7aNYWH2n97-KDzQN3hgAU2h6w53jJj75Xchzalm0z2xu59L8A/s728/S3cret%20Scanner(1).png)

**S3cret Scanner** 工具旨在通过主动搜寻公共 S3 桶中的秘密，为亚马逊 S3 安全最佳实践提供补充层。

可以按计划任务执行，也可以按需执行。

## **自动化工作流程**

自动化将执行以下操作:

列出账户中的公共桶(设置了 public 或 objects 可以是 Public 的 ACL)
列出文本或敏感文件(即 p12，.下载，扫描(使用 truffleHog3)和删除磁盘上的文件，一旦完成评估，一个接一个。
日志将在 logger.log 文件中创建。

## **先决条件**

1.  Python 3.6 或以上版本
2.  安装在 PATH 中的 TruffleHog3
3.  具有以下权限的 AWS 角色:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:GetLifecycleConfiguration",
                "s3:GetBucketTagging",
                "s3:ListBucket",
                "s3:GetAccelerateConfiguration",
                "s3:GetBucketPolicy",
                "s3:GetBucketPublicAccessBlock",
                "s3:GetBucketPolicyStatus",
                "s3:GetBucketAcl",
                "s3:GetBucketLocation"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "*"
        }
    ]
}
```

4.  如果您使用的是 CSV 文件，请确保将文件`accounts.csv`放在`csv`目录中，格式如下:

```
Account name,Account id
prod,123456789
ci,321654987
dev,148739578
```

## **入门**

使用 [pip](https://pip.pypa.io/en/stable/) 安装所需的需求。

```
# Clone the repo
git clone <repo>
# Install requirements
pip3 install -r requirements.txt
# Install trufflehog3
pip3 install trufflehog3
```

## **用途**

| 争吵 | 价值观念 | 描述 | 需要 |
| --- | --- | --- | --- |
| -p，–AWS _ profile |  | 访问键的 aws 配置文件名 | -好的 |
| -r，–扫描仪角色 |  | aws 扫描器的角色名称 | -好的 |
| -m，–方法 | 内部的 | 扫描类型 | -好的 |
| -l，–最后一次修改 | 1-365 | 自上次修改文件以来要扫描的天数；*默认–1* | 一千 |

## **演示**

![](img/68ac3573e2dde887c8641326a8bd3977.png)