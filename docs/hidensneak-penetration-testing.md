# hideNsneak——用于短暂渗透测试的 CLI

> 原文：<https://kalilinuxtutorials.com/hidensneak-penetration-testing/>

**hideNsneak** 应用程序通过提供一个接口来快速部署、管理和关闭各种云服务，从而帮助渗透测试人员管理攻击基础设施。这些包括虚拟机、域前端、Cobalt Strike 服务器、API 网关和防火墙。

## **hideNsneak 概述**

hideNsneak 提供了一个简单的接口，允许渗透测试人员构建短暂的基础设施——一个需要最小开销的基础设施。hideNsneak 可以:

*   `deploy`、`destroy`和`list`

1.  通过 EC2 和数字海洋的云实例(谷歌云、Azure 和阿里云即将推出)
2.  API 网关(AWS)
3.  通过 AWS Cloudfront 和 Google Cloud Functions 实现的域前端(Azure CDN 即将推出)

*   通过基础设施的代理
*   部署 C2 重定向器
*   发送和接收文件
*   经由 NMAP 的端口扫描
*   远程安装 Burp Collab、Cobalt Strike、Socat、LetsEncrypt、GoPhish 和 SQLMAP
*   与团队合作团队

## **本地运行**

1.0 版的一些披露:

*   此时，所有主机都假定为`Ubuntu 16.04 Linux`。
*   安装在您的本地系统上完成(仅限 Linux 和 Mac)。将来，我们希望添加一个 docker 容器来减少初始设置时间
*   目前仅有的 vps 提供商是 AWS 和数字海洋
*   你需要确保安装了 go。说明可以在[这里](https://golang.org/doc/install)找到
*   必须设置 GOPATH 环境变量

1.  在`us-east-1`中创建新的 AWS S3 存储桶
    *   请确保这不是公共的，因为它将保存您的地形状态
2.  `go get github.com/rmikehodges/hideNsneak`
3.  `cd $GOPATH/src/github.com/rmikehodges/hideNsneak`
4.  `./setup.sh`
5.  `cp config/example-config.json config/config.json`
    *   填写数值
    *   至少需要 aws_access_id、aws_secret_key、aws_bucket_name、public_key、private_key、ec2_user 和 do_user
    *   在同一状态下工作的所有操作员必须在所有相同的字段中填写配置值
    *   每个操作员的私钥和公钥必须相同
6.  现在您可以通过运行`./hidensneak [command]`来使用该程序

**也读作[door 404——door 404 是开源项目](https://kalilinuxtutorials.com/door404/)**

## **命令**

*   `**hidensneak help**`–>随时运行该命令以获取可用命令
*   **`hidensneak instance deploy`**
*   **`hidensneak instance destroy`**
*   `**hidensneak instance list**`
*   `**hidensneak api deploy**`
*   `**hidensneak api destroy**`
*   `**hidensneak api list**`
*   `**hidensneak domainfront enable**`
*   `**hidensneak domainfront disable**`
*   `**hidensneak domainfront deploy**`
*   **T2`hidensneak domainfront destroy`**
*   `**hidensneak domainfront list**`
*   `**hidensneak firewall add**`
*   **`hidensneak firewall list`**
*   **`hidensneak firewall delete`**
*   **`hidensneak exec command -c`**
*   **`hidensneak exec nmap`**
*   **`hidensneak exec socat-redirect`**
*   **`hidensneak exec cobaltstrike-run`**
*   **`hidensneak exec collaborator-run`**
*   **`hidensneak socks deploy`**
*   **`hidensneak socks list`**
*   **`hidensneak socks destroy`**
*   **`hidensneak socks proxychains`**
*   **`hidensneak socks socksd`**
*   **`hidensneak install burp`**
*   **`hidensneak install cobaltstrike`**
*   **`hidensneak install socat`**
*   **`hidensneak install letsencrypt`**
*   **`hidensneak install gophish`**
*   **`hidensneak install nmap`**
*   **`hidensneak install sqlmap`**
*   **`hidensneak file push`**
*   **`hidensneak file pull`**

对于所有命令，您可以在其中任何一个命令之后运行`--help`,以获得使用什么标志的指导。

## **组织**

*   **`_terraform`**–>地形模块
*   `**_ansible**`–>可能的角色和行动手册
*   `**_assets**`–>本项目美丽的随机资产
*   `**_cmd**`–>前端接口包
*   `**_deployer**`–>后端命令和结构
*   `**main.go**`–>奇迹发生的地方

## **IAM 权限**

谷歌域名前置

*   应用引擎 API 已启用
*   启用云函数 API
*   项目编辑或更高权限

## **杂项**

所有 AWS 区域中的默认安全组`hideNsneak`都是完全开放的。所有实例都配置了`iptables`,以便在供应时只允许端口 22/tcp。

如果您的程序开始抛出 terraform 错误，表明没有找到资源，那么您可能需要删除有问题的 terraform 资源。您可以通过运行以下命令来实现这一点:

`**cd $GOPATH/src/github.com/rmikehodges/hideNsneak/terraform**`

`**terraform state rm <name of problem resource>**`

如果该资源仍然存在，则需要手动清理。

## **故障排除**

错误:`module name here`的配置不存在；所有操作都需要提供者配置块

这通常是由于遗留在旧部署状态中的工件。以下是如何从您的状态中移除这些工件的说明。如果它们是实时资源，则需要通过云提供商的管理面板手动销毁。

*   `**cd $GOPATH/src/github.com/rmikehodges/hideNsneak/terraform**`
*   **`terraform state rm <module or resource name>`**

错误:错误锁定状态:获取状态锁时出错:ConditionalCheckFailedException:条件请求失败状态代码:400，请求 ID:p 7 bum 7 na 56 lqejqc 20 a3 se 2 sovvvv4 qn so 5 aemvjf 66 q 9 asuaaajg 锁信息:ID:4919d 588-6b 29-4a a7-d917-2 BCB 67 c 14 ab 4

如果在另一个用户完成部署后这种情况没有消失，那么这通常是由于 Terraform 在遇到错误时没有自动解锁您的状态。这可以通过运行以下命令来解决:

*   `**terraform force-unlock <ID> $GOPATH/src/github.com/rmikehodges/hideNsneak/terraform**`

请注意，这将解锁该状态，因此可能会对该状态中发生的任何其他写入产生不利影响，因此请确保您的其他用户在运行此操作时不会主动部署/销毁任何内容。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/rmikehodges/hideNsneak)