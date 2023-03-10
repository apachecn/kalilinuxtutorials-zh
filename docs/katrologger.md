# KatroLogger:用于 Linux 系统的键盘记录器

> 原文：<https://kalilinuxtutorials.com/katrologger/>

[![KatroLogger : KeyLogger for Linux Systems](img/35507579f331de3cd8a76158b6c06dc8.png "KatroLogger : KeyLogger for Linux Systems")](https://1.bp.blogspot.com/-amQUy91HWtc/Xvi3RA6b3xI/AAAAAAAAGvM/ooZqqlOD3JAeem0tRzqEy3vUPY4IRZhswCLcBGAsYHQ/s1600/keylogger%25281%2529.png)

KatroLogger 是一个用于 Linux 系统键盘记录的工具。

**特性**

*   在 GUI 系统或 CLI 上运行
*   通过电子邮件发送数据

**依赖关系**

*   卷曲
*   libx11-dev(基于 Debian)
*   libX11-devel(位于 RHEL)

**编译**

**。/configure
make
make install**

**也可阅读-[图集:快速 SQLMap 篡改提示器 v 1.0](https://kalilinuxtutorials.com/atlas-2/)**

**用途**

**katrologger–输出/路径/文件**

通过电子邮件发送数据:

**katrologger–SMTP-help**

*   **修复通过 SSH 访问的问题**

> 当通过 ssh 远程连接到受害者时，需要导出环境变量来运行键盘记录器。

*   **对于运行 xorg 的主机:**

识别登录用户

**user = $(who | grep "(:0)" | awk ' { print $ 1 } ')
echo $ user**

**导出变量**

**export DISPLAY =:0.0
export x authority =/home/$ user/。权威**

**卸载**

**进行卸载**

[**Download**](https://github.com/Katrovisch/KatroLogger)