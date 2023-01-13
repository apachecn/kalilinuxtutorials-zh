# pwnadventure 3–游戏容易受到黑客攻击

> 原文：<https://kalilinuxtutorials.com/pwnadventure3/>

PwnAdventure3: Pwnie Island 是一个限量发行的第一人称真实开放世界 MMORPG，设定在一个任何事情都可能发生的美丽岛屿上。那是因为这个游戏容易受到各种愚蠢黑客的攻击！飞行，无尽的现金，等等都是一个客户端的变化或网络代理。你准备好大屠杀了吗？！

官方网站[点击这里](http://www.pwnadventure.com/)

**也读作 [牛脂——透明 Tor for Windows](https://kalilinuxtutorials.com/tallow-tor-anonymity-network/)**

## **安装服务器**

### **要求**

来自官方自述:

*   至少 2GB 的内存，更多的内存将允许在一台机器上运行更多的实例
*   游戏服务器不需要任何图形硬件，完全在控制台上运行。众所周知，它在亚马逊 AWS 和数字海洋 VPS 实例上运行良好。
*   游戏服务器需要大量 RAM 来运行，但是使用 fork 和写时复制内存来允许许多实例在单个主机上运行。
*   对于 2GB 内存的服务器，建议不要运行超过 5 个实例，但是 8GB 内存的服务器通常可以运行 CPU 能够处理的所有实例。
*   如果有足够的 RAM，建议每个 CPU 内核使用 2-3 个实例。您可能能够在每个内核上运行 4-5 个实例，但是这样做可能会带来轻微的延迟。
*   客户端和服务器的文件也超过 2GB，因此需要几 GB 的可用磁盘空间。

有几种方法可以构建和部署您自己的服务器。

##### **选项 1–原**

一种选择是下载并遵循官方文件自述文件中的说明。可以在官网[这里](http://www.pwnadventure.com/#server)找到下载。

##### **选项 2–指南**

@Beaujeant 创建了一个优秀的，易于遵循的分步指南。这也是从选项 3 构建 docker 映像的基础。导游可以在这里找到[。](https://github.com/beaujeant/PwnAdventure3/blob/master/INSTALL-server.md)

##### **选项 3–码头工人**

这个选项超级简单，只要在主机上安装`**docker**`和`**docker-compose**`就可以了。它使运行和拆除服务器变得容易，而无需对实际的主机系统进行更改。

首先，收集所有必要的文件:

```
git clone https://github.com/LiveOverflow/PwnAdventure3.git
cd PwnAdventure3
wget http://pwnadventure.com/pwn3.tar.gz
tar -xvf pwn3.tar.gz
```

为了运行服务器，必须安装`docker`和`docker-compose`。Docker 发展很快，所以最好遵循当前官方的安装步骤(这也可能包括删除 docker 的旧系统版本):

*   CE Ubuntu 坞站:https://docs . docker . com/install/Linux/docker-ce/Ubuntu/。
*   `**docker-compose**`:[https://docs . docker . com/compose/install/](https://docs.docker.com/compose/install/)
*   确保当前用户是带有`**sudo usermod -a -G** **docker $USER**`的`docker`组的一部分。重启或重新登录，并通过`id`验证用户是否属于 docker 组。

然后只需构建映像并启动主服务器和游戏服务器:

```
docker-compose build
docker-compose up
```

`**docker-compose up**`也可以通过`**-d**`在分离/后台模式下运行。

## **安装客户端 pwnadventure 3**

先从官网[这里](http://www.pwnadventure.com/#downloads)下载客户端

要让客户机连接到新服务器，必须修改客户机的`**server.ini**`。用 docker 启动的服务器期望主机名`**master.pwn3**`和`**game.pwn3**`被使用(理论上这些可以在 docker/setup 文件中改变)。

客户端的`**server.ini**`应该是这样的:

```
MasterServer]
Hostname=master.pwn3
Port=3333

[GameServer]
Hostname=game.pwn3
Port=3000
Username=
Password=
Instances=
```

确保客户端可以访问这些主机，例如通过将它们添加到 **`/etc/hosts`** 文件中。在本例中，服务器运行在`**192.168.178.57**`上，它们的条目应该是:

```
192.168.178.57  master.pwn3
192.168.178.57  game.pwn3
```

**警告:**使用 IP 作为`**server.ini**`中的 `**Hostname**` 不起作用！我花了两个小时试图找出问题所在。

要停止服务器，只需输入`**docker-compose down**`。

**警告:**数据库文件不是持久的——取下容器会重置所有内容。所以先备份。

## **信用点**

真正的英雄，是游戏的开发者

Pwn Adventure 3 是 Rusty Wagner 的创意。他负责想法、计划和几乎所有的执行(编程、关卡设计、任务等等)。没有他，就没有游戏！还要特别感谢 Shellcode 组织者中的 Ghost，感谢他们在开发和测试期间的支持。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/LiveOverflow/PwnAdventure3/)