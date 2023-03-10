# Terra guard:使用 Wire Guard 创建和破坏您自己的 VPN 服务

> 原文：<https://kalilinuxtutorials.com/terra-guard/>

[![Terra guard : Create And Destroy Your Own VPN Service Using Wire Guard](img/9b70d02e238ba2642c8c42f983c10970.png "Terra guard : Create And Destroy Your Own VPN Service Using Wire Guard")](https://1.bp.blogspot.com/-eU-BbOg2-Go/YPzl_BrvecI/AAAAAAAAKNU/1BWvkjbGICEHz9y8nreVa7sfWrsHkB2tACLcBGAsYHQ/s579/wireguard%2B%25281%2529.png)

Terra guard 的目标是使用 Wire Guard 简单地创建和破坏您自己的 VPN 服务。

**先决条件**

*   地形> = 1.0.0
*   答案> = 2.10.5

**如何部署**

**地形**

使用 sudo 运行是必要的，因为我们需要本地主机上的权限来安装包、配置网络接口和启动进程。

选择您的云提供商 **AWS** 、 **DigitalOcean** 并打开目录

您可以在**变量. tf** 中更改区域或键名

*   初始化 Terraform

**地形初始化**

*   计划我们的修改

**须藤地形图**

*   应用更改

**sudo terraform 应用**

*   对于数字海洋，您需要在**变量. tf** 或命令行中声明您的令牌(do_token):

**sudo terra form plan-var " do _ token = value "
sudo terra form apply-var " do _ token = value "**

**测试–检查 IP**

*   在没有 VPN 的情况下测试连接

**卷曲的 ipinfo.io/ip**

*   启动 VPN

**sudo system CTL start WG-quick @ wg0**

*   测试与 VPN 的连接

**卷曲的 ipinfo.io/ip**

[**Download**](https://github.com/P0ssuidao/terraguard)