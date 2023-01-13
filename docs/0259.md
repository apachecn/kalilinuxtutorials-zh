# dro zer v 2 . 4 . 4–领先的 Android 安全评估框架

> 原文：<https://kalilinuxtutorials.com/drozer-2-4-4-android/>

Drozer 2.4.4 是领先的 Android 安全测试框架。Drozer 允许您通过扮演应用程序的角色并与 Dalvik VM、其他应用程序的 IPC 端点和底层操作系统进行交互，来搜索应用程序和设备中的安全漏洞。

Drozer 提供工具来帮助您使用、分享和理解公开的 Android 漏洞。它帮助您通过利用或社会工程将 drozer 代理部署到设备。使用 weasel (MWR 的高级开发有效载荷)drozer 能够通过安装一个完整的代理，将一个有限的代理注入一个正在运行的进程，或连接一个反向外壳作为远程访问工具(RAT)来最大化可用的权限。

## **安装 Drozer 2 . 4 . 4**

### **建造巨蟒轮**

```
git clone https://github.com/mwrlabs/drozer/
cd drozer
python setup.py bdist_wheel
```

### **安装巨蟒轮**

```
sudo pip install drozer-2.x.x-py2-none-any.whl
```

### **为 Debian/Ubuntu/Mint 搭建**

```
git clone https://github.com/mwrlabs/drozer/
cd drozer
make deb
```

### 正在安装。deb (Debian/Ubuntu/Mint)

```
sudo dpkg -i drozer-2.x.x.deb
```

### **red hat/Fedora/CentOS 的建筑**

```
git clone https://github.com/mwrlabs/drozer/
cd drozer
make rpm
```

### 正在安装。rpm(红帽/Fedora/CentOS)

```
sudo rpm -I drozer-2.x.x-1.noarch.rpm
```

### **窗户建筑**

**注意:** Windows Defender 和其他反病毒软件会将 drozer 标记为恶意软件(一个没有漏洞利用代码的漏洞利用工具不会很好玩！).为了运行 drozer，您必须为 Windows Defender 和任何防病毒软件添加一个例外。或者，我们建议在 Windows/Linux 虚拟机中运行 drozer。

```
git clone https://github.com/mwrlabs/drozer/
cd drozer
python.exe setup.py bdist_msi
```

### 正在安装。微星(Windows)

```
Run dist/drozer-2.x.x.win-x.msi
```

### **Arch Linux**

**`yaourt -S drozer`**

**亦读 [利用 CVE-2017-6079-在 Edgewater Edgemarc 设备中盲目命令注入利用](https://kalilinuxtutorials.com/exploit-injection-edgewater-edgemarc/)**

## **Drozer 2.4.4 用法**

### **安装代理**

Drozer 可以使用 Android 调试桥(adb)安装。

在这里下载最新的 Drozer 代理[。](https://github.com/mwrlabs/drozer/releases/download/2.3.4/drozer-agent-2.3.4.apk)

**`$ adb install drozer-agent-2.x.x.apk`**

### **开始会话**

现在，您应该已经在 PC 上安装了 drozer 控制台，并且代理正在测试设备上运行。现在，您需要将两者联系起来，并准备开始探索。

我们将使用嵌入在 drozer 代理中的服务器来完成这项工作。

如果使用 Android 模拟器，您需要设置一个合适的端口转发，以便您的 PC 可以连接到模拟器内部或设备上的代理打开的 TCP 套接字。默认情况下，drozer 使用端口 31415:

`**$ adb forward tcp:31415 tcp:31415**`

现在，启动代理，选择“嵌入式服务器”选项并点击“启用”来启动服务器。您应该会看到服务器已经启动的通知。

然后，在您的 PC 上，使用 drozer 控制台进行连接:

**在 Linux 上:**

**`$ drozer console connect`**

**在 Windows 上:**

**`> drozer.bat console connect`**

如果使用真实设备，必须指定设备在网络上的 IP 地址:

**在 Linux 上:**

`**$ drozer console connect --server 192.168.0.10**`

**在 Windows 上:**

**`> drozer.bat console connect --server 192.168.0.10`**

您应该会看到一个 drozer 命令提示符:

```
selecting f75640f67144d9a3 (unknown sdk 4.1.1)  
dz>
```

提示确认您已连接的设备的 Android ID，以及制造商、型号和 Android 软件版本。

您现在可以开始探索设备了。

### **命令参考**

| 命令 | 描述 |
| --- | :-- |
| 奔跑 | 执行 drozer 模块 |
| 目录 | 显示可以在当前会话中执行的所有 drozer 模块的列表。这将隐藏您没有适当权限运行的模块。 |
| 壳 | 在代理进程的上下文中，在设备上启动一个交互式 Linux shell。 |
| 激光唱片 | 挂载一个特定的命名空间作为会话的根，以避免重复键入模块的全名。 |
| 干净的 | 删除 drozer 存储在 Android 设备上的临时文件。 |
| 贡献者 | 显示对您系统上使用的 drozer 框架和模块做出贡献的人员列表。 |
| 回声 | 将文本打印到控制台。 |
| 出口 | 终止 drozer 会话。 |
| 帮助 | 显示关于特定命令或模块的帮助。 |
| 负荷 | 加载一个包含 drozer 命令的文件，并按顺序执行它们。 |
| 组件 | 从互联网上查找并安装附加的 drozer 模块。 |
| 许可 | 显示授予 drozer 代理的权限列表。 |
| 设置 | 将一个值存储在一个变量中，该变量将作为环境变量传递给由 drozer 生成的任何 Linux shells。 |
| 复原 | 删除 drozer 传递给它生成的任何 Linux shells 的命名变量。 |

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/mwrlabs/drozer)