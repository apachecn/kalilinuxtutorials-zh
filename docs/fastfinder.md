# 快速查找器:事件响应–快速可疑文件查找器

> 原文：<https://kalilinuxtutorials.com/fastfinder/>

[![](img/0b8a72b6a6b28dbe40a5a2e79db57189.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjWZWgIhi2IxczVLAdpZAvH4FTm8oeAuUOC-yECe364sKlrylMQUoIxQ6Yid-Cnoaiewl3qI96Xh1R_5gP5ZtV0KjW0_5WiUptGIe01s6clU2QjsOxnMUOWXPD2oUQHxPdhr8NY18QSrCkpI5N3XQPT_xUYCZgQqk0ghWT2ZUdu95bCaxC7mtZiJnVD/s728/Icon%20(1).png)

FastFinder 是一款轻量级工具，用于 Windows 和 Linux 平台上的威胁追踪、实时取证和分类。它侧重于端点枚举和基于各种标准的可疑文件查找:

*   文件路径/名称
*   md5 / sha1 / sha256 校验和
*   简单字符串内容匹配
*   基于 YARA 的复杂内容条件

## 准备战斗！

*   fastfinder 已经在多个 CERT、CSIRT 和 SOC 使用案例中的真实案例中进行了测试
*   示例目录现在包括真实的恶意软件/可疑行为或漏洞扫描示例

### 安装

此软件的编译版本可用。如果你想从源代码编译，这可能有点棘手，因为它强烈依赖于 *go-yara* 和 CGO 编译。无论如何，你会找到 windows 和 linux 的详细文档

### 用法

***_ _*_*_*_
|*_/\/` | | | | \ | | \ | _*|/~ \。/| | | | | |/| _ | \
2021-2022 | Jean-Pierre GARNIER | @ codeyourweb
https://github.com/codeyourweb/fastfinder
用法:Fast finder[-h |–help][-c |–configuration " "][-b |–build
" "][-o |–output " "][-n |–no-window]
[-u |–no-user interface][-v |–verbosity]
[-t |–triage]]默认:
-b–将配置和
规则以单个二进制文件的形式构建输出独立包
-O–输出将 fastfinder 日志保存在指定文件中
-n–无窗口隐藏 fastfinder 窗口
-u–无用户界面隐藏高级用户界面
-v–详细度文件日志详细度
| 4:仅警报
| 3:警报和错误
| 2:警报、错误和 I/O 操作
| 1:完整详细默认值:3
-t–Triage Triage 模式(无限运行–扫描
输入路径目录中的每个新文件)。默认:假**

根据你在哪里寻找文件， *FastFinder* 可以使用管理员或简单用户权限。

### 根据需要扫描和导出文件匹配

那里提供了配置示例

**输入:
路径:[] #基于简单字符串匹配文件路径和/或文件名
内容:
grep: [] #匹配文件内容中的文字字符串值
yara: [] #使用 yara 规则并指定规则路径以进行更复杂的模式搜索(通配符/正则表达式/条件)
校验和:[] #解析文件内容中的 MD5/sha1/sha 256
选项:
contentMatchDependsOnPathMatch:true #如果为 true，则路径是内容的预过滤器如果为假， 路径和内容都生成匹配
findInHardDrives: true #枚举硬盘内容
findInRemovableDrives: true #枚举可移动驱动器内容
findInNetworkDrives: true #枚举网络驱动器内容
findInCDRomDrives: true #枚举物理 CD-ROM 和挂载的 iso/vhd…
output:
copy matching files:true #创建每个匹配文件的副本
base64Files: true # base64 在复制之前匹配内容
文件 空值将复制 fastfinder 文件夹中匹配的文件
advanced parameters:
yar arc 4k ey:" # yara rules 可以使用指定的 RC4 密钥进行(不)加密
maxScanFilesize: 2048 #忽略最大 maxScanFileSize Mb 的文件(默认值:2048)
cleanMemoryIfFileGreaterThanSize:512 #在大量文件扫描后清理 fastfinder 内部内存(默认值:512Mb)**

### 在任何地方或指定路径中搜索:

*   使用“？”在简单字符通配符的路径中(例如，powershe？？。exe)
*   在路径中使用“\*”作为多字符通配符(例如\*。exe)
*   正则表达式也是可用的，只需用斜杠(例如/[0-9]{8})将路径括起来。exe/)
*   也可以使用环境变量(如%TEMP%\myfile.exe)

### 重要提示

*   输入路径总是不区分大小写
*   字符串内容搜索(grep)总是区分大小写的
*   反斜杠不应该被转义(除了正则表达式)。更多信息，请看例子

[**Download**](https://github.com/codeyourweb/fastfinder)