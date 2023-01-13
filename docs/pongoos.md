# PongoOS:苹果主板的预引导执行环境

> 原文：<https://kalilinuxtutorials.com/pongoos/>

[![PongoOS : A Pre-Boot Execution Environment For Apple Boards](img/94c4bafaaa39fc4a5a3ea9c5bdb02a03.png "PongoOS : A Pre-Boot Execution Environment For Apple Boards")](https://1.bp.blogspot.com/-WonCV6IOsSo/X_70QC8FRYI/AAAAAAAAIVg/nAblM8JRVAE9Flzys_HYUOtqpmGmKooogCLcBGAsYHQ/s728/pongoOS%25281%2529.png)

PongoOS 是一个基于 checkra1n 构建的苹果主板预启动执行环境。

**在 macOS 上构建**

*   安装 Xcode +命令行实用工具
*   运行`make all`

**在 Linux 上构建**

*   安装铿锵(如有疑问，从[apt.llvm.org](https://apt.llvm.org)开始)
*   安装`ld64`和 cc tools`strip`。
    *   在 Debian/Ubuntu 上，这些可以从 checkra1n repo 安装:

**echo ' deb https://assets.checkra.in/debian/' | sudo tee/etc/apt/sources . list . d/check ra1n . list
sudo apt-key adv–fetch-keys https://assets.checkra.in/debian/archive.key
sudo apt-get 更新
sudo apt-get install-y ld64 cc tools-strip**

*   在其他版本的 Linux 上，你可能需要自己构建它们。也许[这个回购](https://github.com/Siguza/ld64)会帮到你。

如果 **`clang`、`ld64`、**或`**cctools-strip**`没有它们默认的名称/路径，你会想要改变它们的调用。作为参考，默认变量相当于:

**EMBEDDED _ CC = clang EMBEDDED _ LD flags =-fuse-LD =/usr/bin/ld64 STRIP = CC tools-STRIP make all**

**构建工件**

Makefile 将在`build/`中创建四个二进制文件:

*   主蓬古斯的马赫-O
*   `Pongo.bin`–同上，但作为可以跳转到的裸机二进制文件
*   `checkra1n-kpf-pongo`–checkra1n 内核补丁查找器，作为一个彭哥模块(Mach-O/kext)
*   庞古斯和 KPF 合并成一个二进制

**用途**

```
checkra1n -k Pongo.bin                  # Boots to Pongo shell, KPF not available
checkra1n -k PongoConsolidated.bin      # Auto-runs KPF and boots to XNU
checkra1n -k PongoConsolidated.bin -p   # Loads KPF, but boots to Pongo shell 
```

**结构**

*   核心的 PongoOS 和驱动在`src/`。
    *   构建时助手工具在`tools/`中。
*   PongoOS 使用的 stdlib(new lib)在`aarch64-none-darwin`里。
    *   这包括一个为 Newlib 定制的补丁，以便与达尔文 ABI 一起工作。
*   一个示例模块存在于`example/`中。
*   与 PongoOS shell 通信的脚本在`scripts/`中。
    *   这包括用于 macOS 的交互式 shell 客户端`pongoterm`。
*   checkra1n 内核补丁查找器(KPF)在`checkra1n/kpf`中。
    *   这目前包括 SEP 漏洞，尽管将来会转移到主线 PongoOS 中。
*   用户版的 KPF 可以从`checkra1n/kpf-test`开始构建(只能在 arm64 上运行)。

[**Download**](https://github.com/checkra1n/pongoOS)