# g predict–卫星追踪应用

> 原文：<https://kalilinuxtutorials.com/gpredict-satellite-tracking-application/>

Gpredict 是一个用于 Linux 桌面的实时卫星跟踪和轨道预测程序
。它将 SGP4/SDP4 传播算法与
和 NORAD 双线元素集(TLE)一起使用。

## **gpredit 的一些核心特性包括:**

*   对大量卫星的跟踪只受计算机的物理内存和处理能力的限制
*   在列表、地图、极坐标图以及这些的任意组合中显示跟踪数据
*   让许多模块同时在笔记本或他们自己的
    窗口中打开。这些模块也可以全屏模式运行
*   你可以使用许多地面站
*   预测即将到来的通行证
*   Gpredict 可以实时运行，模拟实时运行(快进和
    后退)，以及手动时间控制
*   实时和非实时模式的详细信息
*   通过 Hamlib rigctld 的无线电多普勒调谐
*   通过 Hamlib rotctld 控制天线旋转器

[点击这里](http://gpredict.oz9aec.net/)进入主页。

**也读作[Dnsenum——DNS 枚举工具，用于查找 DNS 服务器](https://kalilinuxtutorials.com/dnsenum/)**

## **要求**

该应用程序是使用 Gtk+ 3 小部件集编写的，它可用于大多数 Unix 操作系统，如 Mac 和 Windows。成功编译 Gpredict 需要以下库
:

1.  **Gtk+ 3 或更高版本**
2.  **GLib 2.32 或更高版本**
3.  **古画布 2**
4.  **Libcurl 7.16 或更高版本**
5.  **Hamlib(仅运行时，构建不需要)**

如果您从源代码编译它，您还需要开发包
,包名中通常带有-dev 或-devel，例如 libgtk-3-dev。在 Debian 和
Ubuntu 系统上，您可以使用以下命令安装构建依赖项:

```
sudo apt install libtool intltool autoconf automake libcurl4-openssl-dev
sudo apt install pkg-config libglib2.0-dev libgtk-3-dev libgoocanvas-2.0-dev
```

要从源代码构建和安装应用程序，首先要打开源代码包:

```
tar -xvf gpredict-x.y.z.tar.gz
```

然后转到 gpredict-x.y.z 目录并构建 gpredict:

```
./configure
make
make install
```

最后一步通常要求您成为 root 用户，否则您可能没有安装它所需的权限。如果您不能或者不想以 root 用户身份安装 gpredict，您可以通过
将——prefix = somedir 添加到。/配置步骤。例如

```
./configure --prefix=/home/user/predict
 will configure the build to install the files into /home/user/gpredict folder.
```

如果您直接从 git 存储库构建，您必须运行
。/autogen.sh 而不是 configure。您可以向
autogen.sh 脚本传递与配置脚本相同的选项。

## **使用应用** 

它附带了一些示例数据，可以“开箱即用”运行。
一旦你有了 UI 的想法，你可以修改
默认模块的设置(点击右上角的小向下箭头)，或者
通过文件创建一个新模块- >新模块。

强烈建议您去 http://gpredict.oz9aec.net/documents.php 看一下用户手册

## **用户支持**

用户支持是通过 https://community.libre.space/c/gpredict 自由空间基金会主办的 Gpredict 论坛提供的

## **条款与条件**

它是在 GNU 通用公共许可证下发布的，没有任何担保。如果您在安装或使用 Gpredict 时遇到问题，
可以在由 https://community.libre.space/c/gpredict 自由空间基金会
主办的 its 论坛上寻求支持

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/csete/gpredict)