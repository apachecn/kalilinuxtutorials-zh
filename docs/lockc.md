# Lockc:用 eBPF 和 Linux 安全模块使容器更安全(LSM)

> 原文：<https://kalilinuxtutorials.com/lockc/>

[![](img/e7acba29e8c9f6067af150dac18fbe4f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiE1uVGAlJj9JfcUzlljge0YxR6ddPgnGQo-z0Ds1dV_3Pml9cIi8YslK930s_rT6eRmpDbnb19HC2Ur-3ud395T1IuSZAArTkxUSvVIWNWLLEOXaEhUjpAfIXPbWLHXkR9JNtQSHOeIykIRgEJSFhBawkhJn505GnbScnmC71qOJE-n-nDGaNwb8gp/s1058/logo-horizontal-lockc%20(1).png)

lockc 是一款开源软件，用于为容器工作负载提供 MAC(强制访问控制)类型的安全审计。

**lockc** 存在的主要原因是**集装箱不包含**。容器不像虚拟机那样安全和孤立。默认情况下，它们公开了大量关于主机操作系统的信息，并提供了从容器中“突破”的方法。 **lockc** 旨在为集装箱提供更多的隔离，使其更加安全。

“容器不包含文档”一节解释了这个短语的含义，以及我们希望用 **lockc** 限制哪种行为。

lockc 背后的主要技术是 eBPF——更准确地说，是它与 LSM 挂钩的能力

请注意，目前 lockc 是一个实验项目，并不意味着生产环境，也没有任何正式的二进制文件或软件包可以使用-目前唯一的使用方法是从源代码构建。

请点击此处查看完整文档。和代码文档。

如果你需要帮助或想与贡献者交谈，请在 Rust Cloud Native Discord 服务器上的`**#lockc**`频道与我们聊天。

**lockc 的**用户空间部分在 Apache 许可证 2.0 版下获得许可。

lockc/src/bpf 目录中的 eBPF 程序是根据 GNU 通用公共许可证第 2 版许可的。

[**Download**](https://github.com/lockc-project/lockc)