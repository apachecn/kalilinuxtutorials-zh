# Dumpscan:从内核和 Windows 小型转储格式中提取和转储机密的工具

> 原文：<https://kalilinuxtutorials.com/dumpscan/>

[![](img/dfda0cce4dfbbde409994163c080b84b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjZkJIvAYSh24Ut7u7XbpgIEpdrQJY_IfhyZBGKC_Y2woCSnbWPlN1YQnCG0b47eoMiZramR5js3XAYWVxrowDDRel-DLj9OK4XlDHbHg4ddVNijhA-HnkLddF-flD-Zou8zSEciSIKq1njCb5d0WJymL4Jwn6K-afp6goJ1YSuLGJOPxCP2Ap_S2K-/s728/dumpscan%20(2).png)

**Dumpscan** 是一个命令行工具，用于从内核和 Windows 小型转储格式中提取和转储机密。内核转储解析由 volatility3 提供。

## 特性

*   x509 公钥和私钥(PKCS #8/PKCS #1)解析
*   符号加密解析
    *   支撑结构
        *   **sym crypt _ RSA key**–确定密钥结构是否也有私钥
    *   与在同一进程中找到的公共证书匹配
    *   更多的 SymCrypt 结构即将出现
*   环境变量
*   命令行参数

**注意**:测试仅在 Windows 10 和 11 64 位主机和进程上进行。请随意提交其他版本的问题。Linux 测试 TBD。

## 安装

作为命令行工具，建议使用 pipx 进行安装。这允许容易的更新，并且确保它被安装在它自己的虚拟环境中。

**pipx 安装 dumpscan
pipx 注入 dumpscan git+https://github . com/volatity foundation/volatity 3 # 39e 812 a**

## 使用

**Usage: dumpscan [OPTIONS] COMMAND [ARGS]…
Scan memory dumps for secrets and keys
╭─ Options ────────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ –help Show this message and exit. │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ───────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ kernel Scan kernel dump using volatility │
│ minidump Scan a user-mode minidump │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯**

对于提取证书的子命令，您可以提供`**--output/-o <dir>**`将任何发现的证书输出到磁盘。

### 内核模式

如上所述，内核分析是由 Volatility3 执行的。 **`cmdline`、`envar`** 、`**pslist**`是对挥发 3 插件的直接调用，而`**symcrypt**`、`**x509**`是自定义插件。

**Usage: dumpscan kernel [OPTIONS] COMMAND [ARGS]…
Scan kernel dump using volatility
╭─ Options ────────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ –help Show this message and exit. │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ───────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ cmdline List command line for processes (Only for Windows) │
│ envar List process environment variables (Only for Windows) │
│ pslist List all the processes and their command line arguments │
│ symcrypt Scan a kernel-mode dump for symcrypt objects │
│ x509 Scan a kernel-mode dump for x509 certificates │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯**

### 小型转储模式

支持 Windows 小型转储格式。

**注意**:这只是在 Windows 10+上的 64 位进程上测试过。32 位进程需要额外的工作，但不是优先事项。

**Usage: dumpscan minidump [OPTIONS] COMMAND [ARGS]…
Scan a user-mode minidump
╭─ Options ────────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ –help Show this message and exit. │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ───────────────────────────────────────────────────────────────────────────────────────╮
│ │
│ cmdline Dump the command line string │
│ envar Dump the environment variables in a minidump │
│ symcrypt Scan a minidump for symcrypt objects │
│ x509 Scan a minidump for x509 objects │
│ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯**

[**Download**](https://github.com/daddycocoaman/dumpscan)