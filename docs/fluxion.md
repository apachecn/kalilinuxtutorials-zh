# fluxion——vk 496 重新制作的 Linset，错误更少，功能更强

> 原文：<https://kalilinuxtutorials.com/fluxion/>

流动是 MITM 水渍险攻击的未来。Fluxion 是一个安全审计和社会工程研究工具。它是 vk496 的 linset 的翻版，有(希望)更少的错误和更多的功能。该脚本试图通过社会工程(网络钓鱼)攻击从目标接入点检索 WPA/WPA2 密钥。它与 Kali(滚动)的最新版本兼容。Fluxion 的攻击设置大多是手动的，但实验性的自动模式处理一些攻击的设置参数。请求问题前，请阅读[常见问题解答](https://github.com/FluxionNetwork/fluxion/wiki/FAQ)。

**也读作[Windows spyblocker-Block 刺探&Windows 上的跟踪](https://kalilinuxtutorials.com/windowsspyblocker/)**

## **流动安装**

**下载最新版本**

```
git clone --recursive git@github.com:FluxionNetwork/fluxion.git
```

**切换到刀具目录**

```
cd fluxion
```

**运行 fluxion(缺少的依赖项将被自动安装)**

```
./fluxion.sh
```

**拱形**中也有流动

```
cd bin/arch
makepkg
```

或者使用 blackarch 回购

```
pacman -S fluxion
```

## **工作原理**

*   扫描目标无线网络。
*   发起`Handshake Snooper`攻击。
*   捕捉握手(密码验证所必需的)。
*   发动`Captive Portal`攻击。
*   产生一个流氓(假)接入点，模仿原来的接入点。
*   产生一个 DNS 服务器，将所有请求重定向到运行强制网络门户的攻击者主机。
*   产生一个 web 服务器，为提示用户输入 WPA/WPA2 密钥的强制网络门户提供服务。
*   产生一个干扰器，取消所有来自原始 AP 的客户端的认证，并将它们引诱到流氓 AP。
*   根据之前捕获的握手文件检查强制网络门户上的所有身份验证尝试。
*   一旦提交了正确的密钥，攻击将自动终止。
*   该密钥将被记录，客户端将被允许重新连接到目标接入点。

## **免责声明**

*   作者不拥有`/attacks/Captive Portal/sites/`目录下的徽标。版权声明根据 1976 年版权法 107 节，允许出于批评、评论、新闻报道、教学、学术和研究等目的的“合理使用”。
*   未经双方事先同意而使用 Fluxion 攻击基础设施可能会被视为非法活动，其作者/开发者非常不鼓励这样做。最终用户有责任遵守所有适用的地方、州和联邦法律。作者不承担任何责任，也不对该程序造成的任何误用或损害负责。

**注意:** Fluxion **在 Windows 10 的 Linux 子系统上不工作**，因为该子系统不允许访问网络接口。任何与此相关的问题都将被**立即关闭**

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/FluxionNetwork/fluxion)