# Poro:扫描 AWS 云环境中可公开访问的资产

> 原文：<https://kalilinuxtutorials.com/poro/>

[![](img/e60587b6ffc89d0c0287ead09bb5cb07.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjNt8dfemHEuOaNHKYGIKWIW44z1Zb12SWaBeAagFbLQcxP-sNaEeFTRuYUAEXwg8FWL9sqyLK9T0TLOjjdVZ-178hZe8VpGIfxqQyAhUVfCE6BR2UZsxX8h9Mb-gkbQ_QOgjCL5wxW_ouRQWH1zqsbWjK8P87-f8k6OQDtBwZSBMCC04psLLfJ0_pe/s728/1%20(1).png)

Poro 是一个扫描 AWS 环境中可公开访问的资产的工具

该工具涵盖的服务:

*   AWS ELB(消歧义)
*   API 网关
*   S3 水桶
*   RDS 数据库
*   EC2 实例
*   红移数据库

Poro 还使用–tag-key 和–tag-value 参数检查您指定的标记是否应用于已识别的公共资源。

## 先决条件

*   对上述服务具有只读访问权限的 AWS 帐户。
*   Python 3。X
*   请求> =2.22.0
*   boto3>=1.20
*   僵尸核心> = 1.20
*   启发> =1

## 用法

*   克隆此存储库
*   使用活动凭据配置您的环境-> aws 配置[sso]
*   运行 python poro . py[-h][–PROFILE PROFILE][–导出文件名][–详细][–标记密钥密钥][–标记值值]

**可选参数:
-h，–help 显示此帮助消息并退出
–PROFILE PROFILE 指定 aws 配置文件(默认为默认)
–export FILE _ NAME 指定要导出结果的文件名
–verbose，-v
–tag-KEY KEY 指定要检查的标记键是否存在于公共资源中
–tag-VALUE 指定要检查的标记值是否存在于公共资源中**

如果没有指定导出选项，Poro 将在执行结束时在 json 文件中打印扫描结果。

[**Download**](https://github.com/9rnt/poro)