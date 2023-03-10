# 在 Debian/Ubuntu/Linux Mint 上获得你最喜欢的 Kali Linux 工具

> 原文：<https://kalilinuxtutorials.com/katoolin3/>

[![](img/f4506fe2c39738aa6a65d739674f17db.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjQ67VWuR00bxhp5spJ9gdXMhK4Sij0vaEte8tkdWoyEGwJGokS8SGGnU9x6lsws4CbvE7SnvSXeSOMojARBRLoKCVOIMqopjC8Jdn3Yq0AIK1C4nfQJQtNkJjneydhJyRLGZjGG-7F64QDFDECY3Qs0-p3nmGwuK-yUo-1v7aFUYoc4_ylT7_MatyI/s728/Install-Kali-Linux-Tools-Using-Katoolin3-In-Ubuntu-1.png)

kato ulin 3 将 Kali Linux 中所有可用的程序带到 Debian 和 Ubuntu 上。

这个程序是从 LionSec 到 python3 的 katoolin 的一个端口。katoolin 3 提供了对 kato ulin 的几项改进:

*   最新软件包
    老卡图林用的是过时的软件包列表。Katoolin3 总是保持它的包列表是最新的。
    *(最后更新时间:2020 年 2 月 18 日)*
*   改进了对丢失包的处理
    如果仓库中不再有可用的包，旧的 katoolin 就会崩溃。Katoolin3 检测到这些，并简单地忽略它们。
*   **移除软件包**
    你现在可以移除所有由 katoolin3 安装的软件包(单独或一次全部移除)。
*   升级不会再破坏你的系统
    …因为 Kali 库只在 katoolin3 运行时启用。
*   **更好地利用 APT 生态系统**
    旧的 katoolin 会进行潜在的危险操作，例如修改和*删除*重要的系统配置文件。这个已经改了。
*   更容易维护 Kalis 软件包
    由于 katoolin 的编程方式，旧的 katoolin 很难将新的软件包添加到软件包列表中。维护包列表现在容易多了。
*   更干净的代码
    由于糟糕的代码质量，卡托林无法维护，不得不从头开始重写。katoolin3 的目标是可读性更强，更易于维护。

### 给 Ubuntu 用户的警告

从不同操作系统的存储库中安装程序通常被认为是危险的！一些软件包可能会破坏你的系统。安装工具时要小心，不要因为任何不便而责怪 katoolin3。
最佳解决方案是安装来自 tools.kali.org 的特定工具。
不建议安装所有工具。

### 要求

*   apt 作为一个包管理器
*   Python >= 3.5
*   Root 权限
*   嘘，巴什
*   python3-apt

### 安装

**git 克隆 https://github.com/s-h-3-l-l/katoolin3;
CD 卡托林 3；
chmod+x ./install . sh；
须藤。/install . sh；**

**重要提示:**如果你得到错误`**Please install the python3-apt package**`，请确保 katoolin3 运行的 python3 版本与`**python3-apt**`包完全相同。在现代发行版上`**python3-apt**`只适用于 python3.7，在旧发行版上`**python3-apt**`只适用于 python3.5。katoo lin3 必须相应地运行 python3.7 或 python 3.5

### 用法

katoolin3 的程序流程是通过呈现一个可供选择的选项列表来实现的。这些列表如下所示:

**0)……
1)……
2)……**

#### 安装工具

要安装软件包，请输入相应的号码。要一次安装多个包，可以指定一个像`**3-5**`一样的范围，一个像`**1,2,3**`一样的列表，或者像 **`1,2,5-7,9`一样组合它们。**你也可以一次安装所有的软件包。

#### 卸载工具

这就像安装一样，除了您必须在选择之前加上一个`**~**`。您也可以一次卸载所有软件包。

#### 搜索

Katoolin3 支持搜索包缓存。
例如，如果您想安装一些与 SQL 注入相关的工具，您可以进入搜索菜单并搜索`**sql injection**`。
如果您想了解某个包的具体信息，只需在同一个搜索菜单中输入包名。

如需更多功能，请参见程序中的帮助对话框。

### 更新

要更新您的工具列表，请执行

**chmod+x ./update . sh；
须藤。/update . sh；**

### 卸载

要卸载 katoolin3，请执行

**chmod+x ./uninstall . sh；
须藤。/uninstall . sh；**

卸载 Kali 工具可以在 katoolin3 内部完成。

[**Download**](https://github.com/s-h-3-l-l/katoolin3#installing-tools)