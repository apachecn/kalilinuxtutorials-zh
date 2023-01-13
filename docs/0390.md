# proc dump:proc dump Sysinternals 工具的 Linux 版本

> 原文：<https://kalilinuxtutorials.com/procdump-linux-version/>

它是 Windows 的 Sysinternals 工具套件中经典 ProcDump 工具的 Linux 翻版。

它为 Linux 开发人员提供了一种基于性能触发器创建应用程序核心转储的便捷方式。

**也读:**[lol bas——靠土地为生的二进制和脚本](https://kalilinuxtutorials.com/lolbas/)

**安装&使用**

**要求**

*   最低操作系统:
    *   红帽企业版 Linux / CentOS 7
    *   Fedora 26
    *   Mageia 6
    *   Ubuntu 14.04 lt
    *   我们正在积极测试其他 Linux 发行版。如果您有特定发行版的请求，请让我们知道(或者创建一个包含必要更改的拉式请求)。
*   gdb >= 7.6.1
*   zlib(仅构建时)

**安装 ProcDump**

**通过软件包管理器【首选方法】**

*   添加 Microsoft 产品源

科尔 https://packages.microsoft.com/keys/microsoft.asc | gpg–dearmor > Microsoft . gpg
sudo mv Microsoft . gpg/etc/apt/trusted . gpg . d/Microsoft . gpg

**注册微软产品订阅源**

**Ubuntu 16.04**

sudo sh-c ' echo " deb[arch = amd64]https://packages . Microsoft . com/repos/Microsoft-Ubuntu-xenial-prod xenial main " >/etc/apt/sources . list . d/Microsoft . list '

**Ubuntu 14.04**

sudo sh-c ' echo " deb[arch = amd64]https://packages . Microsoft . com/repos/Microsoft-Ubuntu-trusty-prod trusty main " >/etc/apt/sources . list . d/Microsoft . list '

*   **安装 Procdump**

sudo apt-get 更新
sudo apt-get 安装 procdump
Via。deb 包
前置依赖:dpkg( > =1.17.5)

**下载。deb 包**

**Ubuntu 16.04**

wget https://packages . Microsoft . com/repos/Microsoft-Ubuntu-xenial-prod/pool/main/p/proc dump/proc dump _ 1 . 0 . 1 _ amd64 . deb

**Ubuntu 14.04**

wget https://packages . Microsoft . com/repos/Microsoft-Ubuntu-trusty-prod/pool/main/p/proc dump/proc dump _ 1 . 0 . 1 _ amd64 . deb

**安装 Procdump**

sudo dpkg-I proc dump _ 1 . 0 . 1 _ amd64 . deb
sudo apt-get-f 安装

**卸载**

**Ubuntu 14.04+**

sudo apt-get 清除程序转储

**用途**

用法:procdump[OPTIONS…]TARGET
OPTIONS
-C 创建进程从 0 到 100 的转储的 CPU 阈值* nCPU
-c 创建进程从 0 到 100 的转储的 CPU 阈值* nCPU
-M 内存提交阈值(MB)，当内存提交低于指定的 MB 值时，创建转储
-m 触发器。
-n 退出前要写入的转储数量
-写入转储前的连续秒数(默认值为 10)
TARGET 必须是以下值之一:
-p 进程的 PID
-w 可执行进程的名称

[**Download**](https://github.com/Microsoft/ProcDump-for-Linux)