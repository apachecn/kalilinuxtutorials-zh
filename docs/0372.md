# conpot–ICS/SCADA 蜜罐

> 原文：<https://kalilinuxtutorials.com/conpot-ics-scada-honeypot/>

Conpot 是一个 ICS 蜜罐，目标是收集有关针对工业控制系统的对手的动机和方法的情报。

**也读作:**[BruteX——自动强力攻击目标上运行的所有服务](https://kalilinuxtutorials.com/brutex-automatically-brute-force/)

#### **安装 Ubuntu**

你需要在源中加入多元宇宙，比如；

**$ sudo vim/etc/apt/sources . list**

添加以下一行:

**黛比·http://dk.archive.ubuntu.com/ubuntu 精确的主多元宇宙**

安装依赖项:

**sudo apt-get install libmysql client-dev libsmi 2 ldbl SNMP-MIBs-downloader python-dev libevent-dev \
libxslt 1-dev libxml 2-dev python-pip python-mysqldb pkg-config lib virt-dev**

它的稳定版本可以从 PyPI 下载:

**pip 安装罐**

开发版本可以从 github 克隆:

**CD/opt
git clone git @ github . com:mush org/conpot . git
CD conpot
python setup . py install**

#### **使用 Docker 轻松安装**

**通过预先构建的图像**

**安装 Docker
运行 docker pull 蜜网/conpot
运行 Docker Run-it-p 80:80-p 102:102-p 502:502-p 161:161/UDP–network = bridge 蜜网/conpot:latest /bin/sh
最后运行 conpot-f–模板默认**

导航到 http://MY_IP_ADDRESS 以确认设置。

**从源构建 docker 映像**

**安装坞站
用 git 克隆 https://github . com/mush org/conpot . git 和 cd conpot/docker
运行坞站构建-t conpot。
运行码头运行-it-p80:8800-p102:1021-p002:5020-p161:16100/UDP-p47808:47808/UDP-p623:6230/UDP-p21:2121-p69:6969/UDP-p448:4488–network = bridge conpot**

导航到 http://MY_IP_ADDRESS 以确认设置。

**从源代码构建并运行 docker-compose**

**安装 docker-compose
用 git 克隆 https://github.com/mushorg/conpot.git 和 cd conpot/docker 克隆这个 repo】用 docker-compose 构建映像
用 docker-compose up 测试一切是否正常运行
用 docker-compose up -d 作为守护进程永久运行**

[**Download**](https://github.com/mushorg/conpot)