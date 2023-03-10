# PurpleCloud:一个小型活动目录测试实验室在云中的基础设施代码(IaC)部署

> 原文：<https://kalilinuxtutorials.com/purplecloud/>

[![PurpleCloud : An Infrastructure As Code (IaC) Deployment Of A Small Active Directory Pentest Lab In The Cloud](img/c7845d88d81a66c30e6254ca07886342.png "PurpleCloud : An Infrastructure As Code (IaC) Deployment Of A Small Active Directory Pentest Lab In The Cloud")](https://1.bp.blogspot.com/-w0d8DtsaGqY/X1tv9W3_u1I/AAAAAAAAHgw/5VyOWNXeVogjYwFv27NCOC2LqjdCoeZewCLcBGAsYHQ/s728/ss-logged-in%25281%2529.png)

Pentest 小型活动目录域的网络范围。在 Azure cloud 中构建您自己的 Pentest/Red Team/Cyber 系列的自动化模板！ **Purple Cloud** 是一个小型的 Active Directory 企业部署，使用 Terraform / Ansible 剧本模板自动部署在 Azure 中。紫色云还包括一个对手节点，实现为一个 docker 容器，可通过 RDP 远程访问。

**有趣的事实**

*   部署可通过 RDP 访问的 pentest 对手 Linux 虚拟机和 Docker 容器(AriaCloud)
*   部署一(1)个 Windows 2019 域控制器和三(3)个 Windows 10 Pro 端点
*   自动将三台 Windows 10 计算机加入 AD 域
*   使用 Terraform 模板在 Azure 中自动部署虚拟机
*   Terraform 模板编写可定制的可行剧本配置
*   如果你喜欢生成成千上万的模拟用户[https://github.com/davidprowe/BadBlood](https://github.com/davidprowe/BadBlood)，自动上传坏蛋(但不安装)
*   部署后 Powershell 脚本在 2019 域控制器上提供三个域用户，并且可以为更多用户进行定制
*   域用户:olivia(域管理员)；lars(域用户)；域名用户
*   所有域用户密码:密码 123
*   域:RTC。当地的
*   域管理员凭据:RTCAdmin:Password123
*   部署四个 IP 子网
*   故意部署不安全的 Azure 网络安全组(NSG ),允许来自公共互联网的 RDP、WinRM (5985、5986)和 SSH。按照你的要求保护好这个。WinRM 用于自动调配主机。
*   部署后 Powershell 脚本，在每个 Windows 10 Pro 端点上添加注册表项，以自动将每个用户名作为各自的用户登录到域中。该功能模拟了一个真实的广告环境，其中的工作站具有交互式域登录。当你试图进入 RDP 端点时，模拟对手遇到了:

![PurpleCloud : An Infrastructure As Code (IaC) Deployment Of A Small Active Directory Pentest Lab In The Cloud](img/c7845d88d81a66c30e6254ca07886342.png "PurpleCloud : An Infrastructure As Code (IaC) Deployment Of A Small Active Directory Pentest Lab In The Cloud")

**AriaCloud Pentest 容器–自动部署**

这个 repo 现在包括一个 Terraform 模板和一个 Ansible 剧本，可以自动将 AriaCloud 部署到 Azure VM 中，并通过 RDP 进行远程访问。您还可以从该 repo 中独立部署 AriaCloud。对于此选项，导航到 **aria-cloud** 目录并查看自述文件。有关 AriaCloud docker 容器和包含的 pentest 工具的更多信息，请导航至 https://github.com/iknowjason/AriaCloud 的。

**紫云部署指令**

**注:**在 Ubuntu Linux 20.04 上测试

**要求:**

*   Azure 订阅
*   Terraform:在 v0.12.26 上测试
*   Ansible:于 2.9.6 测试

**安装步骤**

**注:**在 Ubuntu 20.04 上测试

*   **步骤 1:** 在您的 Linux 系统上安装 Terraform 和 Ansible

为您的平台下载并安装 Terraform->[https://www.terraform.io/downloads.html](https://www.terraform.io/downloads.html)

**安装 Ansible**

**$ sudo apt-get install ansi ble**

*   **步骤 2:** 在你的 Azure 订阅上设置一个 Azure 服务主体，允许 Terraform 自动执行你的 Azure 订阅下的任务

按照这个微软链接中的确切说明:[https://docs . Microsoft . com/en-us/azure/developer/terra form/getting-started-cloud-shell](https://docs.microsoft.com/en-us/azure/developer/terraform/getting-started-cloud-shell)

这是基于上面的链接运行的两个基本命令:

**az ad sp create-for-RBAC–role = " Contributor "-scopes = "/subscriptions/**

下面这个命令。在我的测试中，我需要使用“所有者”的角色，而不是“贡献者”。默认的 Microsoft 文档显示导致错误的“参与者”角色。

az 登录-服务-负责人-u<service_principal_name>-p "<service_principal_password>"-租户"<service_principal_tenant>"</service_principal_tenant></service_principal_password></service_principal_name>

请注意以下内容，我们接下来将使用这些内容来配置我们的 Terraform Azure 提供程序:

**subscription _ id = " "
client _ id = " "
client _ secret = " "
tenant _ id = " "**

*   **第三步:**克隆此回购

**git 克隆 https://github . com/iknowjason/purplecloud . git**

**步骤 4:** 使用您最喜欢的文本编辑器，编辑与您的 Azure 服务主体凭证相匹配的 Azure 资源提供者的 terraform.tfvars 文件

**CD purple cloud/deploy
VI terraform . TF vars**

在 terraform.tfvars 文件中编辑这些参数:

**subscription _ id = " "
client _ id = " "
client _ secret = " "
tenant _ id = " "**

您的 terraform.tfvars 文件应该类似于此，但具有您自己的 Azure 服务主体凭据:

subscription _ id = " aa 9d 8 c 9 f-34 C2-6262-89ff-3c 67527 C1 b 22 "
client _ id = " 7e 9 C2 CCE-8bd 4-887d-B2B 0-90 cd1e 6 e 4781 "
client _ secret = ":+O $+adfafdaF-？%:.？d/eyqlk 6 po 9 `| E<["
tenant _ id = " 8b 6817d 9-f209-2071-8f4f-cc 03332847 CB "

*   **步骤 5:** 运行命令初始化 terraform 并应用资源计划

**$ CD purple cloud/deploy
$ terra form init
$ terra form apply-var-file = terra form . TF vars-auto-approve**

这将启动 Terraform 自动部署计划

*   第六步:可选:从 C:\terraform 目录中解压并运行 bad blood(【https://github.com/davidprowe/BadBlood】T2)

**已知问题或缺陷**

有些问题需要我根据时间进行调试和解决。下面提到了它们的解决方法。

有时，其中一个资源调配步骤对 DC 不起作用。terraform 模块调用 Ansible Playbook，后者运行 Powershell 脚本来添加域用户。运行这些步骤时，错误将如下所示:

```
module.dc1-vm.null_resource.provision-dc-users (local-exec): TASK [dc : debug] **************************************************************
module.dc1-vm.null_resource.provision-dc-users (local-exec): ok: [52.255.151.90] => {
module.dc1-vm.null_resource.provision-dc-users (local-exec):     "results.stdout_lines": [
module.dc1-vm.null_resource.provision-dc-users (local-exec):         "WARNING: Error initializing default drive: 'Unable to find a default server with Active Directory Web Services ",
module.dc1-vm.null_resource.provision-dc-users (local-exec):         "running.'."
module.dc1-vm.null_resource.provision-dc-users (local-exec):     ]
module.dc1-vm.null_resource.provision-dc-users (local-exec): } 
```

如果发生这种情况，您可以切换到 **modules/dc1-vm** 目录，并立即运行 ansible playbook 命令，如 README 中所示。ANSIBLE.txt: `**ansible-playbook -i hosts.cfg playbook.yml**`

如果您在配置 Windows 10 端点之前运行此命令，它们将正常运行。如果整个脚本运行后您看到此错误，那么您需要在 Windows 服务器和所有端点上运行 Ansible 剧本。

有时对手会抛出这个错误:

module . adversar 1-VM . null _ resource . ansi ble-deploy(local-exec):fatal:[40 . 121 . 138 . 118]:失败！=> {"changed": false，" msg ":"更新 apt 缓存失败:" }

要解决该问题，请转到**modules/adversar 1-VM**目录，并运行 README 中显示的 Ansible Playbook 命令。ANSIBLE.txt:

ansi ble _ HOST _ KEY _ CHECKING = False ansi ble-playbook-I ./hosts . CFG–私钥 ssh_key.pem。/playbook.yml

有时，Windows 10 端点不会通过注册表项自动登录到域中。我发现这个问题是由于域控制器创建的时间问题。创建三个用户的 powershell 脚本运行不正确。要解决这个问题，只需在每个模块目录中运行 Ansible 行动手册。以下内容应该可以解决问题:

$ cd../modules/dc1-VM/
$ ansi ble-playbook-I hosts . CFG playbook . yml

$ CD../win 10-VM-1/
$ ansi ble-playbook-I hosts . CFG playbook . yml

$ CD../win 10-VM-2/
$ ansi ble-playbook-I hosts . CFG playbook . yml

$ CD../win 10-VM-3/
$ ansi ble-playbook-I hosts . CFG playbook . yml

[**Download**](https://github.com/iknowjason/PurpleCloud)