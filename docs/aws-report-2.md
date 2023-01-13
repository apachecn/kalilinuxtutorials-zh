# AWS 报告:分析亚马逊资源的工具

> 原文：<https://kalilinuxtutorials.com/aws-report-2/>

[![AWS Report : A Tool For Analyzing Amazon Resources](img/f12591cba5780e4ba7709564d02d79b0.png "AWS Report : A Tool For Analyzing Amazon Resources")](https://1.bp.blogspot.com/-pEnypWKkXgY/XzvkkdeLOnI/AAAAAAAAHYE/VQ_4IfwK8xYy9Vt-7Z1COQaqWv1Qz-UtQCLcBGAsYHQ/s728/aws%25281%2529.png)

**AWS Report** 是分析亚马逊资源的工具。

**使用 PIP 安装**

**pip 安装 AWS 报告**

**特性**

基于创建日期搜索 IAM 用户
搜索桶公共
基于规则搜索安全性，默认为 0.0.0.0/0
搜索弹性 ip 分离
搜索可用卷
搜索具有许可的 ami 公共
搜索互联网网关分离

**选项**

**AWS _ report . py[OPTIONS]**

**选项:**
–s3 中的 S3 搜索桶 public
–iam Search iam users based on creation date
–iam-max-age 使用 max-age 搜索 X 天前创建的用户
–SG Search security groups with inbound specific rule
–elastic IP Search elastic IP not associated
–volumes Search volumes available
–ami Search AMIs with permission public
–使用权限搜索 ami

**举例:**
python AWS report . py–S3
python AWS report . py–iam–owner 296192063842
python AWS report . py–iam–iam-max-age 60
python AWS report . py–SG–CIDR 192 . 168 . 1 . 0/24 或
python AWS report . py–SG(CIDR 默认值为 0。

[**Download**](https://github.com/bsd0x/awsreport)