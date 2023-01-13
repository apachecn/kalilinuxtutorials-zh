# DarkSpiritz:用于 Linux、MacOS 和 Windows 系统的渗透测试框架

> 原文：<https://kalilinuxtutorials.com/darkspiritz-penetration-testing-2/>

DarkSpiritz 是一个针对 Linux 和 Windows 系统的渗透测试框架。它由 SynTel 团队创建，是一个所有者的项目，旨在更新和清理他创建的旧 pentesting 框架，使其更新和现代化。

它是非常流行的框架“Roxysploit”的翻版。你可能熟悉这个框架，如果你是，那么它会帮助你。它也像另一个 pentesting 框架 Metasploit 一样工作。

如果您知道如何使用 metasploit，那么设置和使用它将是轻而易举的事情。

**也可理解为 [劫持者:黑客系统与自动化的劫持者攻击](https://kalilinuxtutorials.com/pastejacker-hacking-systems-pastejacking/)**

## **黑暗精灵入门**

用 git 克隆存储库:

```
git clone https://github.com/DarkSpiritz/DarkSpiritz.git
```

要安装 DarkSpiritz，请克隆 github repo 并运行:

```
pip install -r requirements.txt
```

这将下载所有必要的模块。运行此程序后，您将能够运行:

```
python start.py
```

或者

```
./start.py
```

(如 **。/start.py** 不工作从与 DarkSpiritz 相同的目录下运行`**chmod +x start.py**`。)

您将看到一个启动屏幕。该屏幕将显示命令和配置设置等内容。您可以在 config.xml 文件中设置配置设置，也可以通过 DarkSpiritz shell 中的命令来设置。

## **特性:**

这些是团队基于该计划引以为豪的功能:

*   配置的实时更新
*   即使添加插件或编辑插件，也不需要重启程序。
*   易于使用的 UX
*   多功能性

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/DarkSpiritz/DarkSpiritz) 信用:瑞恩& M4cs