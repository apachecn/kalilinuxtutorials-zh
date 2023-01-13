# Scilla:信息收集工具(DNS/子域/端口枚举)

> 原文：<https://kalilinuxtutorials.com/scilla/>

[![Scilla : Information Gathering Tool (DNS/Subdomain/Port Enumeration)](img/cd44f1c9f6e49ce7113a5f233b42ac8f.png "Scilla : Information Gathering Tool (DNS/Subdomain/Port Enumeration)")](https://1.bp.blogspot.com/-3XdYBto1zN4/X-J1h2X5iyI/AAAAAAAAIL0/trypd52OScM-z47qiab3lXclwmrARe20wCLcBGAsYHQ/s800/Scilla.gif)

**Scilla** 是一个信息收集工具(DNS/子域/端口枚举)。

**安装**

*   首先，在本地克隆回购

**git 克隆 https://github.com/edoardottt/scilla.git**

*   Scilla 具有外部依赖性，因此需要将它们拉入:

**去拿**

*   Linux(需要高 perms，使用 sudo 运行)

**make linux
make unlinux**

*   Windows(可执行文件只能在 scilla 文件夹中运行。别名？)

**制作窗口
制作解窗口
制作 fmt 运行 golang 格式化程序。
进行更新更新。
制作 remod Remod。
进行测试运行测试。**

**开始使用**

**scilla help** 在命令行打印帮助。

**用法:scilla[子命令] { options }

可用子命令:
–DNS {-target REQUIRED }
–子域{[-w word list]-target REQUIRED }
–port {[-p]-target REQUIRED }
–dir {[-w word list]-target REQUIRED }
–report {[-p]-target REQUIRED }
–help**

**例题**

*   DNS 枚举:

**scilla DNS-target . domain**

*   子域枚举:

**scilla 子域-目标 target.domain
scilla 子域-w word list . txt-目标 target.domain**

*   目录枚举:

scilla dir-target . domain
scilla dir-w word list . txt-target target . domain

*   端口枚举:
    *   默认(所有端口，so 1-65635) scilla 端口-目标目标.域
    *   指定端口范围 scilla port-P20-90-target target . domain
    *   指定起始端口(直到最后一个端口)scilla port-p 20--target target . domain
    *   指定结束端口(从第一个开始)scilla port-p-90-target target . domain
    *   指定单端口 scilla port-p 80-target target . domain

*   完整报告:
    *   默认(所有端口，so 1-65635) scilla 报告-目标目标.域
    *   指定端口范围 scilla 报告-第 20-90 页-目标目标.域
    *   指定起始端口(直到最后一个端口)scilla 报告-第 20 页--目标目标域
    *   指定结束端口(从第一个端口开始)scilla 报告-p-90-目标目标.域
    *   指定单端口 scilla 报告-p80-目标目标.域
    *   指定 word list scilla report-w word list . txt-target target . domain

[**Download**](https://github.com/edoardottt/scilla)