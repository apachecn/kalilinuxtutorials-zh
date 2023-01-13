# nmapAutomator:可以在后台运行的脚本

> 原文：<https://kalilinuxtutorials.com/nmapautomator/>

[![nmapAutomator : A Script That You Can Run In The Background](img/ae36ff27c08cb34ea3a438e9d8d713f1.png "nmapAutomator : A Script That You Can Run In The Background")](https://1.bp.blogspot.com/-et3iIDeL16w/XgXnhdcSk9I/AAAAAAAAEMI/2InfosJFZTw_XOzKgAr-KjB63J3kAi-VACLcBGAsYHQ/s1600/nmap.png)

nmapAutomator 是一个可以在后台运行的脚本。这个脚本的主要目标是自动化每次运行的所有 recon/enumeration 过程，而不是将我们的注意力集中在真正的笔测试上。

这将确保两件事:

*   自动执行 nmap 扫描。
*   总是有一些侦察在后台运行。

一旦您在大约 10 秒钟内找到初始端口，您就可以开始手动查看这些端口，让其余的端口在后台运行，而无需您的任何交互。

**特性**

*   **快速:**快速显示所有打开的端口(约 15 秒)
*   **基本:**运行快速扫描，然后 a 对找到的端口运行更彻底的扫描(大约 5 分钟)
*   **UDP:** 在 UDP 端口上运行“基本”程序(大约 5 分钟)
*   **完全:**运行全范围端口扫描，然后对新端口运行全面扫描(大约 5-10 分钟)
*   **漏洞:**在所有找到的端口上运行 CVE 扫描和 nmap 漏洞扫描(大约 5-15 分钟)
*   **Recon:** 运行“基本”扫描“如果尚未运行”，然后根据找到的端口建议 Recon 命令“即 gobuster、nikto、smbmap”，然后提示自动运行它们
*   **All:** 连续运行所有扫描(大约 20-30 分钟)

我试图让脚本尽可能高效，这样你就能尽快得到结果，而不需要重复任何工作。

**要求**

**必需:** Gobuster v3.0 或更高版本，因为它不向后兼容。
您可以使用以下命令在 kali 上更新 gobuster:

**apt-get 更新
apt-get 安装 gobuster-only-升级**

**使用示例**

**。/nmpaumatoror . sh
。/nmpaumatoror . sh 10 . 1 . 1 all
。/nmpaumatoror . sh 10 . 1 . 1 基本
。/nmpaumatoror . sh 10 . 1 . 1 recon**

如果您想在系统的任何地方使用它，请使用以下命令创建一个快捷方式:

**ln-s/PATH-TO-FOLDER/nmapautomator . sh/usr/local/bin/**

[**Download**](https://github.com/21y4d/nmapAutomator)