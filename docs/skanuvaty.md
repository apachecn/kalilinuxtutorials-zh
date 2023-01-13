# Skanuvaty:危险的快速 DNS/网络/端口扫描器

> 原文：<https://kalilinuxtutorials.com/skanuvaty/>

[![](img/556a92ec3865d57f3a2ab63daaaee83a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiFsqgpoYGBAfgARFhkVdtE3pnwtR1prNLNqwQ9ySKxnfUgERsI9NRPpwk7HzIoAZ3XkXpKp_Wc1qidUMC_Xbw3hdgXBbp8ka9Cn_R0tGlctNs3AxnSqvFCDmhaRdr5QxeorhjlCFVuiPXEJaJy7wggmHw35EksZPJ0PY3KU8A6bN0PcrVbIKGKhwbq/s728/image_380x226_6223ff60c15c4.png)

**Skanuvaty** 是危险的快速 DNS/网络/端口扫描器，多合一。

从一个域开始，我们会找到关于它的一切。

## 特征

*   从根域中查找子域
*   查找子域的 IP
*   检查这些 IP 上打开了哪些端口(注意:尚未实现)

输出一个方便的。json 文件中的所有数据，以便进一步调查。

以您的计算机/网络/DNS 解析器允许的最快速度运行。在一台拥有 16 个(逻辑)内核的机器上，将`**concurrency**`设置为 16，在大约 20 秒内测试了 10.000 个子域。

## 用法

**skanuvaty–目标 nmap.org–并发 16–子域名-file/usr/share/dnsenum/DNS . txt**

终端将显示所有找到的子域+一个`**skanuvaty.scan.json**`文件已经在您的当前目录中创建。

[**Download**](https://github.com/Esc4iCEscEsc/skanuvaty)