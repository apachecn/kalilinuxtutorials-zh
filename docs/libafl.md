# LibAFL:先进的 Fuzzing 库-槽你的 Fuzzer 一起生锈

> 原文：<https://kalilinuxtutorials.com/libafl/>

[![LibAFL : Advanced Fuzzing Library – Slot Your Fuzzer Together In Rust](img/de8efdfcb71cf70e178afe2143ddc103.png "LibAFL : Advanced Fuzzing Library – Slot Your Fuzzer Together In Rust")](https://1.bp.blogspot.com/-KOBdh-CNd3A/YKLDv6SqbVI/AAAAAAAAJHk/CLxApJaNKZI12sBkxdmTLbJ8pXyheB80wCLcBGAsYHQ/s728/LibAFL%25281%2529.png)

先进的 Fuzzing 库是一个插槽你自己的 fuzzers 在一起，并扩展他们的功能使用锈。由安德里亚·菲奥拉迪[andreafioraldi@gmail.com](mailto:andreafioraldi@gmail.com)和张秀坤·梅尔[mail@dmnk.co](mailto:mail@dmnk.co)编写和维护。

**为什么是 LibAFL？**

LibAFL 为您提供了许多现成 fuzzer 的好处，同时完全可定制。一些突出功能目前包括:

*   **`fast` :** 我们在编译时竭尽所能，保持运行时开销最小。用户在手机上的 frida 模式下达到 120，000 execs/秒(使用所有内核)。
*   `**scalable**` : **`Low Level Message Passing`，`LLMP`** 简而言之，允许 LibAFL 在内核上几乎线性扩展，并通过 TCP 很快扩展到多台机器！
*   `**adaptable**`:可以更换 LibAFL 的各个部分。例如， **`BytesInput`** 只是一种潜在的表单输入:可以随意添加基于 AST 的结构化模糊输入，等等。
*   `**multi platform**` : LibAFL 在 *x86_64* 和 *aarch64* 上被确认可以在 *Windows* 、 *MacOS* 、 *Linux* 和 *Android* 上运行。 **`LibAFL`** 可以在`**no_std**`模式下构建，将 LibAFL 注入到嵌入式设备、虚拟机管理程序等晦涩难懂的目标中。
*   **`bring your own target` :** 我们支持纯二进制模式，比如 Frida 模式，以及基于源代码的多通道编译。当然，添加定制的仪器后端很容易。

**概述**

LibAFL 是一个可重用的 fuzzers 的集合，用 Rust 编写。它是快速的、多平台的、no_std 兼容的，并且可以在内核和机器上扩展。

它提供了一个主机箱，为定制模糊器提供构建块， [libafl](https://github.com/AFLplusplus/LibAFL/blob/main/libafl) ，一个包含可用于目标检测的公共代码的库， [libafl_targets](https://github.com/AFLplusplus/LibAFL/blob/main/libafl_targets) ，以及一个提供包装编译器的工具的库， [libafl_cc](https://github.com/AFLplusplus/LibAFL/blob/main/libafl_cc) 。

LibAFL 提供了与流行的仪器框架的集成。目前，支持的后端有:

*   清理覆盖，在 [libafl_targets](https://github.com/AFLplusplus/LibAFL/blob/main/libafl_targets)
*   Frida，在 [libafl_frida](https://github.com/AFLplusplus/LibAFL/blob/main/libafl_frida) ，到 s 1341【github@shmarya.net】T2(Windows 支持坏了 atm，就靠[这个上游问题](https://github.com/meme/frida-rust/issues/9)来修复。)
*   更多(QEMU 模式，…)

**入门**

1.  安装 Rust 开发语言。我们强烈建议*而不是*使用例如您的 Linux 发行包，因为这可能已经过时了。所以宁可直接安装铁锈，说明可以在[这里找到](https://www.rust-lang.org/tools/install)。
2.  使用以下命令克隆 LibAFL 存储库

**git 克隆 https://github.com/AFLplusplus/LibAFL**

使用构建库

**货物建造-发布**

使用构建 API 文档

**货物单据**

浏览 LibAFL 书籍(WIP！)与(需要 [mdbook](https://github.com/rust-lang/mdBook)

**cd 文档&MD book 服务**

我们收集了 **[`./fuzzers`](https://github.com/AFLplusplus/LibAFL/blob/main/fuzzers) 中所有的实例模糊化器。**一定要阅读他们的文档(和源代码)，这是*自然的入门方式！*

测试最好的 fuzzer 是 **[`./fuzzers/libfuzzer_libpng`](https://github.com/AFLplusplus/LibAFL/blob/main/fuzzers/libfuzzer_libpng)** ，一个多核的类似 libfuzzer 的 fuzzer，使用 LibAFL 作为 libpng 线束。

**资源**

*   [安装指南](https://github.com/AFLplusplus/LibAFL/blob/main/docs/src/getting_started/setup.md)
*   我们的 RC3 [谈话](http://www.youtube.com/watch?v=3RWkT1Q5IV0)解释核心概念
*   [在线 API 文档](https://docs.rs/libafl/)
*   LibAFL book(非常 WIP) [在线](https://aflplus.plus/libafl-book)或在[回购](https://github.com/AFLplusplus/LibAFL/blob/main/docs/src)

**投稿**

查看 [TODO.md](https://github.com/AFLplusplus/LibAFL/blob/main/TODO.md) 文件，了解我们计划支持的特性。

对于 bug，请随时提出问题或直接联系我们。谢谢你的支持。<3

尽管我们很乐意帮助你完成你的公关，但请尽量

*   使用*稳定*防锈
*   在推送之前，在您的代码上运行 **`cargo fmt`**
*   检查**的输出`cargo clippy --all`或`./clippy.sh`的输出**
*   运行`**cargo build --no-default-features**`来检查`**no_std**`的兼容性(可能还要加上 **`#[cfg(feature`** `**= "std")]**`)来隐藏部分代码。

这个列表中的一些部件可能很难，如果你自己不能修复它们，不要害怕打开 PR，所以我们可以帮助你。

[**Download**](https://github.com/AFLplusplus/LibAFL)