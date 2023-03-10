# AD Explorer Snapshot . py:AD Explorer 快照解析器。这是给警犬做的食物

> 原文：<https://kalilinuxtutorials.com/adexplorersnapshot-py/>

[![](img/b984c8e61b01456b4369a7a9e2d2e361.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhblInMN8o8Hr6_yxzMXyKwV-dEAfWTslorX6Hl3a16betzuH2Asxs2MLTjer769MwexA2w5I57nkf0rjtvZidI2O0y5UiUGSiHqzGsqFL19r6Grd475mKEX7XyulldA2yj2sg7UBK_gwKY_G6_wg_9G9Vijvq12mqLnxSvCf-uHOkghkYVRvU-AB5G/s728/1_Vv8DHzogGhdqEq0SKg3f0Q%20(1).png)

**ADExplorerSnapshot.py** 是一个广告浏览器快照解析器。它是作为 BloodHound 的一个入口，也支持全对象转储到 NDJSON。

AD Explorer 允许您连接到 DC 并浏览 LDAP 数据。它还可以创建您当前连接的服务器的快照。该工具允许您将这些快照转换为 BloodHound 兼容的 JSON 文件，或者将快照中所有可用的对象转储到 NDJSON 以便于处理。

## 支持什么

在`**BloodHound**`输出模式下:

*   用户集合
*   组集合
*   计算机收藏
*   信任集合(从您连接的 LDAP DC 中可见)

在`**Objects**`输出模式中，每个对象的所有属性都被解析并输出为 NDJSON 格式。

## 限制

用于 BloodHound 的 ingestor 仅支持从快照文件中离线收集信息，不会与网络上的系统进行交互。这意味着会话和 localadmin 集合等功能不可用。缺少 GPO/OU 集合。ingestor 尽可能处理来自快照的所有数据(包括 ACL)，但只会输出 BloodHound 可以解释的 JSON 数据。您将只有运行快照时所针对的 LDAP/DC 的数据可用。

## 安装

ADExplorerSnapshot.py 支持 Python 3.6+。依赖关系通过 pip 管理。

**git 克隆 https://github.com/c3c/ADExplorerSnapshot.py.git
CD adexplorersnapshot . py
pip 3 安装–用户。**

## 使用

**用法:adexplorersnapshot . py[-h][-o OUTPUT][-m { blood hound，Objects }]snapshot
adexplorersnapshot . py 是一个 AD Explorer 快照解析器。它是作为 BloodHound 的一个入口，也支持全对象转储到 NDJSON。
位置参数:
快照的快照路径。dat 文件。
可选参数:
-h，–help 显示此帮助信息并退出
-o OUTPUT，–OUTPUT 输出
路径到*。json 输出文件夹。如果文件夹不存在，将创建它。
默认为当前目录。
-m {BloodHound，Objects}，–mode { blood hound，Objects}
要使用的输出模式。除了 BloodHound JSON 输出文件之外，
还可以将所有对象及其所有属性转储到 nd JSON。
默认为 BloodHound 输出模式。**

## 笔记

这个库现在支持 BloodHound v4.1+输出格式(JSON 格式 v4)。对于旧的 v3 输出格式，可以使用 v3-format 分支中的代码。

与传统的 BloodHound ingestors 相比，在 AD Explorer 中制作快照会占用更多的网络资源，因为它会尝试从 LDAP 中检索所有可能的对象。

ADExplorerSnapshot.py 将创建信息缓存，以便在处理数据时更快地查找。尤其是在处理较大的快照(例如 4GB 以上)时，您还需要有足够的可用 RAM。在我的测试中，RAM 中需要大约一半的快照文件大小。

该库已通过大量数据集测试，如果遇到问题，请创建问题报告。

AD Explorer 快照解析器作为其自己的模块实现，也可以单独使用。

AD Explorer 存储快照的格式是专有的，这导致了一次有趣的逆向工程之旅。这个存储库中包含一个 010 编辑器模板，我用它迭代地将快照的内容映射到结构中。

[**Download**](https://github.com/c3c/ADExplorerSnapshot.py)