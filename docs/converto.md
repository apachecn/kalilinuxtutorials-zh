# Converto:在 VPS 服务器上安装 Kali Linux

> 原文：<https://kalilinuxtutorials.com/converto/>

[![Converto : Installing Kali Linux on VPS Server](img/fdf649632af851d9880fdac2f1e38614.png "Converto : Installing Kali Linux on VPS Server")](https://3.bp.blogspot.com/-ZCBkipi4GOY/XOb3JYsD4cI/AAAAAAAAAfs/kCT96ZKaSTUSseA2oVZtEu8d_If94TGIQCLcBGAs/s1600/Converto-1%25281%2529.png)

Converto 是一个用于 VPS 的自动化 Kali Linux 或 Parrot OS 安装程序，也安装 VNC(图形/非图形 VNC)。它在以下方面进行测试:

*   在 Ubuntu 上测试
*   在 Debian 上测试

**安装**

**sudo apt-get 更新
sudo apt-get 安装 git
git 克隆 https://github.com/developerkunal/Converto.git
CD Converto。
chmod +x converto.sh
。/converto.sh**

**也可阅读-[XSS con:简单的 XSS 扫描仪工具](https://kalilinuxtutorials.com/xsscon/)**

![](img/cf1683d94c66e1b470508a79c3631979.png)

*   安装类型 1

类型 2 为退出
类型备注为阅读备注(推荐)

![](img/a170033eb341765b5bca143a1ba8bf24.png)

*   按 1 并输入

![](img/d056bd4af683a8ae23937f5d54474836.png)

*   现在选择所需的选项。

![](img/a2babe1fc1be5f9e1ce385109f6bb1d8.png)

*   我为 Parrot OS 选择 2。

![](img/5197fc6a58a5a5ff944df32fad452d49.png)

*   现在选择所需的选项。

1.  仅安装核心
2.  安装 Headless 版本
3.  安装标准版
4.  安装完整版
5.  安装家庭版
6.  安装嵌入式版本

*   选择 4 进行完全安装

![](img/5ace578384ddfa18e4b22b50e54b5941.png)

*   选择是。(必要的)

![](img/c87da5efb490405cf509fc37e5d86381.png)

*   选择是。(必要的)

![](img/03ce9496f255998c8cd0e90cee3f32cb.png)

*   键入 Y，然后按 Enter 键。(必要的)

![](img/5d6753f56f36ef37baea3e81deda1618.png)

*   键入 Y，然后按 Enter 键。(必要的)

![](img/9b8eef0aa213d16b5d4b708814c12be8.png)

*   选择安装软件包维护者的版本。

![](img/56e893ad323f3dbaf00559ce043576a9.png)

**安装完成**

![](img/44d4f9e569d70cb5a4d7d74a8386777e.png)

**安装 VNC 的可选步骤**

![](img/1163a6534875c75617d7080c4790a911.png)

**步骤**

*   选择您想要安装的 VNC 类型(建议使用图形化 VNC)

![](img/38e4ee2576ef4817f6a96cf088dcf277.png)

*   现在输入 VNC 连接的密码，并再次输入密码进行验证。

![](img/4cca572a3964359394a193ef4bcb5d7f.png)

*   可选:如果您想要仅查看密码，请按 Y 键(在仅查看密码中，拥有该密码的用户只有查看屏幕的权限。)

**启动和停止 VNC 服务器的命令**

**启动 VNC 服务器**

**root@kali:~# vncserver
(它总是在端口 1 上启动)**

**停止一个 VNC 服务器**

**root @ kali:~ # vncserver-kill:1
VNC 查看器中的示例 IP:127 . 0 . 0 . 1:1**

**演职员表:**库纳尔·达瓦尔&阿尤什·萨海

[**Download**](https://github.com/developerkunal/Converto#steps--)