# BruteX 自动强力攻击目标上运行的所有服务

> 原文：<https://kalilinuxtutorials.com/brutex-automatically-brute-force/>

BruteX 是一个自动暴力破解目标上运行的所有服务的工具。

众所周知，暴力攻击包括攻击者提交许多密码或口令短语，希望最终能猜对。攻击者系统地检查所有可能的口令和密码短语，直到找到正确的为止

它包括 Nmap、Hydra 和 DNS enum 等服务。其中 Nmap scan for 打开端口并定义在目标服务器上运行的服务。

此后，使用 Hydra 启动 Bruteforce FTP、SSH 和其他服务，等等。因此，您可以自动暴力破解目标服务器上运行的所有服务:

*   开放端口
*   用户名
*   密码

因此，让我们看看如何安装自动暴力所有服务工具；

**git 克隆 https://github . com/1n 3/bruex . git
原始 CD
chmod+x install . sh
。/install.sh**

一旦您成功安装了该工具，运行下面的命令，看看它是如何工作的开放端口。

布鲁特斯目标

如果您正在寻找暴力多台主机，您可以只使用 brutex-massscan 和包括 IP 的/主机名扫描在目标文件或服务器。

**也可阅读:**[az tarna——机器人的足迹工具](https://kalilinuxtutorials.com/aztarna-footprinting-robots/)

#### **视频教程**

https://www.youtube.com/watch?v=7QCBh9Enl2M

#### **免责声明**

这是一个分发、修改和使用的自由软件，条件是向创作者(1N3@CrowdShield)提供信用，并且不用于商业用途。

[**Download**](https://github.com/1N3/BruteX)