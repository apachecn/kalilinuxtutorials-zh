# 一个顽皮的，跨平台的二进制解析箱，用 Rust 写的

> 原文：<https://kalilinuxtutorials.com/goblin-cross-platform-binary-parsing-crate-written-rust/>

[![Goblin : An Impish, Cross-Platform Binary Parsing Crate, Written In Rust](img/16118d8315bb7648cf9621214b23f393.png "Goblin : An Impish, Cross-Platform Binary Parsing Crate, Written In Rust")](https://1.bp.blogspot.com/-MCop9tGGh7Q/XeUJ07VXdlI/AAAAAAAADuc/KsE18W550NcnDDc9ICx0AY7wQx7HbtnAwCLcBGAsYHQ/s1600/libgoblin.png)

Goblin 是一个顽皮的、跨平台的二进制解析工具，用 Rust 编写。它支持:

*   一个 ELF32/64 解析器和原始 C 结构
*   一个 32/64 位、零拷贝、支持端序的 Mach-o 解析器和原始 C 结构
*   PE32/PE32+ (64 位)解析器和原始 C 结构
*   Unix 档案解析器和加载器

**用途**

*   妖精要求`**rustc**` 1.31.1。
*   添加到您的`**Cargo.toml**`

**【依赖】
哥布林= "0.1"**

**特色**

*   很棒的板条箱名字
*   零拷贝、跨平台、支持端序、ELF64/32 实施——哇！
*   零拷贝、跨平台、支持字节序的 32/64 位 Mach-o 解析器——zoiks！
*   PE 32/64 位解析器–bing！
*   一个 Unix *和* BSD 风格的存档解析器(后者由 [@willglynn](https://github.com/willglynn) 提供)–万岁！
*   许多 cfg 选项——它会让你晕头转向，并在阅读源代码时让你生气！
*   模糊化-“我很高兴地告诉大家，地精经受住了 1 亿次模糊化，1~100 号种子各 100 万次。”–[@ San xiyn](https://github.com/sanxiyn)
*   试验

`**libgoblin**`旨在成为您的二进制解析、加载和分析的一站式商店。

**用例**

Goblin 主要支持以下重要用例:

*   核心、无 std 的`**#[repr(C)]**`结构、极小的编译时间、32/64(或者两者都有)。
*   打字双关。在一种类型上定义一次函数，但是让它在 32 或 64 位变体上工作——不需要真正改变任何东西，也不需要宏！基本示例见`**examples/automagic.rs**`。
*   `**std**`模式。这通过`**Pread**`和`**Pwrite**`抛出了读写 impls，从文件中读取，便利分配，额外的方法等等。这适用于能够分配并希望从磁盘读取二进制文件的客户端。
*   `**Endian_fd**`。这是一个真正可怕的名字，用于二进制分析，如 [panopticon](https://github.com/das-labor/panopticon) 或 [falcon](https://github.com/endeav0r/falcon) 需要读取外国字节序的二进制文件，*或*作为构建跨平台外国架构 binutils 的基础，例如 [cargo-sym](https://github.com/m4b/cargo-sym) 和 [bingrep](https://github.com/m4b/bingrep) 就是这种情况的简单例子，但没有限制。

以下是您可以用这个板条箱做的一些事情(或者帮助实现这些事情):

*   写一个编译器，用它[生成二进制](https://github.com/m4b/faerie)(所有的 raw C 结构都有 [`**Pwrite**`](https://github.com/m4b/scroll) 派生)。
*   编写一个二进制分析工具，加载、解析和分析各种二进制格式，例如 [panopticon](https://github.com/das-labor/panopticon) 或 [falcon](https://github.com/endeav0r/falcon) 。
*   编写一个[半功能动态链接器](https://github.com/m4b/dryad)。
*   编写一个[内核](https://github.com/redox-os/redox)，并使用`**no_std**` cfg 加载二进制文件。也就是说，它本质上只是 struct 和 const 定义(就像 C 头文件一样)——没有 fd，没有 output，没有 std。
*   写一个 [bin2json](https://github.com/m4b/bin2json) 工具，因为二进制格式为什么不应该在 json 里？

**CFGS**

被设计成可大规模配置的。当前标志有:

*   elf 64–64 位 elf 二进制文件，`**repr(C)**`结构定义
*   elf 32–32 位 elf 二进制文件，`**repr(C)**`结构定义
*   mach 64–64 位 mach-o `**repr(C)**`结构定义
*   mach 32–32 位 mach-o `**repr(C)**`结构定义
*   pe32–32 位 PE `**repr(C)**`结构定义
*   pe64–64 位 PE `**repr(C)**`结构定义
*   存档——Unix 存档解析器
*   endian _ FD–根据二进制文件中的字节顺序进行解析
*   标准–允许`**no_std**`环境

**模块**

| [存档](https://docs.rs/goblin/0.1.1/goblin/archive/index.html) | 为 Unix 档案实现一个简单的解析器和提取器。 |
| [集装箱](https://docs.rs/goblin/0.1.1/goblin/container/index.html) | 二进制容器大小信息和字节顺序上下文 |
| [精灵](https://docs.rs/goblin/0.1.1/goblin/elf/index.html) | 通用 ELF 模块，提供对 ELF 常量和其他辅助函数的访问，独立于 ELF 位。还定义了一个实现统一解析器的`Elf`结构，该解析器返回一个包装的`Elf64`或`Elf32`二进制文件。 |
| [elf32](https://docs.rs/goblin/0.1.1/goblin/elf32/index.html) | ELF 32 位结构定义和相关值，重新导出以方便“类型双关” |
| [elf64](https://docs.rs/goblin/0.1.1/goblin/elf64/index.html) | ELF 64 位结构定义和相关值，重新导出以方便“类型双关” |
| [错误](https://docs.rs/goblin/0.1.1/goblin/error/index.html) | 一个自定义的妖精错误 |
| [马赫](https://docs.rs/goblin/0.1.1/goblin/mach/index.html) | Mach-o，主要是零拷贝、二进制格式解析器和原始结构定义 |
| [pe](https://docs.rs/goblin/0.1.1/goblin/pe/index.html) | PE32 和 PE32+解析器 |
| [strtab](https://docs.rs/goblin/0.1.1/goblin/strtab/index.html) | 基于字节偏移量的字符串表。常用于 ELF 二进制，Unix 归档，甚至 PE 二进制。 |

[**Download**](https://github.com/m4b/goblin)