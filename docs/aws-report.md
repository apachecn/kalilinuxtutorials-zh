# AWS 报告-分析亚马逊资源的工具

> 原文：<https://kalilinuxtutorials.com/aws-report/>

[![AWS Report – Tool For Analyzing Amazon Resources](img/864e832228850b0cec6121a591a31c4b.png "AWS Report – Tool For Analyzing Amazon Resources")](https://1.bp.blogspot.com/-Dq4m-YrQX-A/XhHxW1BEEAI/AAAAAAAAERU/RIvsUTcH6xYwwS6Ebl10OYJubtRp2z5ZACLcBGAsYHQ/s1600/AWS%25281%2529.png)

AWS Report 是一个分析亚马逊资源的工具，让我们看看它的一些特性；

*   根据创建日期搜索 iam 用户
*   公共搜索桶
*   使用 0.0.0.0/0 的入站规则搜索安全组
*   搜索已分离的弹性 ip
*   可用的搜索卷
*   允许公共搜索 ami
*   搜索 internet 网关已分离

**也可阅读-[nmapAutomator:可以在后台运行的脚本](https://kalilinuxtutorials.com/nmapautomator/)**

**安装要求**

**pip 3 install–user-r requirements . txt**

**环境变量**

IAM_MAX_ACCESS_KEY_AGE 默认为 60 天。

**用途**

**用法:AWS _ report . py[选项]**

**选项:**
**–S3**搜索存储桶 S3
**–iam**基于创建日期搜索 iam 用户
**–SG**搜索入站规则为 0.0.0.0 的安全组
**–elastic IP**搜索未关联的弹性 IP
**–volumes**搜索可用卷
**–ami**搜索 互联网网关分离
**–区域文本**定义资源的区域
**–帮助**显示此消息并退出。

**例题**

**python 3 AWS _ report . py–S3
python 3 AWS _ report . py–iam
python 3 AWS _ report . py–owner 296193067842–ami**

**在 Docker 中运行**

**docker run-it-e AWS _ ACCESS _ KEY _ ID = you-ACCESS-KEY-e AWS _ SECRET _ ACCESS _ KEY = you-SECRET-KEY gmd utra/AWS-report–S3**

[**Download**](https://github.com/gmdutra/aws-report)