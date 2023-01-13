# 进攻:红队交战的铁锈武器化

> 原文：<https://kalilinuxtutorials.com/offensiverust-rust/>

[![](img/35a6e5fc2b2c202d9f22571cbe3d797e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhHvMpaNWAP6F5VrZgGOivHFFjL9wpMd-MyUGL7J85b8Rk7FnYuW1vY0xtp1qscZgHCrRDNYH9odV0P5ghK-tw20Vcj9Paqc98IE9TX26Yr9V78sEu-bm7cZ6PfBWFwTQ-9UJxAAbRe6iG2DsYspmQz-id1EN1i6xdELiJNYp8kTikbUXwmFTeJidXu=s728)

**进攻型**，我为了植入物开发和一般进攻作战而进行的铁锈武器化实验。

**为什么会生锈？**

*   它比像 C/C++这样的语言更快
*   它是多用途语言，承载着优秀的社群
*   它有一个惊人的内置依赖构建管理，称为 Cargo
*   它是基于 LLVM 的，这使它成为绕过静态 AV 检测的非常好的候选
*   从*nix/MacOS 到 Windows 的超级简单交叉编译，只需要你安装`**mingw**`工具链，尽管某些库不能在其他操作系统中成功编译。

**本回购中的例子**

| 文件 | 描述 |
| --- | --- |
| Allocate_With_Syscalls | 它通过 ntapi 库直接使用 NTDLL 函数 |
| 创建动态链接库 | 创建 DLL 并弹出一个 msgbox，Rust 不完全支持这个，所以事情可能会变得很奇怪，因为 Rust DLL 没有主函数 |
| 设备控制 | 打开驱动程序句柄并执行 DeviceIoControl |
| 启用调试权限 | 在当前进程中启用 SeDebugPrivilege |
| Shellcode_Local_injec [t](https://github.com/trickster0/OffensiveRust/blob/master/Shellcode_Local_inject/src/main.rs) | 通过强制转换指针直接在本地进程中执行外壳代码 |
| 用命令执行 | 通过 Rust 传递命令来执行 cmd |
| ImportedFunctionCall | 它从 dbghelp 导入小型转储并执行它 |
| 内核驱动程序利用 | 简单缓冲区溢出的内核驱动程序漏洞 |
| 命名管道客户端 | 命名管道客户端 |
| 命名管道服务器 | 命名管道服务器 |
| 流程 _ 注入 _ 创建线程 | 使用 CreateRemoteThread 在远程进程中进行进程注入 |
| 解开 | 挂断电话 |
| asm _ 系统调用 | 通过 asm 获取 PEB 地址 |
| base64 _ 系统 _ 枚举 | Base64 编码/解码字符串 |
| http-https-请求 | 通过忽略 GET/POST 的证书检查的 HTTP/S 请求 |
| 补丁 _etw | 补丁 ETW |
| ppid_spoof | 为创建的进程欺骗父进程 |
| tcp _ ssl _ 客户端 | 使用 SSL 的 TCP 客户端忽略证书检查(需要安装 openssl 和 perl 进行编译) |
| tcp _ ssl _ 服务器 | TCP 服务器，带端口参数(需要安装 openssl 和 perl 进行编译) |
| wmi_execute | 执行 WMI 查询以获取主机中的 AV/EDRs |
| Windows.h+绑定 | 这个文件包含了 Windows.h 的结构以及完整的 LDR、PEB 等自定义文件..这是微软官方没有记录的，在你的文件顶部添加 include！("../bindings . RS ")； |
| UUID _ 外壳代码 _ 执行 | 将外壳代码从 UUID 数组植入堆空间，并使用`**EnumSystemLocalesA**`回调来执行外壳代码。 |

**整理本回购中的例子**

这个库不提供二进制文件，你必须自己编译它们。

安装 Rust
只需下载二进制文件并安装即可。

这个回购是在 Windows 10 中编译的，所以我会坚持使用它。如前所述，OpenSSL 二进制文件会有依赖问题，需要安装 OpenSSL 和 perl。对于 TCP SSL 客户机/服务器，我推荐静态构建，因为它依赖于将要执行二进制文件的主机。创建项目时，执行:
`**cargo new <name>**`这将自动创建结构化项目文件夹，其中包含:

**项目
收费。toml
src
main . RS**

Cargo.toml 文件包含编译的依赖项和配置。main.rs 是将与包含库的任何潜在目录一起编译的主文件。

编译项目时，进入项目目录，执行:
`**cargo build**`

这将使用您的默认工具链。如果你想构建最终的“发布”版本，执行:
`**cargo build --release**`

对于静态二进制，在终端 build 命令执行前:
**`"C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat"`
`set RUSTFLAGS=-C target-feature=+crt-static`**

如果你觉得阅读我写的代码不容易，
你也可以在项目目录中使用下面的命令以更好的方式格式化它
`**cargo fmt**`

某些例子可能无法编译并给你一些错误，因为它可能需要每晚用最新的特性构建 Rust。要安装它只需做:
`**rustup default nightly**`

最容易找到附属品或所谓的板条箱的地方。

**交叉编译**

交叉编译需要按照这里的说明安装不同的工具链，你可以使用下面的命令
`**cargo build --target <toolchain>**`进行交叉编译

要查看系统上安装的工具链，请执行:
`**rustup toolchain list**`

要检查您可以在系统中安装的所有可用工具链，请执行:
`**rustup target list**`

要安装新的工具链，请执行:
`**rustup target add <toolchain_name>**`

**优化可执行文件大小**

这个 repo 包含了很多关于减少文件大小的配置选项和想法。静态二进制文件通常很大。

**陷阱我发现自己掉进了**

小心\0 字节，不要忘记它们是内存中的字符串，我花了很多时间，但 windbg 总是帮助解决它。

**有趣的锈库**

*   WINAPI
*   WINAPI2
*   windows——这是微软的官方版本，我没怎么玩过

**OPSEC**

*   尽管 Rust 有很多优点，但是很难习惯它，而且它也不是很直观。
*   外壳代码生成是 LLVM 带来的另一个问题。我已经找到了一些方法来解决这个问题。Donut 有时会生成有用的外壳代码，但根据项目的制作方式，也可能不会。
    一般来说，对于外壳代码生成，所制作的工具应该能够在。文本片段，这导致了这个惊人的回购。这个项目中有一个 shellcode 示例，它可以向您展示如何构建代码以成功生成 shellcode。
    此外，这个项目还有一个外壳代码生成器。二进制和的文本段，并在执行一些补丁后转储外壳代码。
    这个项目从一个特定的位置获取二进制文件，所以我做了一个 fork，在这里接收二进制文件的路径作为参数。
*   即使您删除了所有调试符号，rust 仍然可以在二进制文件中保留对您的主目录的引用。我发现消除这种情况的唯一方法是传递下面的标志:`**--remap-path-prefix {your home directory}={some random identifier}**`。您可以使用 bash 变量来获取您的主目录并生成一个随机占位符:`**--remap-path-prefix "$HOME"="$RANDOM"**`。(作者山口百惠)
*   尽管对于上述内容，还有另一种方法可以通过在 Cargo.toml
    **`cargo-features = ["strip"]`的顶部添加来删除关于主目录的信息。**
*   由于 Rust 默认会在二进制文件中留下很多字符串，所以我主要使用这个 cargo.toml 来避免它们，并使用 build 命令
    `c**argo build --release -Z build-std=std,panic_abort -Z build-std-features=panic_immediate_abort --target x86_64-pc-windows-msvc**`减小大小

[**Download**](https://github.com/trickster0/OffensiveRust)