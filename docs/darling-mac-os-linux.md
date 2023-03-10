# darling——用于 Linux 的达尔文/Mac OS 仿真层

> 原文：<https://kalilinuxtutorials.com/darling-mac-os-linux/>

Darling 是 OS X 应用程序的运行时环境。请注意，目前不支持任何 GUI 应用程序。

![](img/e4a0a643810027aa9a3f88e71edeaed3.png)

## **下载乖乖** 

Darling 使用了许多 Git 子模块，所以简单的克隆是不行的。

```
git clone --recurse-submodules https://github.com/darlinghq/darling.git
```

更新来源:

```
git pull` `**git submodule init**
**git submodule update**
```

## **前缀**

Darling 支持 DPREFIXes，这与 WINEPREFIXes 非常相似。它们是虚拟的“chroot”环境，具有类似 macOS 的文件系统结构，您可以在其中安全地安装软件。默认的 DPREFIX 位置是`~/.darling`，但是这可以通过导出一个同名的环境变量来更改。前缀是在第一次使用时自动创建和初始化的。

请注意，我们使用`overlayfs`来创建前缀，所以我们不支持在像 NFS 或 eCryptfs 这样的文件系统上放置前缀。特别是，如果您有一个加密的主目录，默认的前缀位置将不起作用。

**又读[Crypton——对各种加密系统、数字签名、哈希算法的攻击](https://kalilinuxtutorials.com/crypton/)**

### **你好世界**

让我们从 Hello world 开始:

```
$ darling shell echo Hello world
Hello world
```

恭喜你，你已经通过达林的 OS X 系统调用仿真和运行时库打印了 Hello world。

## **安装软件**

您可以使用 shell 中的安装工具安装`.pkg`包。它有点像 OS X 安装程序的近亲:

```
$ darling shell
Darling [~]$ installer -pkg mc-4.8.7-0.pkg -target /
```

如果你之前已经从 [Rudix](http://rudix.org) 下载了 Midnight Commander 包，你现在可以运行`mc`来启动 MC for OS X，为了更容易安装，安装 Rudix 包管理器。注意不是所有的 Rudix 包都可以在 Darling 下工作。

您可以使用`uninstaller`命令卸载并列出软件包。

### **处理 DMG 图像**

DMG 图像可以从`darling shell`内部用`hdiutil`连接和分离。这是安装 Xcode 及其工具链和 SDK 的方法(注意 Xcode 本身还没有运行):

```
Darling [~]$ hdiutil attach Xcode_7.2.dmg
/Volumes/Xcode_7.2
Darling [~]$ cp -r /Volumes/Xcode_7.2/Xcode.app /Applications
Darling [~]$ export SDKROOT=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk
Darling [~]$ echo 'void main() { puts("Hello world"); }' > helloworld.c
Darling [~]$ /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang helloworld.c -o helloworld
Darling [~]$ ./helloworld
Hello world
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/darlinghq/darling)