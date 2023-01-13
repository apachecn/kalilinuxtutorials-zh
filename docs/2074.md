# Kali Linux 2021.3 为 NetHunter 智能手表发布，并带有新的黑客工具

> 原文：<https://kalilinuxtutorials.com/kali-linux-2021-3/>

[![Kali Linux 2021.3](img/16deabb62fe3f0ccb79a1ea424975492.png "Kali Linux 2021.3")](https://1.bp.blogspot.com/-ajaSweEYMn4/YUGvgSQp-GI/AAAAAAAAOyo/ZbLeanPpKOIGdEoxzj3kkHuxBlOkmZHOQCLcBGAsYHQ/s16000/Kali%2BLinux%2B2021.3%2BReleased.png)

最受欢迎的渗透测试发行版 Kali linux 宣布了一个新版本，其中包括对 OpenSSL 的扩展支持、新工具、Live VM 支持和对智能手表的支持。

Kali Linux 2021.3 是今年的第三个版本，现在可以随时下载或用户可以更新到最新版本。

## 【Kali Linux 2021.3 的新特性

#### **默认情况下 OpenSSL**

从 Kali Linux 2021.3 开始，默认情况下启用对传统协议和密码的支持。这将有助于研究人员测试仍在使用旧协议的旧机器。

完整的 OpenSSL 配置可以在[这里](https://www.kali.org/docs/general-use/openssl-configuration/)找到。

#### **新的卡莉工具**

工具页面已经用新的设计刷新，帮助用户选择工具并做出贡献。“我们已经刷新了以前网站的每个方面，给出了一个新的，更快的，布局，内容和系统！”

以下是引入的新工具:

*   [Berate _ AP](https://pkg.kali.org/pkg/berate-ap)–协调管理流氓 Wi-Fi 接入点
*   [CALDERA](https://pkg.kali.org/pkg/caldera)–可扩展的自动化对手仿真平台
*   [EAP hammer](https://pkg.kali.org/pkg/eaphammer)–针对 WPA2 企业 Wi-Fi 网络的定向邪恶双胞胎攻击
*   host hunter–使用 OSINT 技术发现主机名的侦查工具
*   [RouterKeygenPC](https://pkg.kali.org/pkg/routerkeygenpc)–生成默认 WPA/WEP Wi-Fi 密钥
*   [Subjack](https://pkg.kali.org/pkg/subjack)–子域接管
*   [WPA _ 阿谀奉承者](https://pkg.kali.org/pkg/wpa-sycophant)–EAP 中继攻击的邪恶客户端部分

#### **虚拟化和桌面**

新版本简化了 Hyper-V 增强会话模式，只需按下回车键即可启用。

**以下是桌面的改进**

*   改进了 Xfce 通知和注销对话框的 GTK3 主题
*   重新设计的 GTK2 主题更适合旧的程序
*   改进了 Kali-Dark 和 Kali-Light 语法——突出 GNOME 和 Xfce 的主题

![](img/e5e193de336e0b2b139140daeb7b2737.png)

#### **卡利网猎人**

Kali linux 第一次被引入智能手表 TicHunter Pro，它仍处于实验阶段，现在有许多限制，希望在未来它会很有前途。

![](img/9b4e8a47f35e66ec3342732f1b00a07b.png)

你可以在这里找到如何安装它的文档。

Kali Linux 2021.3 可以从[这里](https://www.kali.org/get-kali/)下载，你也可以使用以下命令更新。

```
┌──(kali㉿kali)-[~]
└─$ echo "deb http://http.kali.org/kali kali-rolling main non-free contrib" | sudo tee /etc/apt/sources.list
┌──(kali㉿kali)-[~]
└─$ sudo apt update && sudo apt -y full-upgrade
┌──(kali㉿kali)-[~]
└─$ [ -f /var/run/reboot-required ] && sudo reboot -f
```

**查看更新**

```
┌──(kali㉿kali)-[~] 
└─$ grep VERSION /etc/os-release VERSION="2021.3" VERSION_ID="2021.3" VERSION_CODENAME="kali-rolling"
```

攻击性安全团队正计划通过改变结构来更新 kali 菜单，并改变处理操作系统映像的负载平衡器。