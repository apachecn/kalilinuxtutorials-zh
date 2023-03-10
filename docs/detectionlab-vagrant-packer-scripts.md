# DetectionLab:用于构建实验室环境的漫游和打包脚本

> 原文：<https://kalilinuxtutorials.com/detectionlab-vagrant-packer-scripts/>

[![DetectionLab : Vagrant & Packer Scripts To Build A Lab Environment](img/fbf1111d2d94953305136327292b4a98.png "DetectionLab : Vagrant & Packer Scripts To Build A Lab Environment")](https://1.bp.blogspot.com/-3uVWglJe_-A/XdfLLsa3S3I/AAAAAAAADiw/hakjjxc5-Csom9fqbijTWLUWoSl3IzHSQCLcBGAsYHQ/s1600/DetectionLab%25281%2529.png)

通过预定的 CircleCI 工作流，DetectionLab 每周在周六进行测试，以确保构建通过。这个实验室是为防御者而设计的。它的主要目的是允许用户快速构建一个 Windows 域，该域预装了安全工具和一些关于系统日志配置的最佳实践。它可以很容易地进行修改以满足大多数需求，或者扩展以包括更多的主机。

**注意**:这个实验室没有经过任何方式的加固，使用默认的流浪者凭证运行。请不要将其连接或桥接到任何您关心的网络。这个实验室是故意设计成不安全的；它的主要目的是提供对每个主机的可见性和内省。

**也读作-[自定义报头:自动向整个 BurpSuite HTTP 请求添加新报头](https://kalilinuxtutorials.com/custom-header-burpsuite-http-requests/)**

**主要实验室特征**

*   微软高级威胁分析([https://www . Microsoft . com/en-us/cloud-platform/Advanced-Threat-Analytics](https://www.microsoft.com/en-us/cloud-platform/advanced-threat-analytics))安装在 WEF 机器上，轻量级 ATA 网关安装在 DC 上
*   Splunk 转发器是预安装的，并且所有索引都是预创建的。还预先配置了用于 Windows 的技术附件。
*   通过 GPO 设置自定义 Windows 审核配置，以包括命令行进程审核和其他操作系统级别的日志记录
*   [Palantir 的 Windows 事件转发](http://github.com/palantir/windows-event-forwarding)订阅和自定义频道已实施
*   Powershell 脚本日志记录已启用。所有日志都保存到`\\wef\pslogs`
*   osquery 安装在每台主机上，并预先配置为通过 TLS 连接到一个[机群](https://kolide.co/fleet)服务器。车队预先配置了来自 [Palantir 的 osquery 配置](https://github.com/palantir/osquery-configuration)的配置
*   Sysmon 是使用 SwiftOnSecurity 的开源配置安装和配置的
*   所有自动启动项目都通过 [AutorunsToWinEventLog](https://github.com/palantir/windows-event-forwarding/tree/master/AutorunsToWinEventLog) 记录到 Windows 事件日志中
*   SMBv1 审核已启用

**要求**

*   55GB 以上的可用磁盘空间
*   16GB 以上的内存
*   封隔器 1.3.2 或更新版本
*   流浪者 2.2.2 或更新版本
*   Virtualbox 或 VMWare Fusion/Workstation

**快速入门**

*   [AWS](https://github.com/clong/DetectionLab/wiki/Quickstart---AWS-(Terraform))
*   [苹果电脑](https://github.com/clong/DetectionLab/wiki/Quickstart---MacOS)
*   [窗户](https://github.com/clong/DetectionLab/wiki/Quickstart---Windows)
*   [Linux](https://github.com/clong/DetectionLab/wiki/Quickstart-Linux)

**从零开始建立检测实验室**

1.  确定您要使用哪个流浪者提供者。当前支持的提供商有:

*   Virtualbox(虚拟方块)
*   VMware 工作站和融合
    *   注意:Virtualbox 是免费的， [VMWare 桌面流浪者插件](https://www.vagrantup.com/vmware/#buy-now)是 80 美元，需要与 VMWare 一起使用流浪者。

目前有三种方式来建立实验室:

*   **推荐**:使用[流浪云](https://app.vagrantup.com/detectionlab)上托管的盒子。这种方法总共需要 **~2 个小时**来下载盒子和配置实验室。
*   使用 Packer 自己制作盒子。这种方法需要大约 4 个小时来构建机箱，另外需要大约 90-120 分钟来配置它们，总共需要 **5-6 个小时**。
*   [使用 Terraform](https://github.com/clong/DetectionLab/blob/master/Terraform/README.md) 在 AWS 中配置实验室。实验室可以在 **30 分钟**内上线。

如果你选择使用流浪云上的盒子，你可以跳过第 2 步和第 3 步。如果您不信任预构建的盒子，我建议按照步骤 2 和 3 在您的机器上构建它们。

1.  `cd`到 Packer 目录，使用下面的命令构建 Windows 10 和 Windows Server 2016 盒子。每个建筑将需要大约 1 小时。据我所知，你一次只能造一个箱子。

$ CD detection lab/Packer
$ Packer build–only =[VMware | virtualbox]-iso windows _ 10 . JSON
$ Packer build–only =[VMware | virtualbox]-iso windows _ 2016 . JSON

1.  一旦两个盒子都构建成功，移动生成的盒子(。盒子文件)放在 Packer 文件夹中到盒子文件夹: **`mv *.box ../Boxes`**
2.  `**cd**`进入流浪目录:`**cd ../Vagrant**`，编辑`**Vagrantfile**`。将**`cfg.vm.box = "detectionlab/win2016"``cfg.vm.box = "detectionlab/win10`分别改为`cfg.vm.box = "../Boxes/windows_2016_<provider>.box"`****`cfg.vm.box = "../Boxes/windows_10_<provider>.box"`**。
3.  安装流浪-重装外挂: **`vagrant plugin install vagrant-reload`**
4.  **仅限 VMware:**

*   [购买 VMware 插件的许可证](https://www.vagrantup.com/vmware/index.html#buy-now)
*   用`**vagrant plugin install vagrant-vmware-desktop**`安装。
*   用`**vagrant plugin license vagrant-vmware-desktop <path_to_.lic>**`许可。
*   下载并安装 VMware 流浪者实用程序:[https://www.vagrantup.com/vmware/downloads.html](https://www.vagrantup.com/vmware/downloads.html)

1.  确保您在 base DetectionLab 文件夹中，并运行`**./build.sh**` (Mac & Linux)或`**./build.ps1**` (Windows)。该脚本将执行以下操作:

*   设置记录器主机。该主机将运行 [Fleet](https://kolide.co/fleet) osquery manager 和全功能预配置 Splunk 实例。
*   设置 DC 主机并将其配置为域控制器
*   预配 WEF 主机，并将其配置为服务器 OU 中的 Windows 事件收集器
*   供应 Win10 主机，并将其配置为工作站 OU 中的计算机

1.  构建日志将作为`**vagrant_up_<host>.log**`出现在`**Vagrant**`文件夹中。如果提出问题，请将日志内容粘贴到要点中，以帮助调试工作。
2.  在浏览器中导航到[https://192 . 168 . 38 . 105:8000](https://192.168.38.105:8000)以访问 logger 上的 Splunk 实例。默认凭据是 admin:changeme(您可以在下一个屏幕上选择更改它们)
3.  在浏览器中导航至[https://192 . 168 . 38 . 105:8412](https://192.168.38.105:8412)以访问 logger 上的车队服务器。默认凭据是 admin:admin123#。查询包预先配置了来自[palantir/osquery-configuration](https://github.com/palantir/osquery-configuration)的查询。

[**Download**](https://github.com/clong/DetectionLab)