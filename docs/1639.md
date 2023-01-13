# Leonidas:云中的自动攻击模拟，包括检测用例

> 原文：<https://kalilinuxtutorials.com/leonidas/>

[![Leonidas : Automated Attack Simulation In The Cloud, Complete With Detection Use Cases](img/d110faaf1dc91196fdd8891b91199c8a.png "Leonidas : Automated Attack Simulation In The Cloud, Complete With Detection Use Cases")](https://1.bp.blogspot.com/-6dwUazDCGzk/X7LirnHH5yI/AAAAAAAAH_o/RJOeohf_eUMJf9heFGgusefQxlQir9PTQCLcBGAsYHQ/s728/Leonidas%25281%2529.png)

这是包含 **Leonidas** 的存储库，这是一个在云中执行攻击者动作的框架。它提供了一种基于 YAML 的格式，用于定义云攻击者策略、技术和程序(TTP)及其相关的检测属性。这些定义可以被编译成:

*   一个 web API 将每个测试用例公开为一个单独的端点
*   探测的适马法则([https://github.com/Neo23x0/sigma](https://github.com/Neo23x0/sigma))
*   文档——参见[http://detectioninthe.cloud/](http://detectioninthe.cloud/)中的示例

**部署 API**

API 通过 AWS-native CI/CD 管道部署。这方面的说明可以在[部署列奥尼达](https://github.com/FSecureLABS/leonidas/blob/master/docs/deploying-leonidas.md)中找到。

**使用 API**

API 是通过由 API 密钥保护的 web 请求来调用的。有关使用 API 的详细信息，请参见[使用 Leonidas](https://github.com/FSecureLABS/leonidas/blob/master/docs/using-leonidas.md)

**就地安装发电机**

要构建文档或适马规则，您需要在本地安装生成器。您可以通过以下方式做到这一点:

【T2`cd generator`
`poetry install`

**生成适马规则**

适马规则可以按如下方式生成:

`**poetry run ./generator.py sigma**`

规则将出现在`./output/sigma`中

**生成文档**

文档生成如下:

`**poetry run ./generator.py docs**`

这将产生在`output/docs`可用的文档的降价版本。这可以上传到现有的基于 markdown 的文档系统，或者可以使用以下内容来创建文档的美化 HTML 版本:

【T2`cd output`
`mkdocs build`

这将创建一个包含 HTML 站点的`**output/site**`文件夹。也可以通过在同一个文件夹中运行`**mkdocs serve**`在本地查看。

**编写定义**

这些定义以基于 YAML 的格式编写，下面提供了一个例子。关于如何编写这些的文档可以在[编写定义](https://github.com/FSecureLABS/leonidas/blob/master/docs/writing-definitions.md)中找到

```
---
name: Enumerate Cloudtrails for a Given Region
author: Nick Jones
description: |
  An adversary may attempt to enumerate the configured trails, to identify what actions will be logged and where they will be logged to. In AWS, this may start with a single call to enumerate the trails applicable to the default region.
category: Discovery
mitre_ids:
  - T1526
platform: aws
permissions:
  - cloudtrail:DescribeTrails
input_arguments:
executors:
  sh:
    code: |
      aws cloudtrail describe-trails
  leonidas_aws:
    implemented: True
    clients:
      - cloudtrail
    code: |
      result = clients["cloudtrail"].describe_trails()
detection:
  sigma_id: 48653a63-085a-4a3b-88be-9680e9adb449
  status: experimental
  level: low
  sources:
    - name: "cloudtrail"
      attributes:
        eventName: "DescribeTrails"
        eventSource: "*.cloudtrail.amazonaws.com"
```