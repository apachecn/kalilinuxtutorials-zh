# 如何在 Windows 10 上安装 Ubuntu？

> 原文：<https://kalilinuxtutorials.com/ubuntu-windows-10/>

本文将为您提供在 Windows 10 操作系统上安装 Ubuntu 的分步指导。我们假设您的机器预装了 Windows 10 操作系统或较旧版本的 Microsoft Windows，如 Windows 8.1 或 8。

另请参阅:**[Kage–Metasploit meter preter 的图形用户界面&会话处理程序](https://kalilinuxtutorials.com/kage-metasploit-session-handler/)**

**安装**

首先，我们需要检查硬件使用情况。如果你的硬件使用 **UEFI** ，那么我们应该修改 **EFI** 设置并禁用**安全引导**功能，然后再继续。为了进行更改，请遵循以下步骤。

*   重启 Windows PC，选择**故障排除>高级选项>UEFI 固件选项设置>重启**
*   然后 **BIOS 设置**将打开，这将根据您的设置而变化
*   现在导航到**引导标签**并禁用**安全引导**。
*   您可能还需要**打开/关闭传统支持**。

如果系统安装在单个分区上，当您对硬件进行更改后，您需要在计算机硬盘上创建一个空闲空间。按照下面提到的步骤创建分区；

*   以管理员身份登录 Windows PC，点击**开始菜单** **- >** **命令提示符**(管理员)。
*   在命令提示符中，只需键入“ **diskmgmt.msc** ”，这将打开**磁盘管理**实用程序。然后右击你要分区的驱动器，选择**收缩卷**来调整分区大小。
*   在收缩驱动器上，输入要收缩的空间值(MB ),然后点击 **Shrink** 开始调整分区大小。
*   一旦调整了空间大小，您将在硬盘上看到一个新的**未分配空间**。
*   保留默认设置，重启电脑，继续安装 Ubuntu。

现在所有的预安装步骤都已完成，我们将开始安装过程。我们需要一个 Ubuntu ISO 文件，可以从 Ubuntu 的[网站](https://www.ubuntu.com/download/desktop)下载。

然后我们需要一个至少 4GB 存储空间的记忆棒来为 Ubuntu 创建一个可启动的 u 盘。你可以使用一个与 **UEFI** 兼容的 [Rufus](https://rufus.ie/) 工具为 Ubuntu 创建一个可启动的 u 盘。

一旦您完全下载并启动了 Rufus，在 Create a bootable disk using 部分，选择 ISO 映像并找到下载的 Ubuntu ISO 文件。

现在重新启动您的 windows PC 进入 BIOS，并启用从 USB 启动。现在你会在电脑上看到 Ubuntu 安装菜单。

*   首先你需要选择语言**选择语言**然后选择选项**选择其他。**
*   现在找到你之前创建的**空闲空间**，点击 **+** 分配空间给你的**操作系统**和**交换空间**。
*   接下来你需要**给你的 RAM** 空间来交换，然后设置你的**登录凭证**。
*   最后点击**安装**然后**重启**。

就这样，你完了。

**注意:**我们始终建议您在继续之前备份您的重要文件，尽管这种方法已经在我们这边测试过几次了。