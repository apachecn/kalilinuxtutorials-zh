# rz-Ghidra:Rizin 的深度 g hidra 反编译器和 Sleigh 反汇编器集成

> 原文：<https://kalilinuxtutorials.com/rz-ghidra/>

[![Pown Recon : A Powerful Target Reconnaissance Framework Powered By Graph Theory](img/4b5072592274ff29f53d369a42e27c0c.png "Pown Recon : A Powerful Target Reconnaissance Framework Powered By Graph Theory")](https://3.bp.blogspot.com/-jqykbKhfu8c/XNwMUihRKlI/AAAAAAAAAWk/3BxCJ3CJkuY7T9xa1l7tys-RaySPECLkACLcBGAs/s1600/Tutorial%25281%2529.png)

Rz-Ghidra 是 rizin 的 Ghidra 反编译器和 Sleigh 反汇编器的集成。它完全基于完全用 C++编写的 Ghidra 的反编译器部分，所以根本不需要 Ghidra 本身，插件可以独立构建。这个项目最初是为 radare2 在 r2con 2019 上展示的，作为“切割者对话:https://youtu.be/eHtMiezr7l8?t=950”的一部分

**安装**

rz-pm 软件包可以轻松安装，如下所示:

rz-pm -i rz-ghidra

这个包只安装 rizin 部分。要使用 cutter 提供的 rz-ghidra，可以使用从 Cutter 1.9 开始的预构建版本，该版本捆绑了 rz-ghidra，或者遵循下面的构建说明。

**用途**

**用法:pdg #原生 Ghidra 反编译插件
| pdg #用 Ghidra 反编译程序反编译当前函数
| pdgd #转储调试 XML 转储
| pdgx #转储当前反编译函数的 XML
| pdgj #转储当前反编译函数为 JSON
| pdgo #反编译当前函数并带有偏移量
| pdgs #显示加载的 Sleigh 语言
| pdg* #反编译后的代码作为注释返回给 rizin**

以下配置变量(用于`**e**`命令)可用于调整 rz-ghidra 的行为:

**GHI DRA . CMT . CPP:c++ Comment style
GHI DRA . CMT . Indent:Comment Indent
GHI DRA . Indent:Indent increment increment
GHI DRA . lang:自定义 Sleigh ID 以覆盖自动检测(例如 x86:LE:32:default)
GHI DRA . line len:最大行长度
ghidra.nl.brace:打开前换行' { '
GHI DRA . nl . else:else 前换行
GHI DRA . Sleigh home:Sleigh home【T8**

这里，`**ghidra.sleighhome**`必须指向包含`***.sla**`、`***.lspec**`、…文件的目录，这些文件是反编译器应该支持的架构的文件。然而，这是在使用 rz-pm 包或如下所示安装时自动设置的。

**大楼**

首先，确保包含在这个存储库中的子模块被获取并且是最新的:

**git 子模块初始化
git 子模块更新**

然后，rizin 插件可以按如下方式构建和安装:

**mkdir build&&CD build
cmake-DC make _ INSTALL _ PREFIX = ~/。当地的..
制造
制造安装**

在这里，将`**CMAKE_INSTALL_PREFIX**`设置为 rizin 可以加载插件的位置。安装步骤对于插件的工作是必要的，因为它包括安装必要的 Sleigh 文件。

要构建 Cutter 插件，将`**-DBUILD_CUTTER_PLUGIN=ON -DCUTTER_SOURCE_DIR=/path/to/cutter/source**`传递给 cmake，例如:

**/my/path > git 克隆 https://github.com/rizinorg/cutter
/my/path>#构建切割器，克隆 rz-ghidra 等。
…
/my/path/rz-ghidra>mkdir build&&CD build
/my/path/rz-ghidra/build>cmake-DBUILD _ CUTTER _ PLUGIN = ON-DC CUTTER _ SOURCE _ DIR =/my/path/CUTTER-DC make _ INSTALL _ PREFIX = ~/。当地的..
/my/path/rz-ghidra/build>make&make install**

**版本和 Rizin 兼容性**

Rizin 有一个快速发展的 C API，因此有必要明确 rz-ghidra 的哪个版本与 Rizin 的哪个版本兼容:

使用 git 的 Rizin 和 rz-ghidra 时:

*   rz-ghidra 分支 **`dev`** 跟随 Rizin 分支 **`dev`。**
*   rz-ghidra 分支`**stable**`沿着 Rizin 分支**前进。**

关于版本，rz-ghidra 一般与 Rizin 同时发布，经常使用相同的版本号(但不保证，不要依赖这些号！).此外，随着每个 Rizin 版本的发布，rz-ghidra 上会创建一个类似于`**rz-0.1.2**`的标签，它准确地指向一个 rz-ghidra 版本，并表明该版本与指定的 Rizin 版本兼容。发行版维护人员可以使用这些标签来查找如何建立依赖关系。

[**Download**](https://github.com/rizinorg/rz-ghidra)