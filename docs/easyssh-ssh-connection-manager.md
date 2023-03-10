# easy SSH——SSH 连接管理器，让您的生活更加轻松

> 原文：<https://kalilinuxtutorials.com/easyssh-ssh-connection-manager/>

Easyssh 是一个完整、高效且易于使用的管理器。使用同一连接的多个实例创建和编辑连接、分组、自定义终端。

## **Easyssh 功能**

1.  管理连接和组
2.  定制终端
3.  黑暗主题
4.  同一连接的多个实例
5.  恢复打开的主机
6.  同步 `**~/.ssh/config**`

**也可理解为 [射箭——开源漏洞评估&管理帮助开发者&测试者执行扫描&管理漏洞](https://kalilinuxtutorials.com/archery-scan-vulnerabilities/)**

## **建设&发展**

如果您想自己动手构建 EasySSH，您需要以下依赖项:

*   libgee-0.8-dev
*   libgtk-3-dev
*   libgranite-dev
*   libvte-2.91-dev
*   莉吉森-格利布-德夫
*   libunity-dev
*   介子
*   valac

运行`**meson build**`来配置构建环境，运行`ninja test`来构建和运行自动化测试

```
meson build --prefix=/usr
cd build
ninja test
```

要安装，使用`**ninja install**`，然后用`**com.github.muriloventuroso.easyssh**`执行

```
sudo ninja install
com.github.muriloventuroso.easyssh
```

## **安装 Flatpak**

**安装:**

```
flatpak install flathub com.github.muriloventuroso.easyssh
```

**运行:**

```
flatpak run com.github.muriloventuroso.easyssh
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/muriloventuroso/easyssh)

**作者:穆里洛·文图拉索**