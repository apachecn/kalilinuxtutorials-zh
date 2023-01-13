# Droidefense:高级 Android 恶意软件分析框架

> 原文：<https://kalilinuxtutorials.com/droidefense-engine-android-malware/>

**droid defense**是 android 应用/恶意软件分析/逆转工具的代号。它主要关注恶意软件研究人员在日常工作中遇到的安全问题和技巧。

对于恶意软件具有**反分析**例程的情况，Droidefense 试图绕过它们，以获取代码和“坏小子”例程。

有时这些技术可以是虚拟机检测、仿真器检测、自我证书检查、管道检测。tracer pid 检查等等。

droid defense 使用了一个创新的想法，即代码不是被反编译而是被查看。

这使我们能够以 100%的准确率获得代码执行工作流的全局视图。在这种情况下，**droid defense**会生成一个漂亮的 **html** 报告，其中的结果很容易理解。

**也可阅读-[H2T:HTTP 加固工具扫描网站&建议应用安全报头](https://kalilinuxtutorials.com/h2t-http-hardening/)**

**机器人防御功能**

*   。apk 拆包机
*   。apk 资源解码器
*   。apk 文件枚举
*   。apk 文件分类和识别
*   二进制 xml 解码器
*   使用虚拟文件系统的内存处理
*   资源模糊和散列
*   熵计算器
*   本机代码转储
*   证书分析
*   调试证书检测
*   操作码分析
*   未使用操作码检测
*   androidManifest.xml 分析
*   内部结构分析
*   达尔维克字节码流分析
*   多路径分析实施(未测试)
*   CFG 生成
*   简单反射分解器
*   字符串分类
*   模拟工作流生成
*   动态规则引擎

**机器人防御模块**

*   PSCout 数据模块
*   完整的 Android 清单解析器，基于官方 SDK 文档 v23。
*   插件
*   机器学习(基于 Weka)模块

**droid defense 外挂**

*   隐藏的 ELF 文件检测器插件
*   隐藏的 APK 文件检测器插件
*   应用程序 UID 检测器插件
*   隐私插件

**用法**

**TL；博士**

**Java-jar droid defense-CLI-1.0-snapshot . jar-I/path/to/your/sample . apk**

**详细用法**

**Java-jar droid defense-CLI-1.0-snapshot . jar
当前构建:2018_03_09__09_17_34
在 Github 上查看:https://github.com/droidefense/
报告您的问题:https://github.com/droidefense/engine/issues
首席开发者:@zerjioang
用法:droid defense
-d，–debug 打印调试信息
-h，–帮助打印此消息
-i，–input 输入。要分析的 apk
-o，–output select preferred output:
JSON
JSON . min
html
-p，–profile Wait for JVM profiler
-s，–show 显示扫描后生成的报告
-u，–unpacker select preferred unpacker:
zip
memapktool
-V，–verbose be verbose
-V，–version 显示当前版本信息**

[**Download**](https://github.com/droidefense/engine)