# Dnx 防火墙——构建在 Linux 内核/Netfilter 之上的纯 Python 下一代防火墙

> 原文：<https://kalilinuxtutorials.com/dnx-firewall/>

[![Dnx Firewall – A Pure Python Next Generation Firewall Built On Top Of Linux Kernel/Netfilter](img/77392e836416913f57d8f1b512578a5a.png "Dnx Firewall – A Pure Python Next Generation Firewall Built On Top Of Linux Kernel/Netfilter")](https://1.bp.blogspot.com/-UqBYSeM2fx0/X2utDuJ3ZgI/AAAAAAAAHpQ/GVfEiE6G3DMcBLXdD10Sw7s54txGtsnPQCLcBGAsYHQ/s728/dnxlogo_v2%25281%2529.png)

**DNX 防火墙**是一个优化的/高性能的应用或服务集合，可将标准 linux 系统转换为基于区域的下一代防火墙。

所有的软件都被设计成彼此协同运行，但是通过模块化设计，某些方面可以不费吹灰之力就完全去除。主安全模块对通过系统的所有连接、流、消息具有直接/内嵌控制。

也就是说，根据协议，卸载到较低级别的控制是为了在启用全面检查的情况下保持最高的吞吐量。

有一个 IPTable 自定义链，允许管理员连接到数据包流，而不会意外覆盖 dnx 安全模块。我们将制作一个低级的“架构、系统设计”视频，展示如何用纯 python 实现这一点。

**包含的特性**

*   **DNS 代理**
    *   基于类别的阻止(常规、TLD、子串匹配)
    *   用户添加的白名单/黑名单或自定义常规类别创建
    *   带可选 UDP 回退的 TLS 本地 DNS 转换
    *   本地 dns 服务器
    *   软件故障转移
    *   2 级记录缓存
*   **IP 代理(透明)双向**
    *   基于重复的主机过滤
    *   地理定位过滤器
    *   局域网限制(禁止未列入白名单的所有 IP 访问局域网)
*   **IPS/IDS(广域网/入站)**
    *   拒绝服务检测/预防
    *   端口扫描检测/预防
*   **轻量级 DHCP 服务器(定制)**
    *   ip 保留
    *   安全警报集成
*   **总务**
    *   日志处理
    *   数据库管理
    *   Syslog 客户端(UDP、TCP、TLS)重要提示:目前处于测试/不稳定状态。默认情况下不会启用该服务，并且需要在系统启动时启用该服务。
*   **附加功能**
    *   IPv6 已禁用
    *   预构建的 iptable 规则
    *   HTTPs 上的 dns 阻止(DNS 绕过防护)
    *   TCP 块上的 dns(防止 DNS 绕过)
    *   TLS 块上的 dns(防止 DNS 绕过)
    *   默认情况下，到 wan 的所有入站连接都会断开
    *   IPTABLES 定制链，用于管理挂钩到数据包流

**运行前**

**新增:** sqlite3 现在是使用中的默认数据库(为了简化部署)。位于 dnx_configure/dnx_constants.py 中的环境变量“SQL_VERSION”可以翻转以使用 postgresql。警告:在初始配置后切换使用的数据库可能会导致问题。

*   [+]编辑 data/config.json 和 data/dhcp_server.json 以反映您的系统[接口]。
*   [+]将所有 systemd 服务文件移动到 systems systemd 文件夹中。
*   [+]配置系统界面。LAN 需要成为本地网络的默认网关。
*   [+]为您当前的架构/发行版编译 python-netfilterqueue(下面的链接)。`- ensure name is netfilter.so and placed in the dnxfirewall/netfilter folder`
    *   注意:在将来，这一步将被打包到部署脚本中
*   [+]为您当前的架构/发行版编译 dnx_iptools/binary_search.pyx。`- ensure name is binary_search.so and placed in the dnxfirewall/dnx_iptools folder`
    *   注意:在将来，这一步将被打包到部署脚本中
*   [+]按顺序运行/遵循[所选数据库]的相应部署脚本，以自动化系统设置。查看脚本文件中的注释以获得更多指导。

**非 DNX 代码依赖/来源！**

*   [https://github.com/kti/python-netfilterqueue](https://github.com/kti/python-netfilterqueue)| cy thon<->用于绑定 linux 内核的 python 扩展【netfilter】|这太棒了！
*   [https://www.ip2location.com/free/visitor-blocker](https://www.ip2location.com/free/visitor-blocker)|地理定位 ip 过滤数据集
*   [https://gitlab.com/ZeroDot1/CoinBlockerLists](https://gitlab.com/ZeroDot1/CoinBlockerLists)|隐密者主机设置
*   [https://squidblacklist.org](https://squidblacklist.org)|恶意和广告主机集
*   可选:[https://github.com/tlocke/pg8000](https://github.com/tlocke/pg8000)|纯 python postgresql 适配器

**通用展示演示(已过时)**

这个视频已经非常过时了，但是仍然展示了一般的功能和一些高级别的安全实现。我们将很快制作一个更新视频，展示新添加的模块:syslog 客户端、标准日志、ips/ids、更新的 dns 代理功能、更新的 ip 代理功能等等。

[**Download**](https://github.com/DOWRIGHTTV/dnxfirewall)