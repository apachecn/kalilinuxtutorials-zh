# 涡轮入侵者:一个发送大数字的打嗝套件扩展

> 原文：<https://kalilinuxtutorials.com/turbo-intruder/>

[![Turbo Intruder : A Burp Suite Extension For Sending Large Numbers](img/57649551bcee327cc3521b96c6701e39.png "Turbo Intruder : A Burp Suite Extension For Sending Large Numbers")](https://1.bp.blogspot.com/-qZKkOpkshlY/YFNnhOhYeII/AAAAAAAAIlQ/j_K5p2f3SWEn-r0agPZtDAa13PSqU6SfgCLcBGAsYHQ/s728/Turbo-Intruder%25281%2529.png)

**Turbo intrusor**是一个 Burp 套件扩展，用于发送大量 HTTP 请求并分析结果。它旨在通过处理需要非凡速度、持续时间或复杂性的攻击来补充 Burp 入侵者。以下特性使其与众不同:

*   **快速**–Turbo intrusor 使用一个从零开始手工编码的 HTTP 堆栈，同时考虑到速度。因此，在许多目标上，它甚至可以远远超过流行的异步 Go 脚本。
*   **可扩展**–Turbo intrusor 可以实现平坦的内存使用，支持可靠的多日攻击。它也可以通过命令行在无头环境中运行。
*   **灵活**–使用 Python 配置攻击。这使得能够处理复杂的需求，如签名请求和多步攻击序列。此外，自定义 HTTP 堆栈意味着它可以处理破坏其他库的格式错误的请求。
*   **便捷**–钻孔结果可通过先进的差分算法自动过滤，该算法由反斜杠驱动的扫描仪改编而来。这意味着您可以发起攻击，并在两次点击中获得有用的结果。

另一方面，它不可否认地更难使用，并且网络堆栈不像 core Burp 那样可靠和经得起考验。由于这是一个工具，只有高级用户，我不会提供个人支持任何人有困难使用它。我还应该提到，它是为向单个主机发送大量请求而设计的。如果你想发送一个请求给很多主机，我推荐 ZGrab。

**文档**

要开始使用 Turbo Intruder，请参考视频和文档，网址为[https://ports wigger . net/blog/Turbo-intrusor-incoming-the-billion-request-attack](https://portswigger.net/blog/turbo-intruder-embracing-the-billion-request-attack)

[**Download**](https://github.com/PortSwigger/turbo-intruder)