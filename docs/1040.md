# ReconPi:一个轻量级的侦察工具，执行广泛的扫描

> 原文：<https://kalilinuxtutorials.com/reconpi-recon-tool-performs-extensive-scanning/>

[![ReconPi : A Lightweight Recon Tool That Performs Extensive Scanning](img/d5bb5c305a4a1f70ce322a0990fab861.png "ReconPi : A Lightweight Recon Tool That Performs Extensive Scanning")](https://1.bp.blogspot.com/-4Vy9rleBCd8/Xe93iY93AqI/AAAAAAAAD4k/fLmUBdXpOCIEM-Y9bGJ6XYsge3wPsB9CwCLcBGAsYHQ/s1600/ReconPi%25281%2529.png)

ReconPi 是一个轻量级的侦察工具，使用最新的工具使用 Raspberry Pi 执行广泛的侦察。

**安装**

点击这里查看更新的博客文章，获得如何设置你自己的 ReconPi 的完整指南: [ReconPi 指南](https://x1m.nl/posts/recon-pi/)

如果你通过上面链接的指南准备了你的覆盆子酱，你应该可以继续下面的操作。

> 工具 v2.0 需要 [HypriotOS](https://blog.hypriot.com/downloads/) (V1.10.0)镜像才能 100%工作！

**易于安装**

用 SSH 连接到您的 ReconPi:

**ssh pirate@192.168.2.16【将 IP 改为 re conpi IP】**

卷曲`**install.sh**`脚本并运行它:

**curl-L https://raw . githubusercontent . com/x1 mdev/re conpi/master/install . sh | bash**

**手动安装**

用 SSH 连接到您的 ReconPi:

**$ ssh pirate@192.168.2.16【将 IP 改为 re conpi IP】**

现在我们可以设置一切，这很简单:

*   **T2`git clone https://github.com/x1mdev/ReconPi.git`**
*   **T2`cd ReconPi`**
*   **T2`./install.sh`**
*   脚本在`**install.sh**`的末尾给出了一个`**reboot**`命令，请再次登录以开始使用 ReconPi。

喝杯咖啡，因为这需要一段时间。

**亦读-[APK-MITM:安卓 APK 档案供 HTTPS 查验](https://kalilinuxtutorials.com/apk-mitm-android-apk-https-inspection/)**

**用途**

安装完 ReconPi 的所有依赖项后，你终于可以开始做一些 re coni 了！

**$ recon<domain.tld></domain.tld>**

`**recon.sh**`将首先收集给定目标的解析器，然后进行子域枚举，并检查这些资产是否可能被子域接管。完成后，枚举目标的 IP 地址。打开的端口将通过 Nmap 提供的服务扫描来发现。

最后，将对实时目标进行截屏和评估，以发现终点。

结果将存储在 Recon Pi 上，可以通过在结果目录中运行“python -m SimpleHTTPServer 1337”来查看。您的结果将可从同一网络中任何装有浏览器的系统中访问。

**工具**

此刻正在使用的工具:

*   [催眠状态](https://blog.hypriot.com/downloads/)
*   [出发](https://github.com/golang)
*   [子查找器](https://github.com/Ice3man543/subfinder)(现在运行在原生 Go 上)
*   [水叮当](https://github.com/michenriksen/aquatone)
*   [http 探测](https://github.com/tomnomnom/httprobe)
*   [资产发现者](https://github.com/tomnomnom/assetfinder)
*   [和](https://github.com/tomnomnom/meg)
*   [捉鬼敢死队](https://github.com/OJ/gobuster)
*   [积聚](https://github.com/OWASP/Amass)
*   [MassDNS](https://github.com/blechschmidt/massdns)
*   [质量扫描](https://github.com/robertdavidgraham/masscan)
*   [nmap](https://nmap.org/)
*   [CORScanner](https://github.com/chenjj/CORScanner)
*   [子租赁](https://github.com/yassineaboukir/sublert)
*   [低音](https://github.com/Abss0x7tbh/bass)
*   [LinkFinder](https://github.com/GerbenJavado/LinkFinder)

将来会添加更多工具，请随时提出拉取请求！

[**Download**](https://github.com/x1mdev/ReconPi)