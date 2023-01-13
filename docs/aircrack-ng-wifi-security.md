# Aircrack-NG : WiFi 安全审计工具套件

> 原文：<https://kalilinuxtutorials.com/aircrack-ng-wifi-security/>

Aircrack-ng 是一整套评估 WiFi 网络安全的工具。

它侧重于 WiFi 安全的不同领域:

*   监控:数据包捕获和数据导出到文本文件，供第三方工具进一步处理。
*   攻击:重放攻击，解除认证，假冒接入点和其他通过数据包注入。
*   测试:检查 WiFi 卡和驱动程序功能(捕获和注入)。
*   开裂:WEP 和 WPA PSK (WPA 1 和 2)。

所有的工具都是命令行，允许繁重的脚本。很多图形用户界面都利用了这个特性。它主要运行 Linux，但也运行 Windows、OS X、FreeBSD、OpenBSD、NetBSD 以及 Solaris，甚至 eComStation 2。

**也可理解为[PUT 2 win–脚本通过 PUT HTTP 方法自动上传 Shell 以获取 Meterpreter](https://kalilinuxtutorials.com/put2win-script-automatize-shell-upload/)**

## **空调安装和可选附件**

下面是安装基本要求的说明，以便为许多操作系统构建`aircrack-ng`。

**注意**:在打包 Aircrack-ng 时，CMocka 不应成为依赖项。

### **Linux**

#### **Debian/Ubuntu**

```
sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev ethtool shtool rfkill zlib1g-dev libpcap-dev libsqlite3-dev libpcre3-dev libhwloc-dev libcmocka-dev
```

#### **Fedora/CentOS/RHEL**

```
sudo yum install libtool pkgconfig sqlite-devel autoconf automake openssl-devel libpcap-devel pcre-devel rfkill libnl3-devel gcc gcc-c++ ethtool hwloc-devel libcmocka-devel
```

### **FreeBSD**

```
pkg install pkgconf shtool libtool gcc7 automake autoconf pcre sqlite3 openssl gmake hwloc cmocka
```

### **OSX**

需要 Xcode，XCode 命令行工具和家酿。

```
brew install autoconf automake libtool openssl shtool pkg-config hwloc pcre sqlite3 libpcap cmocka
```

### **窗户**

#### **Cygwin**

Cygwin 需要到`setup.exe`实用程序的完整路径，以便自动安装必要的包。此外，它还需要安装位置、缓存包下载位置的路径和镜像 URL。

自动安装所有依赖项的示例如下:

```
c:\cygwin\setup-x86.exe -qnNdO -R C:/cygwin -s http://cygwin.mirror.constant.com -l C:/cygwin/var/cache/setup -P autoconf -P automake -P bison -P gcc-core -P gcc-g++ -P mingw-runtime -P mingw-binutils -P mingw-gcc-core -P mingw-gcc-g++ -P mingw-pthreads -P mingw-w32api -P libtool -P make -P python -P gettext-devel -P gettext -P intltool -P libiconv -P pkg-config -P git -P wget -P curl -P libpcre-devel -P openssl-devel -P libsqlite3-devel
```

#### **MSYS2**

```
**pacman -Sy autoconf automake-wrapper libtool msys2-w32api-headers msys2-w32api-runtime gcc pkg-config git python opens**
```

## **编译**

为了构建`**aircrack-ng**`，使用了自动工具构建系统。自动工具取代了旧的编译方法。

**注意**:如果使用开发者版本，例如:从源代码控制中签出的版本，你将需要运行一个前`configure`脚本。要使用的脚本是下列之一: **`autoreconf -i`** 或 **`env NOCONFIGURE=1 ./autogen.sh`** 。

首先， **`./configure`** 该项目为建筑与环境指定了合适的选项:

```
./configure <options>
```

**提示**:如果以上失败，请参见上面关于开发者源码控制版本。

接下来，编译项目(考虑是否需要`make`或`gmake`):

*   编译:

`make`

*   在*BSD 或 Solaris 上编译:

`gmake`

最后，下面列出的其他目标可能对您的环境有用:

*   执行所有单元测试:

`make check`

*   安装:

`make install`

*   卸载:

`make uninstall`

### `./configure`旗帜

配置时，可以使用和组合以下标志来根据您的选择调整套件:

*   **with-air cap = DIR**:需要在 windows 上支持 air cap 设备(仅限 cygwin 或 msys2)将上面的 DIR 替换为从 Airpcap CD 或在线下载的 SDK 中提取的源代码的根目录的绝对位置。搭建实验工具时需要在 Windows 上搭建`besside-ng`、`besside-ng-crawler`、`easside-ng`、`tkiptun-ng`、`wesside-ng`。开发者包(兼容版本 4.1.1 和 4.1.3)可以从[https://support . riverbed . com/content/support/software/steel central-NPM/aircap . html](https://support.riverbed.com/content/support/software/steelcentral-npm/airpcap.html)下载
*   **带-实验**:需要编译`tkiptun-ng`、`easside-ng`、`buddy-ng`、`buddy-ng-crawler`、`airventriloquist`、`wesside-ng`。libpcap 开发包也是编译大部分工具所需要的。如果不存在，并不是所有的实验工具都会被制造出来。在 Cygwin 上，libpcap 不存在，由 Airpcap SDK 代替。请参见上面的–with-air cap 选项。
*   **with-ext-scripts** :需要建造`airoscript-ng`、`versuck-ng`、`airgraph-ng`和`airdrop-ng`。注意:每个脚本都有自己的依赖项。
*   **with-gcrypt** :使用 libgcrypt 加密库，而不是默认的 OpenSSL。并且还使用内部快速 sha1 实现(借用 GIT)依赖(Debian): libgcrypt20-dev
*   **带-杜马**:带杜马支持编译。DUMA 是一个检测缓冲区溢出和欠载运行的库。依赖关系(debian):杜马
*   **disable-libnl** :设置要编译的项目，不带 libnl (1 或 3)。仅限 Linux 选项。
*   不带-opt:不启用堆栈保护器(在 GCC 4.9 及更高版本上)。
*   **enable-shared** :使 OSdep 成为共享库。
*   **disable-shared** :与 **enable-static** 结合使用，将静态编译 Aircrack-ng。
*   **with-avx512** :在 x86 上，增加对 aircrack-ng 中 avx512 指令的支持。仅在当前 CPU 支持 AVX512 时使用。
*   **with-static-simd=** :在 aircrack-ng 二进制中编译单个优化。对于静态编译和/或空间受限的设备非常有用。有效的 SIMD 选项:x86-sse2、x86-avx、x86-avx2、x86-avx512、ppc-altivec、ppc-power8、arm-neon、arm-asimd 必须与–enable-static–disable-shared 一起使用。当使用这两个选项时，默认情况下是在二进制文件中编译通用优化。–with-static-SIMD 仅允许选择另一个。

#### 例子:

*   配置和编译:

```
./configure --with-experimental
make
```

*   用 gcrypt 编译:

```
./configure --with-gcrypt
make
```

*   安装:

**`make install`**

*   安装(剥离二进制文件):

**`make install-strip`**

*   使用外部脚本安装:

```
./configure --with-experimental --with-ext-scripts
make
make install
```

*   测试(使用 sqlite、实验和 pcre)

```
./configure --with-experimental
make
make check
```

*   使用 macports 在 OS X 上编译(以及所有选项):

```
./configure --with-experimental
gmake
```

*   使用 XCode 7.1 和 Homebrew 在 OS X 10.10 上编译:

```
env CC=gcc-4.9 CXX=g++-4.9 ./configure
make
make check
```

**注意:**旧版 XCode 附带了一个不支持 CPU 特性检测的 LLVM 版本；这导致`./configure`失败。为了解决这个旧的 LLVM，需要使用一个不同的编译套件，比如 GCC 或者家酿公司的一个新的 LLVM。

如果您希望使用家酿的 OpenSSL，您可能需要指定它的安装位置。要找出 OpenSSL 的位置，运行:

`**brew --prefix openssl**`

使用上面的输出作为`./configure`行中`--with-openssl=DIR`的方向:

```
env CC=gcc-4.9 CXX=g++-4.9 ./configure --with-openssl=DIR
make
make check
```

*   以更好的性能在 FreeBSD 上编译

```
env CC=gcc7 CXX=g++7 ./configure
gmake
```

*   用 air cap 在 Cygwin 上编译(假设 Airpcap devpack 在 Aircrack-ng 目录中解包)

```
cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src
cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-osdep
cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-crypto
cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-util
dlltool -D Airpcap_Devpack/bin/x86/airpcap.dll -d build/airpcap.dll.def -l Airpcap_Devpack/bin/x86/libairpcap.dll.a
autoreconf -i
./configure --with-experimental --with-airpcap=$(pwd)
make
```

#### [![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/aircrack-ng/aircrack-ng)