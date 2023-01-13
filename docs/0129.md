# Aircrack-NG:评估 WiFi 网络安全的完整套件工具

> 原文：<https://kalilinuxtutorials.com/aircrack-ng-wifi-network-security/>

Aircrack-ng 是一整套评估 WiFi 网络安全的工具。它侧重于 WiFi 安全的不同领域:

*   **监控:**数据包捕获和数据导出到文本文件，以便第三方工具进一步处理。
*   **攻击:**通过数据包注入的重放攻击、去认证、假冒接入点等。
*   **测试:**检查 WiFi 卡和驱动能力(捕获和注入)。
*   **裂解:** WEP 和 WPA PSK (WPA 1 和 2)。

所有的工具都是命令行，允许繁重的脚本。很多图形用户界面都利用了这个特性。它主要运行 Linux，但也运行 Windows、OS X、FreeBSD、OpenBSD、NetBSD 以及 Solaris，甚至 eComStation 2。

**也可理解为[【cloud mapper】工具帮助分析你的 AWS 环境](https://kalilinuxtutorials.com/cloudmapper/)**

 **### **要求**

*   Autoconf
*   自动制造
*   Libtool
*   shtool
*   OpenSSL 开发包或 libgcrypt 开发包。
*   Airmon-ng (Linux)需要 ethtool。
*   在 windows 上，必须使用 cygwin，并且还需要 w32api 包。
*   在 Windows 上，如果使用 clang、libiconv 和 libiconv-devel
*   Linux: LibNetlink 1 或 3。可以通过传递–disable-libnl 进行配置来禁用它。
*   pkg-config(FreeBSD 上的 pkgconf)
*   带有 macports 的 FreeBSD、OpenBSD、NetBSD、Solaris 和 OS X:gmake
*   Linux/Cygwin: make 和标准 C++库开发包(Debian: libstdc++-dev)

### **可选的东西**

*   如果你想在 airodump-ng (-essid-regex)中用正则表达式过滤 SSID，就需要 pcre 开发包。
*   如果要在 aircrack-ng 中使用 airolib-ng 和'-r '选项，SQLite 开发包> = 3.3.17(建议使用 3.6.X 版本或更高版本)
*   如果要使用 Airpcap，需要 CD/ISO/SDK 中的“developer”目录。
*   为了构建`besside-ng`、`besside-ng-crawler`、`easside-ng`、`tkiptun-ng`、`wesside-ng`，需要 libpcap 开发包(在 Cygwin 上，用 Aircap SDK 代替；见上文)
*   为了在 FreeBSD 上获得最佳性能(高出 50-70%)，请通过以下方式安装 gcc5(或更好): pkg install gcc7
*   rfkill

## **解析基本要求**

下面是安装基本要求的说明，以便为许多操作系统构建`aircrack-ng`。

#### **Linux**

##### **Debian/Ubuntu**

```
sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev libsqlite3-dev libpcre3-dev ethtool shtool rfkill zlib1g-dev libpcap-dev
```

##### **Fedora/CentOS/RHEL**

```
sudo yum install libtool pkgconfig sqlite-devel autoconf automake openssl-devel** libpcap-devel pcre-devel rfkill libnl3-devel gcc gcc-c++ ethtool 
```

##### **FreeBSD**

```
pkg install pkgconf shtool libtool gcc7 automake autoconf pcre sqlite3 openssl gmake
```

#### **OSX**

需要 Xcode，XCode 命令行工具和家酿。

```
brew install autoconf automake libtool openssl shtool pkg-config
```

#### **窗户**

##### **Cygwin**

Cygwin 需要到`setup.exe`实用程序的完整路径，以便自动安装必要的包。此外，它还需要安装位置、缓存包下载位置的路径和镜像 URL。

自动安装所有依赖项的示例如下:

```
c:\cygwin\setup-x86.exe -qnNdO -R C:/cygwin -s http://cygwin.mirror.constant.com -l C:/cygwin/var/cache/setup -P autoconf -P automake -P bison -P gcc-core -P gcc-g++ -P mingw-runtime -P mingw-binutils -P mingw-gcc-core -P mingw-gcc-g++ -P mingw-pthreads -P mingw-w32api -P libtool -P make -P python -P gettext-devel -P gettext -P intltool -P libiconv -P pkg-config -P git -P wget -P curl -P libpcre-devel -P openssl-devel -P libsqlite3-devel
```

##### **MSYS2**

```
pacman -Sy autoconf automake-wrapper libtool msys2-w32api-headers msys2-w32api-runtime gcc pkg-config git python openss
```

## **编译**

为了构建`aircrack-ng`，使用了自动工具构建系统。自动工具取代了旧的编译方法。

**注意**:如果使用开发者版本，例如:从源代码控制中签出的版本，你将需要运行一个前`configure`脚本。要使用的脚本是以下之一:`autoreconf -i`或`env NOCONFIGURE=1 ./autogen.sh`。

首先，`./configure`使用为您的环境指定的适当选项来构建项目:

```
./configure <options>
```

**提示**:如果以上失败，请参见上面关于开发者源码控制版本。

接下来，编译项目(考虑是否需要`make`或`gmake`):

*   **编译:**

**`make`**

*   `*** BSD 或 Solaris 上编译:**`

 `**`gmake`**

最后，下面列出的其他目标可能对您的环境有用:

*   **执行所有单元测试:**

`**make check**`

*   `**安装:**`

 ``**make install**`

*   **卸载:**

`**make uninstall**`

#### **`./configure`旗帜**

配置时，可以使用和组合以下标志来根据您的选择调整套件:

*   **with-air cap = DIR**:需要在 windows 上支持 air cap 设备(仅限 cygwin 或 msys2)将上面的 DIR 替换为从 Airpcap CD 或在线下载的 SDK 中提取的源代码的根目录的绝对位置。搭建实验工具时需要在 Windows 上搭建`besside-ng`、`besside-ng-crawler`、`easside-ng`、`tkiptun-ng`、`wesside-ng`。开发者包(兼容 4.1.1 和 4.1.3 版本)可以在[这里](https://support.riverbed.com/content/support/software/steelcentral-npm/airpcap.html)下载。
*   **带-实验**:需要编译`tkiptun-ng`、`easside-ng`、`buddy-ng`、`buddy-ng-crawler`、`airventriloquist`、`wesside-ng`。libpcap 开发包也是编译大部分工具所需要的。如果不存在，并不是所有的实验工具都会被制造出来。在 Cygwin 上，libpcap 不存在，由 Airpcap SDK 代替。请参见上面的–with-air cap 选项。
*   **with-ext-scripts** :需要建造`airoscript-ng`、`versuck-ng`、`airgraph-ng`和`airdrop-ng`。注意:每个脚本都有自己的依赖项。
*   **with-gcrypt** :使用 libgcrypt 加密库，而不是默认的 OpenSSL。并且还使用内部快速 sha1 实现(借用 GIT)依赖(Debian): libgcrypt20-dev
*   **带-杜马**:带杜马支持编译。DUMA 是一个检测缓冲区溢出和欠载运行的库。依赖关系(debian):杜马
*   **disable-libnl** :设置要编译的项目，不带 libnl (1 或 3)。仅限 Linux 选项。
*   **不带-opt** :不启用栈保护器(GCC 4.9 及以上)。
*   **enable-shared** :使 OSdep 成为共享库。
*   **disable-shared** :与 **enable-static** 结合使用，将静态编译 Aircrack-ng。
*   **with-avx512** :在 x86 上，增加对 aircrack-ng 中 avx512 指令的支持。仅在当前 CPU 支持 AVX512 时使用。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/aircrack-ng/aircrack-ng)``**