# Ad-Honeypot-Autodeploy:完全自动地为 RDP 蜜罐部署一个小的、故意不安全的、易受攻击的 Windows 域

> 原文：<https://kalilinuxtutorials.com/ad-honeypot-autodeploy/>

[![](img/4d53cc9d716ee2b6ae59b2b600ef06bb.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhBrYl4BktWjETplfqDuGryAKJYtTftkqnel_3JuyrenMLXyUzEimVid1OtQ5ebekqxCgIepp_prvwL5D_m3uICCuvxRI2Vih2rIfor5GjImAOiwWjNHt6l6lCMFbZcquIGhJtr_MUDPDtqjmVEI4Eb12o_UZwxc9f3A9SCXtRIksZyV10eunhWBjG9=s728)

Ad-Honeypot-Autodeploy 一个为 RDP 蜜罐完全自动部署一个小的、故意不安全的、易受攻击的 Windows 域的工具。

使用带有 QEMU/KVM 的 libvirt 在自托管虚拟化上运行(但可以针对基于云的解决方案轻松定制)。

用于无痛苦地从零开始自动设置一个小的 Windows 域(无需用户交互),用于 RDP 蜜罐测试。

具有一个域控制器，一台台式计算机和一个配置的灰色日志服务器，用于记录坏人的行动。

**自动部署阶段**

1.  打包程序:下载必要的安装介质，并自动设置基本虚拟机映像。
2.  Terraform:使用打包程序准备的虚拟机映像供应 libvirt 虚拟化基础架构(网络+虚拟机)。
3.  Ansible:自动配置基础架构(DC、桌面、Graylog)，无需用户交互。

通过 Packer+Terraform+Ansible 管道后，配置的 Windows 域应该启动并运行，您可以将桌面的 RDP 服务连接到公共互联网，让我们通过 Graylog 监视事件。

**特色**

运行系统的特点是:

*   Windows Server 2016 作为域控制器
*   作为域计算机的 Windows 10 台式机(2004 版)
*   在 Ubuntu 18.04 LTS 上作为日志收集器运行的 Graylog 3.3(开源版)
*   使用虚拟驱动程序获得最佳性能
*   已启用 RDP 和 WinRM 服务
*   随机用户填充的 Windows Active Directory
*   在域计算机上安装并运行的 Sysmon(来自 Windows Sysinternals)
*   NXLog 收集器运行域计算机并将日志转发到 Graylog
*   为 IP 地址配置了 Graylog GeoIP 查找表和管道(用于显示无效 RDP 登录尝试的地图)
*   RDP 袭击的灰色世界地图

**主机系统需求**

虚拟化需要您的主机系统的一些功能:

*   大约 80 GB 的磁盘空间用于来宾计算机的基本映像和稀疏映像。
*   来宾机器至少需要 3 x 4 GB 内存(由于过量使用，运行时可能需要不到 12 GB 的内存)
*   安装了带有 QEMU/KVM 的最新 lib virt(Ubuntu 18.04 LTS 版中的官方当前包应该可以工作)
*   用于 Ansible 的 Python 3(最好带有 venv)

在 Ubuntu 18.04 LTS 主机上测试。

**安装和使用**

首先，克隆回购:

**git 克隆 https://github.com/tothi/ad-honeypot-autodeploy
CD 广告-蜜罐-自动部署**

在启动封隔器之前，设置初始密码:

**。/init_passwords.sh**

**打包机**

现在构建初始图像。

**cd 打包机**

Windows Server 2016 和 Ubuntu 安装介质要通过打包脚本下载。VirtIO 需要通过附加的 get-virtio.sh 脚本下载:

**。"获取能量"**

Windows 10 应该通过获取临时下载链接并保存到 ISO 文件夹来手动下载。可以从这里获得下载链接。选择英语(国际)、64 位版本，并将 ISO 保存到`**ISO/Win10_2004_EnglishInternational_x64.iso**`。

要在 Graylog 的世界地图上绘制 IP 位置，需要 MaxMind GeoIP 数据库。不幸的是，由于许可条款，它不能被重新分发，所以你必须从 MaxMind 网站手动下载(注册后)。免费的 GeoLite2 版本应该可以工作，获得 MMDB 格式的“GeoLite2 城市”数据库(下载 GZIP 和 untar)并将其放在`**resources/GeoLite2-City.mmdb**`。

如果您没有 Packer，请从 packer.io 站点获取最新版本(下载预编译的二进制文件)或尝试将 [](https://learn.hashicorp.com/tutorials/terraform/install-cli) Hashicorp 存储库添加到您的打包系统中(对 Terrafrom 也很有用)。

如果您正在重建映像，请不要忘记清理以前的构建:

**rm -fr 输出 _***

如果您想重新下载图像，请删除 packer_cache:

**rm -fr packer_cache**

完成这些准备步骤后，并行运行封隔器:

**。/packer-build-all.sh**

图像应该在合理的时间内准备好(大约 20-30 分钟，取决于您的主机硬件电源)。

**地形**

现在可以使用 Terraform 部署基础设施。

如果您没有 Terraform (>=0.13)，请获取它(查看上面 Packer 中的安装方法)。

还需要 Terraform provider for libvirt，从 github releases 页面获取适当的二进制文件，并查找 Terraform v13 迁移说明，以便正确安装。

输入 Terraform 文件夹:

**cd../地形**

初始化工作目录(仅在首次使用时需要):

**地形初始化**

构建并启动基础设施(“应用变更”):

**地形应用**

过了一会儿(大约 2-3 分钟)，网络和虚拟机就启动并运行了。

警告:你应该注意保护你的私人网络。这里提供的 terraform config (main.tf)只是包含一个我自己的测试环境的自定义防火墙规则(拦截来自 192.168.3.0/24 蜜罐网络的 192.168.0.0/16 目的地流量)。

接下来是配置阶段。

**Ansible**

进入 ansible 文件夹:

**cd../ansible**

推荐的安装方法是在 Python venv 虚拟化环境中安装最新的 Ansible 以及一些必需的附加依赖项:

**python3 -m venv venv
。。/venv/bin/activate
pip 安装 ansible pywinrm faker**

以后使用时，只需通过以下方式激活静脉阀

**。。/venv/bin/activate**

如果在您当前的会话中不再需要它，只需`**deactivate**`。

您应该将一个文件名为`**id.pub**`的 SSH 公钥放入 ansible 文件夹，以便使用 Ubuntu 用户访问 Ubuntu Graylog 机器(ansible 会将它添加到`**~ubuntu/.ssh/authorized_keys**`)。

`**wordlist.txt**`文件包含一些可定制的已填充域用户的密码(故意设置为弱密码)。

运行配置阶段:

ansi ble-playbook-I hosts setup-domain . yml-v

20-25 分钟后，一切准备就绪。

**部署好的系统**

| 主机名 | IP 地址；网络地址 | 操作系统 | 作用 |
| --- | --- | --- | --- |
| dc1 | 192.168.3.100 | Windows Server 2016 | 域控制器 |
| 桌面 12 | 192.168.3.112 | windows 10(2004 版) | 域成员工作站 |
| 灰色日志 | 192.168.3.191 | Ubuntu 18.04 lt | 灰色日志服务器 |

根据 libvirt 网络配置(NAT)，主机可以访问公共互联网(如果您的主机系统允许)。

可以通过主机系统访问主机。实际上，使用 SSH socks 隧道和 proxychains 进行 RDP 或 WinRM 访问是非常舒适的。

例如，如果您的 libvirt 主机 IP 是 192.168.0.10，那么通过

**ssh 192 . 168 . 0 . 10-d5000-ntv**

并访问 Windows 10 桌面(使用为:5000 隧道配置的适当的`**/etc/proxychains.conf**`):

**代理链 xfreerdp /v:192.168.3.112 /u:管理员**

或者，通过 SSH ProxyJump 和自定义转发隧道在 Graylog Ubuntu 服务器上本地访问 Graylog web 界面 listen on:9000:

**ssh-j 192 . 168 . 0 . 10 Ubuntu @ 192 . 168 . 3 . 191-ntv-l 9000:127 . 0 . 0 . 1:9000**

然后打开 URL `**http://localhost:9000**`，你就到达了 Graylog web 界面。

要激活 RDP 蜜罐，只需允许公共访问 192.168.3.112:3389(例如在您的路由器上配置一些端口转发，在主机上配置 iptables 规则；我的助手脚本是 rdp_public.sh)继续看 Graylog。😉

[**Download**](https://github.com/tothi/ad-honeypot-autodeploy)