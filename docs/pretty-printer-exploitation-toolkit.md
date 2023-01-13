# 漂亮:“打印机开发工具包”局域网自动化工具

> 原文：<https://kalilinuxtutorials.com/pretty-printer-exploitation-toolkit/>

当网络上有大量打印机时，PRETty 非常有用。它不会对每台打印机进行扫描、记录和手动运行 PRET，而是会针对目标网络上的所有打印机自动发现和运行所选的 PRET 有效负载。

此外，它还可以用来自动向任何给定的打印机列表发送命令/有效负载。

另请参阅: [Kube-Hunter:寻找 Kubernetes 集群中的安全弱点](https://kalilinuxtutorials.com/kube-hunter-security-weaknesses/)

**安装**

安装 [PRET](https://github.com/RUB-NDS/PRET) 和所有必需的依赖项

sudo pip install-U arg parse term color
sudo apt-y install ARP-scan t shark

导航到您安装 [PRET](https://github.com/RUB-NDS/PRET) 的位置:

cd PRET

将其安装到 [PRET](https://github.com/RUB-NDS/PRET) 中:

git 克隆 https://github.com/BusesCanFly/PRETty

导航到它

**cd 蛮**

使其可执行

**chmod +x PRETty.py**

*   一行变量(来自 [PRET](https://github.com/RUB-NDS/PRET) 文件夹):

**sudo apt-y install ARP-scan t shark
sudo pip install-U arg parse term color
git 克隆 https://github.com/BusesCanFly/PRETty
CD PRETty&&chmod+x PRETty . py**

*   单线变型 w/ [PRET](https://github.com/RUB-NDS/PRET) 安装:

**sudo apt-y install imagemagick ghostscript 扫描 tshark
sudo pip install-u argar term color pysnmp
git clone https://github . com/rub-NDS/pret
pret CD
git clone https://github . com/busescanfigy/PRETty
光盘【pretty】**

**列出了**

*   它自动扫描局域网中的 HP/Brother/Kyocera 打印机，并为自己创建一个 IP 列表
    *   但是，您可以在`**PRETty/IP/**`中放置自定义 IP 列表
*   它带有位于`**PRETty/commands/**`的 PRET 的预制命令列表文件
    *   但是，您可以在`**PRETty/commands/**`中放置额外的命令列表文件

**用法**

*   用`**./PRETty.py**`运行它，并按照提示进行操作😀
*   对于更高级的用户，运行`**./PRETty.py -h**`
    *   启用 CLI 模式。(不需要用户输入)
    *   默认的`**./PRETty.py --cli**`将扫描当前局域网，并在找到的每台打印机上运行`**./commands/pret_pagecount.txt**`
    *   (可选)附加参数有:`**-r [IP range to scan] -c [Name of command list file to use] -s [PRET shell type]**`

[**Download**](https://github.com/BusesCanFly/PRETty)