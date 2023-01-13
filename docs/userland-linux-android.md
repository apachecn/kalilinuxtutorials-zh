# 用户世界:在 Android 上运行 Linux 发行版或应用程序

> 原文：<https://kalilinuxtutorials.com/userland-linux-android/>

UserLAnd 所依赖的资产和构建它们的脚本包含在其他存储库中。用于所有发行版和应用程序的公共资产可以在[CypherpunkArmory/UserLAnd-Assets-Support](https://github.com/CypherpunkArmory/UserLAnd-Assets-Support)找到。

在 Android 上运行 Linux 发行版或应用程序的最简单方法。特点:

*   在 Android 上运行完整的 linux 发行版或特定的应用程序。
*   像正规 app 一样安装卸载。
*   不需要根目录。

**同样，阅读-[RootOS–MAC OS Root 助手](https://kalilinuxtutorials.com/rootos-macos-root-helper/)**

## **如何开始使用 UserLAnd:**

有两种方法可以使用 UserLAnd:单击应用程序和用户定义的自定义会话。

## **使用单击应用:**

1.  点按一个应用程序。
2.  填写所需信息。
3.  你可以走了！

### **使用用户定义的自定义会话:**

1.  **定义一个会话**–它描述了您将要使用的文件系统，以及连接到它时您想要使用的服务类型(ssh 或 vnc)。
2.  **定义一个文件系统**——它描述了您想要安装的 Linux 发行版。
3.  定义后，只需点击会话即可启动。这将下载必要的资产，设置文件系统，启动服务器，并连接到它。第一次启动需要几分钟，但之后会更快。

### **管理软件包**

Debian、Ubuntu 和 Kali :

*   更新:`**sudo apt-get update && sudo apt-get dist-upgrade**`
*   安装包:`**sudo apt-get install <package name>**`
*   移除软件包:`**sudo apt-get remove <package name>**`

Archlinux :

*   更新:`**sudo pacman -Syu**`
*   安装包:`**sudo pacman -S <package name>**`
*   移除软件包:`**sudo pacman -R <package name>**`

## **安装桌面**

#### Debian、Ubuntu 和 Kali :

*   安装 Lxde: `**sudo apt-get install lxde**` **(默认桌面)**
*   安装 X 服务器客户端:[在 Play store 上下载](https://play.google.com/store/apps/details?id=x.org.server&hl=en)
*   启动 XSDL
*   在用户区类型:`**export DISPLAY=:0 PULSE_SERVER=tcp:127.0.0.1:<PORT NUMBER>**`
*   然后键入:`**startlxde**`
*   然后回到 XSDL，桌面就会出现

#### ArchLinux :

*   安装 lxd:`**sudo pacman -S lxde**`
*   安装 X 服务器客户端:[在 Play store 上下载](https://play.google.com/store/apps/details?id=x.org.server&hl=en)
*   启动 XSDL
*   在用户区域类型:导出`**DISPLAY=:0 PULSE_SERVER=tcp:127.0.0.1:<PORT NUMBER>**`
*   然后键入:`**startlxde**`
*   然后回到 XSDL，桌面就会出现

[**Download**](https://github.com/CypherpunkArmory/UserLAnd)