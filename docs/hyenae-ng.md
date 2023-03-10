# Hyenae Ng:一个先进的跨平台网络包生成器，是 Hyenae 的继承者

> 原文：<https://kalilinuxtutorials.com/hyenae-ng/>

[![](img/880669a6bd2e03b7f138032559feb40f.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg_xWfeU_v9zSIPMlJb4y11TqrWvYoYckpjHjk7kez__39QiyEF8kfu6-5Mdp_Y_HLa1WoThHel3rgX6-OTdi1_K_kSl-K4_deCHZP5bcfVFUGuEVmN193w20HUxHg16bFzoCvtgMo1ovky6RMetSD8dwJD-apAlTQ6w2EBqOqbpGum-0O4lkPfALxa=s760)

鬣狗 Ng(下一代)是对 2010 年发布的原始鬣狗工具的重写。

除了从 C 转换到 C++，使用现代的设计概念，Hyenae NG(就像最初的 Hyenae 一样)的编写考虑到了最大的可移植性。由于最初的鬣狗有一个非常复杂的命令行语法，鬣狗 NG 提供了一个快速和直观可用的命令行菜单，允许您在几秒钟内有效地设置甚至复杂的压力测试或攻击场景。

**特性**

*   完全可定制和可组合的数据生成器:
    *   以太网层
    *   空气播放器
    *   IPv4 层
    *   IPv6 层
    *   ICMPv4 层
    *   icmp V6-层
    *   ttplayer
    *   UDP 层
    *   文本缓冲区
*   固定或随机发送延迟
*   基于模式的地址随机化
*   干净和易于使用的命令行菜单(不需要 RTFM 'ing))
*   独立于平台

**覆盖范围**

*   ARP-请求泛洪(DoS)
*   ARP 缓存中毒(MITM)
*   ICMP-回声泛洪(DoS)
*   ICMP-Smurf 攻击(DoS)
*   TCP-SYN 泛洪(DoS)
*   TCP-陆地攻击(DoS)
*   盲目 TCP 连接重置(DoS)
*   UDP 泛洪(DoS)
*   还有更多…

**项目目标**

最初的 Hyenae 项目是从研究网络堆栈实现开始的，但很快就获得了更复杂的功能，如远程守护程序和攻击助手。即使它被广泛接受并且仍然是当今笔测试工作流程中非常常用的工具，它也有复杂的命令行语法，需要一些培训和研究才能正确使用。

对于 Hyenae NG，我想用一个简洁易用的命令行工具来提供 hyenea 的复杂性和灵活性，这种工具可以立即使用，而无需进一步研究命令行参数来传递特定的场景。

**基本用法**

一旦你启动鬣狗 NG，它将进入主菜单状态。从这里，您可以设置您想要的输出，发电机和调度配置。

*   **输出设置**
    输出设置让你从几个不同的输出选项中选择。你可以选择“不输出”来忽略 Hyenae NG 的输出，或者将它发送到文件或网络适配器。一旦选择了一个输出，您可以通过再次输入它的菜单项编号或简单地按 enter 键再次选择它，从而进入它的子设置。一旦选择了具有子设置的输出，就会用一个(…)进行标记。
*   **发电机设置**
    发电机设置让你从几个不同的发电机中选择。大多数发生器都提供了一个有效负载选项，您可以选择另一个发生器，依此类推。由于网络帧生成器嵌套在传输层中，因此其可用的有效负载生成器将根据之前选择的帧生成器而有所不同。以下是以太网数据包的典型有效载荷嵌套示例:

**以太网+->ARP
|
+->IP v4+->ICMP v4->ICMP Echo 有效载荷
|+->TCP
|+->UDP
|+->…
|
+->IPv6+->ICMP v4->ICMP Echo 有效载荷
+->ICMP V6->**

*   **调度员设置**
    调度员设置会让你设置实际的数据调度员。您可以定义停止限制或配置固定或随机的发送延迟，以打破目标系统上的泛洪检测机制。**重要提示**
    建议在 GPD Pocket 2 等低规格系统上使用至少 100 毫秒的固定发送延迟，以防止按键检测问题。
*   **启动调度器**
    一旦你设置了一个发生器，你可以选择这个选项来启动调度器并开始发送数据包。如果您还没有设置生成器，将会显示一条错误消息。调度程序将一直运行，直到达到停止限制(如果设置)或用户按下任何键。dispatcher 停止后，您可以通过输入 0 返回主菜单，或者通过输入 1 或简单地按 enter 键再次启动它。

**发电机模式**

许多分组生成器参数，例如地址、端口和号码字段，可以与生成器模式一起提供。这些模式将被用于在每个新分组上生成新值。下面是一些基本模式的例子:

*   随机 5 位数:`*********`
*   增量 3 位数:`**+++**`
*   递减的两位数:`**--**`
*   `**100**`和`**190**`之间的随机数:`**1*0**`
*   从`**1**`到`**991**`的递增数:`**++1**`
*   从`**299**`到`**200**`的递减数:`**2--**`
*   `**.200**`和`**.255**`之间的随机 IPv4 地址:`**129.168.0.2****`
*   `**:00**`和`**:FF**`之间的增量 MAC 地址:`**AA:BB:CC:DD:EE:++**`
*   在`**:FFFF**`和 **`:FF00`之间递减 IPv6 地址:`1000:2000:3000:4000:5000:6000:7000:FF--`**

**配置文件**

当 Hyenae NG 启动时，它会在启动文件夹中查找名为“hyenae.conf”的配置文件。如果该文件不存在，它将自动创建它。

**重要提示**
如果配置文件无法解析，鬣狗 NG 会给出一条错误信息，要求您修复或删除配置文件。

*   **前端部分**
    *   **terminal_colors**
        如果设置为“开”(默认)，鬣狗将使用 ANSI 终端颜色以增强它的用户界面。如果由于某些原因，您使用的终端不支持 ANSI 颜色，您应该将其设置为“关”。
    *   **line_chars**
        如果设置为“开”(默认)，鬣狗将使用特殊的行字符作为它的菜单分隔符(在基于 Windows 的 ASCII 和基于*nix 的 UniCode 系统中)。如果您遇到任何奇怪的分隔符输出，您应该将其设置为“关”。

[**Download**](https://github.com/r-richter/hyenae-ng)