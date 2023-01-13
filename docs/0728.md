# 云安全审计:Amazon Web Services 的命令行安全审计工具

> 原文：<https://kalilinuxtutorials.com/cloud-security-audit-aws/>

[![Cloud Security Audit : A Command Line Security Audit Tool For Amazon Web Services](img/5d1865f2fdfe320a2368dfe75f29e880.png "Cloud Security Audit : A Command Line Security Audit Tool For Amazon Web Services")](https://1.bp.blogspot.com/-5deRXCojgPk/XSd1IKF-mbI/AAAAAAAABT4/gBUGXvW9ww0hht9RQf4qCd5e8FKFTExBgCLcBGAs/s1600/AWS%25282%2529.png)

**云安全审计**是一个命令行工具，可以扫描你的 AWS 账户中的漏洞。通过简单方式，您将能够识别基础设施中不安全的部分，并为安全审计准备好您的 AWS 帐户。

**安装**

目前它不支持任何包管理器，但这项工作正在进行中。

**建筑来源**

首先，您需要将其下载到您的 GO 工作区:

**$GOPATH $ go 获取 github.com/Appliscale/cloud-security-audit
$ GOPATH $ CD 云-安全-审计**

然后，通过执行以下命令，在 cloud-security-audit 目录中为应用程序构建和安装配置:

**云-安全-审计$ make all**

**也可阅读-[Dark scrape:OSINT 用于抓取黑暗网站的工具](https://kalilinuxtutorials.com/darkscrape/)**

**用法**

**初始化会话**

如果你正在使用 MFA，你需要告诉它在尝试使用标志`--mfa`连接之前验证你。示例:

**$云-安全-审计-服务 S3-MFA-MFA-持续时间 3600**

**EC2 扫描**

**如何使用**

要对所有 EC2 实例执行审计，请键入:

**$云-安全-审计-服务 ec2**

您可以使用标志`**-r**` **或** `**--region**` **将审计范围缩小到一个区域。**它还支持 AWS 配置文件-要指定配置文件，请使用标志`**-p**` **或** `**--profile**` **。**

**文档**

您可以在以下文档中找到有关加密的更多信息:

[https://docs . AWS . Amazon . com/AWS C2/latest/user guide/EBS encryption . html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html)

**S3 扫描**

**如何使用**

要对所有 S3 时段执行审计，请键入:

**$云-安全-审计-服务 s3**

它支持 AWS 配置文件-要指定配置文件，请使用标志`**-p**` **或** `**--profile**` **。**

**文档**

您可以在以下文档中找到有关保护 S3 的更多信息:

*   [**https://docs . AWS . Amazon . com/Amazon S3/latest/dev/serv-side-encryption . html**](https://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html)
*   [**https://docs . AWS . Amazon . com/Amazon S3/latest/dev/server logs . html**](http:// https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html)
*   [**https://docs . AWS . Amazon . com/Amazon S3/latest/user-guide/server-access-logging . html**](http:// https://docs.aws.amazon.com/AmazonS3/latest/user-guide/server-access-logging.html)

[**Download**](https://github.com/Appliscale/cloud-security-audit)