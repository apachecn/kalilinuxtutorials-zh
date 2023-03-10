# 破解蓝牙智能加密

> 原文：<https://kalilinuxtutorials.com/crackle-crack-bluetooth/>

**爆裂声**破解 BLE 加密。它利用了 BLE 配对过程中的一个缺陷，该缺陷允许攻击者猜测或非常快速地暴力破解 TK(临时密钥)。利用从配对过程中收集的 TK 和其他数据，可以收集 STK(短期密钥)以及随后的 LTK(长期密钥)。

![](img/6fd823cd36fe492dcf76d7d16bcb23a6.png)

有了 STK 和 LTK，主从之间的所有通信都可以被解密。在尝试使用 crackle 之前，请查看 FAQ 以确定它是否适合您的情况。

这是由**迈克·瑞恩**写的。

## **爆裂声运行方式**

它有两种主要的操作方式:**破解 TK** 和**用 LTK** 解密。

**也读[WP crack——暴力破解的简单工具 WordPress](https://kalilinuxtutorials.com/wpcrack/)**

## **破解 TK**

这是使用`-i`向 crackle 提供输入文件时使用的默认模式。

在裂纹 TK 模式下，裂纹蛮力在 BLE 配对事件中使用的 TK。它利用了以下事实:Just Works(tm)中的 TK 和 6 位 PIN 是填充到 128 位的范围[0，999999]内的值。

crackle 使用了几种方法来执行这种强力攻击:如果所有配对包都出现在输入文件中，则使用一种非常快速的方法；如果出现了最少的一组包，则使用一种慢速方法。

要使用此模式，请使用包含一个或多个 BLE 配对对话连接的输入 PCAP 或 PcapNG 文件启动 crackle。它将分析所有连接，确定是否有可能破解给定的连接，并自动选择最佳策略来破解每一个连接。

如果 TK 成功破解，它将获得用于加密连接其余部分的剩余密钥，并将解密随后的任何加密包。如果交换了 LTK(通常是建立加密后的第一件事)，crackle 会将这个值输出到 stdout。LTK 可用于解密两个端点之间的任何未来通信。

使用`-o`为其提供一个输出文件，以创建一个包含解密数据(除了已经加密的数据之外)的新 PCAP 文件。

示例用法:

```
$ crackle -i input.pcap -o decrypted.pcap
```

## **用 LTK 解密**

在用 LTK 解密模式中，crackle 使用用户提供的 LTK 来解密主设备和从设备之间的通信。该模式与破解 TK 模式的解密部分相同。

示例用法:

```
$ crackle -i encrypted.pcap -o decrypted.pcap -l 81b06facd90fe7a6e9bbd9cee59736a7
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/mikeryan/crackle)