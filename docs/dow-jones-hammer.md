# 道琼斯锤子:用云的力量保护云(AWS)

> 原文：<https://kalilinuxtutorials.com/dow-jones-hammer/>

[![Dow Jones Hammer : Protect The Cloud With The Power Of The Cloud(AWS)](img/3b74619f5b1b2f65fbe7db2b23dda55e.png "Dow Jones Hammer : Protect The Cloud With The Power Of The Cloud(AWS)")](https://1.bp.blogspot.com/-g3F70SUePfQ/XVroI5zOCJI/AAAAAAAACDo/PlHvJ1s8FEYxibzlY6dyVdT5Rbd2x6BEgCLcBGAs/s1600/Dow%2BJones%2BHammer%25281%2529.png)

**道琼斯锤子**是 AWS 的多账户云安全工具。它可以识别所有地区和客户的最受欢迎的 AWS 资源中的错误配置和不安全数据暴露。

道琼斯哈默拥有接近实时的报告能力(如 JIRA、Slack)向工程师提供快速反馈，并可以对一些错误配置进行自动补救。这有助于通过创建安全护栏来保护部署在云上的产品。

**安全特性**

*   [不安全的服务](https://dowjones.github.io/hammer/playbook2_insecure_services.html)
*   [S3 ACL 公共访问](https://dowjones.github.io/hammer/playbook1_s3_public_buckets_acl.html)
*   [S3 政策公众访问](https://dowjones.github.io/hammer/playbook5_s3_public_buckets_policy.html)
*   [IAM 用户非活动键](https://dowjones.github.io/hammer/playbook3_inactive_user_keys.html)
*   [IAM 用户键旋转](https://dowjones.github.io/hammer/playbook4_keysrotation.html)
*   [CloudTrail 日志问题](https://dowjones.github.io/hammer/playbook6_cloudtrail.html)
*   [EBS 未加密卷](https://dowjones.github.io/hammer/playbook7_ebs_unencrypted_volumes.html)
*   [EBS 公开快照](https://dowjones.github.io/hammer/playbook8_ebs_snapshots_public.html)
*   [RDS 公共快照](https://dowjones.github.io/hammer/playbook9_rds_snapshots_public.html)
*   [SQS 公共政策准入](https://dowjones.github.io/hammer/playbook10_sqs_public_policy.html)
*   [S3 未加密的桶](https://dowjones.github.io/hammer/playbook11_s3_unencryption.html)
*   [RDS 未加密实例](https://dowjones.github.io/hammer/playbook12_rds_unencryption.html)
*   [AMIs 公共访问](https://dowjones.github.io/hammer/playbook13_amis_public_access.html)

**又读-[no sqlmap:自动化 NoSQL 数据库枚举& Web 应用开发工具](https://kalilinuxtutorials.com/nosqlmap-enumeration-web-application-exploitation-tool/)**

**技术**

*   Python 3.6
*   AWS (Lambda、Dynamodb、EC2、SNS、CloudWatch、CloudFormation)
*   将（行星）地球化（以适合人类居住）
*   JIRA
*   松弛的

**运行测试**

使用以下命令运行测试:

**毒性**

[**Download**](https://github.com/dowjones/hammer/)