# FudgeC2:用 Python3、Powershell &编写的紫色团队的合作 C2 框架。网

> 原文：<https://kalilinuxtutorials.com/fudgec2-a-collaborative-c2-framework-for-purple-teaming-written-in-python3-powershell-net/>

[![FudgeC2 : A Collaborative C2 Framework For Purple-Teaming Written In Python3, Powershell & .NET](img/56af564caed123123491d65027824686.png "FudgeC2 : A Collaborative C2 Framework For Purple-Teaming Written In Python3, Powershell & .NET")](https://1.bp.blogspot.com/-W8ZQjtbIkYc/XYXPJlppUOI/AAAAAAAACjk/aC8Rn5Y4cd0QGrbQUhKOzwPAthEiZy3aACLcBGAsYHQ/s1600/FudgeC2%2B%25281%2529.png)

**FudgeC2** 是基于 Python3/Flask 构建的面向活动的 Powershell C2 框架——专为团队协作、客户互动、活动时间表和使用可见性而设计。

**注意:** FudgeC2 目前处于 alpha 阶段，在非测试环境中使用要谨慎。测试版将于今年晚些时候在[黑帽兵工厂](https://www.blackhat.com/us-19/arsenal/schedule/#fudge-a-collaborative-c2-framework-for-purple-teaming-16968)发布。

**设置**

**安装**

要在 Linux 主机上快速安装和运行 FudgeC2，请运行以下命令:

**git 克隆 https://github.com/Ziconius/FudgeC2
CD fudge C2/fudge C2
sudo pip 3 install-r requirements . txt
sudo python 3 controller . py**

对于那些希望通过 Docker 使用 FudgeC2 的人来说，repo 中也有一个模板 Dockerfile。

##### **设置:**

FudgeC2 的默认服务器配置可以在设置文件中找到:

<install dir="">/fudge C2/Storage/settings . py</install>

这些设置包括 FudgeC2 服务器应用程序端口、SSL 配置和数据库名称。更多详情参见“服务器配置”部分。

注意:根据您的网络设计/RT 架构部署，您可能需要配置大量代理和路由调整。

有关即将发布的开发说明和最近的更改，请参见 [release.md 文件](https://github.com/Ziconius/FudgeC2/blob/master/release.md)

**也可阅读-[Stegify:用于 LSB 隐写术的 Go 工具，能够隐藏图像中的任何文件](https://kalilinuxtutorials.com/stegify-lsb-steganographycapable-hiding-file-within-image/)**

**首次登录**

初始安装后，您可以使用以下凭据以默认管理员帐户登录:

管理员:letmein

首次登录后，系统会提示您更改管理员密码。

**服务器设置**

< Reworking >
证书:如何部署/在哪里部署
端口–考虑监听器
DB 名称:

**用户**

Fudge 中的用户分为两组，管理员和标准用户。管理员拥有所有常用的功能，例如创建用户和活动，并且需要创建新的活动。

在活动 a 中，用户权限可以配置为以下之一:无/读/读+写。如果没有读取权限，用户将无法看到活动的存在，也无法读取植入响应或注册的命令。

具有读取权限的用户只能查看命令及其输出，以及活动记录页面。这个角色通常会分配给初级测试人员，或者观察者。

具有写权限的用户将能够创建植入物模板，并在所有活动植入物上执行命令。

**注意:**在进一步的开发中，这将变得更加精细，允许对特定植入物的写权限。

**用户创建**

管理员可以从全局设置选项中创建新用户。他们还可以选择为用户配置管理权限。

**战役**

**什么是战役？**

活动是一种针对客户组织约定的方法，它允许在每个用户的基础上应用访问控制

每个活动都包含唯一的名称、植入物和日志，而用户可以是多个活动的成员。

**植入物**

植入物分为 3 个部分

*   植入模板
*   陌生人
*   活性植入物

**植入模板**

植入模板是我们将创建的用于生成 stagers 的模板。植入模板将包含植入的默认配置。一旦 stager 被触发并且主机上正在运行活动植入，这可以被改变。

所需配置列表如下:

*   统一资源定位器
*   初始回拨延迟
*   港口
*   信标延迟
*   协议:
    *   HTTP(默认)
    *   HTTPS
    *   域名服务器(Domain Name Server)
    *   二进制的

创建模板后，阶段选项将显示在活动阶段页面中。

**舞台演员**

stagers 是负责下载和执行完整植入的小脚本/宏等。

一旦生成了植入体，stagers 页面将提供许多可用于危害目标的基本技术。目前可用的 stagers 有:

*   IEX 方法
*   Windows Words 宏

**主动植入**

主动植入是成功阶段执行的结果。当一个 stager 连接回软糖 C2 服务器时，一个新的主动植入被生成，并被传送到目标主机。每个 stager 执行和检入创建一个新的活动植入条目。

##### **例子**

作为活动的一部分，用户创建一个名为“Moozle Implant”的植入模板，通过 word macro 发送给人力资源部门。这将导致宏登台程序的五次成功执行；结果，用户将看到五个活动植入物。

这些将被列在活动的主植入页面上，带有一个六个字符的独特斑点。独特的植入物将列出如下:

穆兹勒植入 _123459
穆兹勒植入 _729151
穆兹勒植入 _182943
穆兹勒植入 _613516
穆兹勒植入 _810021

这些植入体中的每一个都可以单独交互，或者使用“ALL”关键字注册一个针对所有活动植入体的命令。

**植入通信**

植入将使用植入模板配置使用的任何协议与 C2 服务器通信。如果将植入设置为使用 HTTP 和 HTTPS，将需要两个监听器来确保与植入进行完全通信。

侦听器是在“侦听器”页面的 Fudge 中全局配置的。设置和修改监听者的状态需要管理员权限，因为对 stagers 的更改可能会影响使用同一 Fudge 服务器的其他正在进行的活动。

目前,“侦听器”页面显示活动的侦听器，但允许管理员:

*   在可定制的端口上为 HTTP/S、DNS 或二进制通道创建监听器
*   启动创建的监听程序
*   停止活动的侦听器
*   为监听程序分配通用名称

**植入配置进一步信息**

URL:植入将被配置为回调给定的 URL 或 IP 地址。

信标时间:[缺省值:15 分钟]这是植入回叫 C2 服务器的时间间隔。一旦植入物已经展开，就可以动态地设置它。

协议:植入物将能够使用以下协议之一:

*   超文本传送协议
*   域名服务器(Domain Name Server)
*   二元协议

用户可以根据他们认为的工作环境来启用和禁用协议。

[**Download**](https://github.com/Ziconius/FudgeC2)