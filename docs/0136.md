# scout 2–用于 AWS 环境的安全审计工具

> 原文：<https://kalilinuxtutorials.com/scout2-security-auditing-aws/>

Scout2 是一个安全工具，让 AWS 管理员评估其环境的安全状况。Scout2 使用 AWS API 收集配置数据进行人工检查，并自动突出显示高风险区域。Scout2 不会在网上浏览大量网页，而是自动提供攻击面的清晰视图。

**注意:** Scout2 是稳定的，并得到了积极的维护，但许多特性和内部结构可能会发生变化。因此，请耐心等待我们找到时间来改进这个工具。随意报告一个错误的详细信息(*例如*使用“–debug”参数的控制台输出)，请求一个新特性，或者发送一个 pull 请求。

**也读 [后知后觉——分析网页神器的工具 Chrome 浏览器&基于 Chrome 的应用](https://kalilinuxtutorials.com/hindsight-chrome-chromium-applications/)**

## **Scout2 安装** 

**通过 pip 安装:**

```
$ pip install awsscout2
```

从源安装:

```
$ git clone https://github.com/nccgroup/Scout2
$ cd Scout2
$ pip install -r requirements.txt
$ python setup.py install
```

## **计算资源**

Scout2 是一个多线程工具，在运行时获取并在内存中存储 AWS 帐户的配置设置。预计该工具将在任何现代笔记本电脑或同等虚拟机上顺利运行。在计算资源有限的 VM(如 t2.micro 实例)中运行它并不是我们想要的，很可能会导致进程被终止。

## **Python**

它是用 Python 编写的，支持以下版本:

*   Two point seven
*   Three point three
*   Three point four
*   Three point five
*   Three point six

## **AWS 凭证**

要运行它，您需要有效的 AWS 凭证(*例如*访问密钥 id 和秘密访问密钥)。与这些凭证相关联的角色或用户帐户需要对许多服务中的所有资源具有只读访问权限，这些服务包括但不限于 CloudTrail、EC2、IAM、RDS、Redshift 和 S3。

为了授予必要的权限，可以将以下 AWS 托管策略附加到主体:

*   只读访问
*   安全性审计

## **遵守 AWS 的可接受使用政策**

使用此功能不需要 AWS 用户完成并提交 AWS 漏洞/渗透测试申请表。Scout2 只执行 AWS API 调用来获取配置数据和识别安全漏洞，这不被视为安全扫描，因为它不会影响 AWS 的网络和应用程序。

## **用途**

在执行了许多 AWS API 调用之后，Scout2 将创建一个本地 HTML 报告，并在默认浏览器中打开它。

使用已经配置为使用 AWS CLI、boto3 或其他 AWS SDK 的计算机，您可以使用以下命令来使用 Scout2:

```
$ Scout2
```

**注意:**具有 IAM 角色的 EC2 实例符合此类别。

如果在中配置了多个配置文件。AWS/凭据和。aws/config 文件，您可以使用以下命令指定要使用的凭据:

```
$ Scout2 --profile <PROFILE_NAME> 
```

如果您有一个包含 API 访问密钥 ID 和密码的 CSV 文件，您可以使用以下命令运行 Scout2:

```
$ Scout2 --csv-credentials <CREDENTIALS.CSV> 
```

## **高级文档**

以下命令将提供可用命令行选项的列表:

```
$ Scout2 --help
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/nccgroup/Scout2#installation)