# BinAbsInspector:二进制漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/binabsinspector/>

[![](img/e0e848ee925f51aa22a05730483757b3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhIW6wybVZj2tYenihqyCfCMxYRVtN5d1P72pcYGpWBQrWeSen4lu_m5SOocq-FpBrDHzM0e7b66JQE_kCXp36pSIyhqquptkN66Dv0F8DbJzIbh4AIkxAqbv-nV0CE573nZ35DdRMpL3n9AxApULJD5oPzsXXHwF4vEGTCsXrpLi15FBPWWovtyvS8/s728/binary%20(1).png)

**binabs Inspector**(Binary Abstract Inspector)是一个用于自动化逆向工程和扫描二进制文件中漏洞的静态分析器，是在 Keenlab 孵化的长期研究项目。它是基于抽象的解释，并得到了吉卓的支持。它在 Ghidra 的 Pcode 上工作，而不是汇编。目前它支持 x86、x64、armv7 和 aarch64 上的二进制文件。

# 安装

*   根据 Ghidra 的文件安装 Ghidra
*   安装 Z3(测试版本:4.8.15)
*   注意，Z3 库一般有两个部分:一个是 Java 包，另一个是原生库。Java 包已经包含在“/lib”目录中，但是为了版本兼容性，我们建议您用自己的 Java 包替换它。
    *   对于 Windows，从这里下载一个预构建的包，解压 zip 文件并添加一个指向`**z3-${version}-win/bin**`的 PATH 环境变量
    *   对于 Linux，不建议安装软件包管理器，有两个选项:
        *   您可以从这里下载合适的预编译包，解压 zip 文件并将`**z3-${version}-win/bin/*.so**`复制到`**/usr/local/lib/**`
        *   或者你可以使用 make 和 GCC/Clang 按照构建 z3 来构建和安装 Z3
    *   对于 MacOS 来说，和 Linux 差不多。
*   从发布页面下载扩展 zip 文件
*   根据 Ghidra 扩展注释安装扩展

# 建筑

自己构建扩展，如果你想开发一个新功能，请参考开发指南。

*   安装 Ghidra 和 Z3
*   安装 Gradle 7.x(测试版本:7.4)
*   提取存储库
*   在存储库根目录下运行`**gradle buildExtension**`
*   扩展将在`**dist/${GhidraVersion}_${date}_BinAbsInspector.zip**`生成

# 用法

您可以在 headless 模式、GUI 模式或 docker 中运行 BinAbsInspector。

*   用 Ghidra 无头模式。

**$ GHIDRA _ INSTALL _ DIR/support/analyze headless-import-postScript binabs inspector " @ @ "**

`**<projectPath>**` — Ghidra 项目路径。
`**<projectName>**` — Ghidra 项目名称。
`**<scriptParams>**` —该参数为我们的分析器提供了以下选项:

| 参数 | 描述 |
| --- | --- |
| `**[-K <kElement>]**` | KSet 大小限制 K |
| `**[-callStringK <callStringMaxLen>]**` | 调用字符串最大长度 K |
| `**[-Z3Timeout <timeout>]**` | Z3 超时 |
| `**[-timeout <timeout>]**` | 分析超时 |
| `**[-entry <address>]**` | 入口地址 |
| `**[-externalMap <file>]**` | 外部功能模型配置 |
| `**[-json]**` | json 格式的输出 |
| `**[-disableZ3]**` | 禁用 Z3 |
| `**[-all]**` | 启用所有检查器 |
| `**[-debug]**` | 启用调试日志输出 |
| `**[-check "<cweNo1>[;<cweNo2>...]"]**` | 启用特定的检查器 |

*   使用 Ghidra GUI
    *   运行 Ghidra 并将目标二进制文件导入到项目中
    *   使用默认设置分析二进制文件
    *   分析完成后，打开`**Window -> Script Manager**`并找到`**BinAbsInspector.java**`
    *   双击`**BinAbsInspector.java**`条目，在配置窗口中设置参数，点击确定
    *   当分析完成后，你可以在控制台窗口中看到 CWE 报告，从报告中双击地址可以跳转到相应的地址
*   使用 Docker

**git 克隆 git @ github . com:keensecurityabr/binbsinspector . git
CD binbsinspector
dock build。-t bai
坞站运行-v $(pwd):/data/workspace Bai @ @**

# 实现的检查器

到目前为止，BinAbsInspector 支持以下检查器:

*   CWE78(操作系统命令注入)
*   CWE119(缓冲区溢出(一般情况))
*   CWE125(缓冲区溢出(越界读取))
*   CWE134(使用外部控制的格式字符串)
*   CWE190(整数溢出或回绕)
*   CWE367(检查时间使用时间(TOCTOU))
*   CWE415(双自由)
*   CWE416(免费后使用)
*   CWE426(不受信任的搜索路径)
*   CWE467(在指针类型上使用 sizeof()
*   CWE476(空指针取消引用)
*   CWE676(潜在危险功能的使用)
*   CWE787(缓冲区溢出(越界写入))

# 项目结构

该项目的结构如下，请参阅技术细节了解更多详情。

**【主要】
【Java】
【com】
【Bai】
【检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查人员实施检查**

也可以用`**gradle javadoc**`构建 javadoc，API 文档会在`**./build/docs/javadoc**`中生成。

[**Download**](https://github.com/KeenSecurityLab/BinAbsInspector)