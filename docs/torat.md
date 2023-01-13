# ToRat:用 Go 编写的远程管理工具，使用 Tor 作为传输机制& RPC 进行通信

> 原文：<https://kalilinuxtutorials.com/torat/>

[![ToRat : A Remote Administration Tool Written In Go Using Tor As A Transport Mechanism & RPC For Communication](img/f80415e180bf691e35f811c1f699507a.png "ToRat : A Remote Administration Tool Written In Go Using Tor As A Transport Mechanism & RPC For Communication")](https://1.bp.blogspot.com/-R3761ByzQp8/X9vkHrR3ZPI/AAAAAAAAIK8/7ls746vTVaQPuiJNOis3Vhs2Nwk0j-GYACLcBGAsYHQ/s728/ToRat_1_ToRat_Logo%25281%2529.png)

ToRat 是用 Go 编写的跨平台远程管理工具，使用 Tor 作为其传输机制，目前支持 Windows、Linux、MacOS 客户端。

**如何？**

**TL；博士**

**git 克隆 https://github . com/Lu 4p/torat . git
CD。/ToRat
sudo 码头建设。-t 胸片
【sudo 坞站运行-it-v " $ pwd】/dist:/dist _ ext 胸片**

**先决条件**

*   在 Linux 上安装 Docker
    *   Ubuntu[https://docs . docker . com/install/Linux/docker-ce/Ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
    *   debian[https://docs . docker . com/install/Linux/docker-ce/debian/](https://docs.docker.com/install/linux/docker-ce/debian/)
    *   fedorahttps://docs . docker . com/install/Linux/docker-ce/fedora/
    *   centos[https://docs . docker . com/install/Linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)
    *   拱门`sudo pacman -s docker`

**安装**

*   通过 git 克隆这个 repo

**git 克隆 https://github . com/Lu 4p/torat . git**

*   将目录更改为 ToRat

**cd。/ToRat**

*   构建 ToRat Docker 容器

*   您需要自己构建容器的一部分来获得自己的洋葱地址和证书，所有的先决条件都由 other 中预先构建的 torat-pre 映像来满足，以使快速构建成为可能

**sudo 码头建设。-t 胸片**

*   运行容器
    *   将直接进入 ToRat 服务器外壳
    *   v 标志将编译后的二进制文件复制到主机文件系统
    *   要将一台机器连接到服务器 shell，只需在另一个系统上运行一个客户机二进制文件

**sudo 坞站运行-it-v " $(pwd)"/dist:/dist _ ext torat**

*   在另一个 shell 中运行客户端。

**sudo chown $ user dist/-r
CD dist/dist/client/
。/client_linux**

*   查看客户端连接

在您的服务器外壳中，您现在应该看到类似于`[+] New Client H9H2FHFuvUs9Jz8U connected!`的内容。您现在可以通过在服务器外壳中运行`select`来选择这个客户端，这将为您提供一个很好的交互式选择器来选择您想要连接的客户端。在您选择了一个客户端之后，您在客户端系统上放入一个交互式 shell。

**注释**

docker 运行后`ToRat/dist`的内容

```
$ find ./dist
./dist/
./dist/dist
./dist/dist/client
./dist/dist/client/client_linux                   # linux client binary
./dist/dist/client/client_windows.exe             # windows client binary
./dist/dist/server
./dist/dist/server/key.pem                              # tls private-key
./dist/dist/server/banner.txt                           # banner
./dist/dist/server/cert.pem                             # tls cert
./dist/dist/server/ToRat_server                         # linux server binary 
```

**当前特征**

*   基于 RPC(远程过程调用)的通信，便于添加新功能
*   自动 upx 可生成约 6MB 的客户端二进制文件，并嵌入 Tor
*   ToRAT_client 通过 Tor 代理的 TLS 加密 RPC 与 ToRat_server 通信(隐藏服务)
    *   客户端和服务器的匿名性
    *   端到端加密
*   跨平台反向外壳(Windows、Linux、Mac OS)
*   窗口:
    *   绕过多个用户帐户控制(权限提升)
    *   多种持久性方法(用户、管理员)
*   Linux:
    *   多种持久性方法(用户、管理员)
*   不带 Tor 的可选传输，例如使用 Tor2Web、DNS 主机名或公共/本地 IP
    *   较小的二进制文件，约 7MB，已升级
    *   客户端和服务器的匿名性
*   嵌入式 Tor
*   每个客户端的唯一永久 ID
    *   给客户一个别名
    *   从客户端下载的所有内容都会保存到。/$ID/$filename
*   sqlite 通过 gorm 存储关于客户端的信息
*   客户端通过[乱码](https://github.com/burrowers/garble)混淆

**服务器外壳**

*   支持多个连接
*   欢迎横幅
*   彩色输出
*   tab-完成:
    *   命令
    *   服务器工作目录中的文件/目录

| 命令 | 信息 |
| --- | --- |
| **选择** | 选择要与之交互的客户端 |
| **列表** | 列出所有连接的客户端 |
| **别名** | 选择客户端以提供别名 |
| **cd** | 更改服务器的工作目录 |
| **帮助** | 列出可能的命令及其用法信息 |
| **退出** | 退出服务器 |

**选择客户端后的外壳**

*   tab-完成:
    *   命令
    *   客户端工作目录中的文件/目录

| 命令 | 信息 |
| --- | --- |
| **cd** | 更改客户端的工作目录 |
| **ls** | 列出客户端工作目录的内容 |
| **切丝** | 删除文件/目录不可恢复 |
| **shredremove** | 与粉碎相同+删除粉碎的文件 |
| **屏幕** | 给客户端截图 |
| **猫** | 从客户端查看文本文件，包括。docx，。rtf，。pdf，。国防运输局(Office of Defense Transportation) |
| **别名** | 给客户端一个自定义别名 |
| **向下** | 从客户端下载文件 |
| **上升** | 将文件上传到客户端 |
| **逃跑** | 对命令进行转义，并在客户端的本机 shell 中运行它 |
| **重新连接** | 告诉客户端重新连接 |
| **帮助** | 列出可能的命令及其用法信息 |
| **退出** | 后台当前会话并返回主外壳 |
| 其他 | 该命令将在客户端的本机 shell 中执行 |

**即将推出的功能**

*   Linux 的权限提升
*   Mac OS 的持久性和权限提升
*   支持 Android 和 iOS 需要修复[https://github.com/ipsn/go-libtor/issues/12](https://github.com/ipsn/go-libtor/issues/12)
*   [Windows 上的无文件持久性](https://github.com/ewhitehats/InvisiblePersistence)

**预览**

[![](img/8fe26e325277a77cd1bbfe67da742e61.png)](https://asciinema.org/a/318534)[**Download**](https://github.com/lu4p/ToRat)