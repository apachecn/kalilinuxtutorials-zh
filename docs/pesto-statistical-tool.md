# PESTO–PE(文件)统计工具

> 原文：<https://kalilinuxtutorials.com/pesto-statistical-tool/>

[![PESTO – PE (Files) Statistical Tool](img/9c2a46a0b744e328b30d94fc5e939bfd.png "PESTO – PE (Files) Statistical Tool")](https://1.bp.blogspot.com/-pyN4tEGV7w4/XbwKuE-OwkI/AAAAAAAADNw/sFhPsqGkuUYN2DsRlWaA8jjTbamEr-JYACLcBGAsYHQ/s1600/Pesto%25281%2529.png)

**PESTO** 是一个 Python 脚本，它在数据库中提取并保存一些 PE 文件安全特征或标志，在整个目录中搜索每个 PE 二进制文件，并将结果保存在数据库中。

PESTO 检查报头中的架构标志，以及以下安全标志:ASLR、SEH、DEP 和 CFG。代码足够清晰，可以根据自己的需要修改标志和格式。

**功能**

这个脚本只需要一个路径和一个标签。该程序将通过路径和子目录搜索。DLL 和。EXE 文件并提取 PE 头中的标志(多亏了 PEfile python 库)。

**也可阅读-[pock int:为 DFIR/OSINT 专业人士准备的便携式 OSINT 瑞士军刀](http://kalilinuxtutorials.com/pockint-portable-osint-swiss-army-knife-dfir-osint/)**

该程序需要一个标记，该标记将用作日志和数据库文件名的后缀，因此可以在同一个目录中进行不同的分析。

该脚本提供的信息是:

*   的百分比。DLL 和。EXE 文件与 i386，AMD64，IA64 或其他架构。
*   标题中启用或禁用的 ASLR、SEH、DEP 和 CFG 标志的百分比。
*   完成分析后，它会提示以 SQL 或 CSV 格式导出结果。

它还将创建一个. db 文件，这是一个包含收集到的信息的 sqlite 文件。

[**Download**](https://github.com/ElevenPaths/PESTO)