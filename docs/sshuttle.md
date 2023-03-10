# SShuttle:透明代理遇到 VPN 遇到 SSH 的地方

> 原文：<https://kalilinuxtutorials.com/sshuttle/>

[![SShuttle: Where Transparent Proxy Meets VPN Meets SSH](img/208f901cccd9be29452219d0f1887f6a.png "SShuttle: Where Transparent Proxy Meets VPN Meets SSH")](https://1.bp.blogspot.com/-ZbLMq20kv8c/XncDoQV3uyI/AAAAAAAAFlI/C93XYOEqq6EHgS_-p9ltfbzYLYqNkmAmgCLcBGAsYHQ/s1600/SSHuttle.png)

SShuttle 是一个透明的代理服务器，作为一个穷人的 VPN。通过 ssh 转发。不需要管理员。适用于 Linux 和 MacOS。支持 DNS 隧道。

据我所知，它是解决以下常见情况的唯一程序:

*   您的客户机(或路由器)是 Linux、FreeBSD 或 MacOS。
*   您可以通过 ssh 访问远程网络。
*   您不一定拥有远程网络的管理员权限。
*   远程网络没有 VPN，或者只有愚蠢/复杂的 VPN 协议(IPsec、PPTP 等)。或者也许你*是*管理员，你只是对 VPN 工具的糟糕状态感到沮丧。
*   您不希望为远程网络上的每个主机/端口创建一个 ssh 端口转发。
*   你讨厌 openssh 的端口转发，因为它随机缓慢和/或愚蠢。
*   您不能使用 openssh 的 PermitTunnel 功能，因为它在 openssh 服务器上默认是禁用的；此外，它确实 TCP-over-TCP，其性能[非常糟糕](https://sshuttle.readthedocs.io/en/stable/how-it-works.html)。

**也读作-[AWS gen . py:AWS S3 桶名生成器(beta v.)](https://kalilinuxtutorials.com/awsgen-py-aws-s3-bucket-name-generator-beta-v/)**

**获取**

*   Debian stretch 或更高版本:

**apt-get install sshuttle**

*   Arch Linux:

pacman-S shuttle

*   软呢帽:

**dnf 安装包**

*   NixOS:

**尼克斯-env -iA nixos.sshuttle**

*   来自 PyPI:

**sudo pip install sshuttle**

*   克隆:

git 克隆 https://github.com/sshuttle/sshuttle.git
CD shuttle
sudo。/setup.py 安装

*   FreeBSD:

**ports
CD/usr/ports/net/py-sshuttle&&make install clean
pkg
pkg install py36-sshuttle**

也可以作为非 root 用户安装到 virtualenv 中。

*   来自 PyPI:

**virtualenv-p python 3/tmp/sshuttle
。/tmp/sshuttle/bin/activate
pip install sshuttle**

*   克隆:

**virtualenv-p python 3/tmp/sshuttle
。/tmp/sshuttle/bin/activate【https://github.com/sshuttle/sshuttle.git】git 克隆
cd sshuttle
。/setup.py 安装**

*   自制:

**brew install sshuttle**

*   Nix:

**nix-env-iA nixpkgs . sshuttle**

[**Download**](https://github.com/sshuttle/sshuttle)