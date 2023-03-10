# 一个网络枚举和攻击工具集

> 原文：<https://kalilinuxtutorials.com/activereign-network-enumeration-attack-toolset/>

[![ActiveReign : A Network Enumeration & Attack Toolset](img/3fc5c25f62700ffd949ef420243f5c0c.png "ActiveReign : A Network Enumeration & Attack Toolset")](https://1.bp.blogspot.com/-1yqU4Wjg6Dc/XXc0fs_BVHI/AAAAAAAACdg/OwZ85WsphXwl229IhsS4rsWtuXgL1edSgCLcBGAs/s1600/ActiveReign%2B%25281%2529.png)

**active region**是一个网络枚举和攻击工具集。不久前，我被挑战用 Python3 编写一个发现工具，它可以自动发现网络文件共享上的敏感信息。在用 pysmb 编写了整个工具，并添加了诸如打开和扫描 docx 和 xlsx 文件的功能之后。

我们慢慢开始添加来自牛逼的 Impacket 库的功能；只是我想在内部渗透测试工具中看到的简单特性。我添加的越多，它就越像是从头开始创建的 CrackMapExec 的 Python3 重写版。

如果你做一个直接的比较，CME 是一个令人惊奇的工具，它有比目前这里实现的更多的特性。然而，我添加了一些修改，在评估过程中可能会派上用场。

**也可以理解为-[PyFuscation:通过替换函数名、变量&参数](https://kalilinuxtutorials.com/pyfuscation-function-names-variables-parameters/)来混淆 Powershell 脚本**

**运行模式**

*   db–在 ActiveReign 数据库中查询或插入值
*   枚举–系统枚举和模块执行
*   shell–在目标系统上生成模拟 shell
*   喷射-域密码喷射和暴力破解
*   查询–在域上执行 LDAP 查询

**主要特征**

*   通过 LDAP 自动提取域信息并合并到网络枚举中。
*   使用 LDAP 执行域密码喷洒，删除接近锁定阈值的用户。
*   本地和远程命令执行，用于整个网络的多个起始点。
*   目标系统上的模拟交互式外壳
*   能够扫描 xlsx 和 docx 文件的数据发现。
*   添加和扩展功能的各种模块。

**最终想法**

编写这个工具并在各种网络/系统上进行测试让我明白了执行方法的重要性，它取决于系统的配置。如果某个特定模块或功能不起作用，请在产生问题之前确定它实际上是程序、目标系统、配置还是网络布局。

为了帮助这个调查过程，我创建了一个`test_execution`模块，在一个具有已知管理员权限的系统上运行。这将循环所有的执行方法，并提供一个状态报告，以确定要使用的最佳方法:

$ active region Enum-u administrator-p Password–local-auth-M test _ execution 192 . 168 . 3 . 20
[*]使用默认锁定阈值的锁定跟踪器:3
[*]Enum authentic ation \ administrator(Password:p * * * *)(Hash:False)
[+]WIN-T460 192 . 168 . 3 . 20 Enum Windows 7 Ultimate 7601 Service Pack 1(Domain:)(Signing:False)(SMB v1:True)(Adm！n)
[*]WIN-T460 192 . 168 . 3 . 20 TEST _ EXECUTION 执行方法:WMIEXEC file less:SUCCESS Remote(default):SUCCESS
[*]WIN-T460 192 . 168 . 3 . 20 TEST _ EXECUTION 执行方法:SMBEXEC file less:SUCCESS Remote(default):SUCCESS

[**Download**](https://github.com/m8r0wn/ActiveReign)