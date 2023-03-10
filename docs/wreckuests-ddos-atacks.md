# 利用 HTTP-Flood 运行 DDoS 攻击的工具

> 原文：<https://kalilinuxtutorials.com/wreckuests-ddos-atacks/>

**screen uests**是一个脚本，可以让你用 **HTTP-flood** 运行 **DDoS 攻击**。它由纯粹的 Python 和应用代理服务器组成，称为**机器人**。这个脚本并不是包罗万象的，你不能简单地只点击鼠标就放弃五角大楼/国家安全局/无论什么网站。每一次攻击都是独一无二的，对于每一个网站，你都必须寻找漏洞，并表扬它们。

**警告:**此内容可以说是出于教育目的发布的！创作者将不承担任何因使用而导致的后果、伤害或不幸。

**也读 [同形异义字——获取相似字母，转换成 ASCII，检测可能的语言& UTF-8 组](https://kalilinuxtutorials.com/homoglyphs-convert-ascii-utf-8-group/)**

## **残骸特征**

1.  URL 参数随机化的缓存旁路
2.  云耀斑探测和通知
3.  自动 gzip/deflate 切换
4.  HTTP 验证绕过
5.  用户代理替代
6.  参考随机数发生器
7.  HTTP 代理支持

## **要求**

*   Python 3.5 以上版本
*   请求 2.10.0 或更高版本
*   Netaddr 用 0.7.19 测试

## **安装**

只需在所需的目录中克隆存储库，并运行安装脚本:

```
chmod +x install.sh
./install.sh
```

## **用途**

在 *sudo* 模式下键入:

`**python3 wreckuests.py -v <target url> -a <login:pass> -t <timeout>**`

### **可能的参数**:

`**-h**`或 **`--help`** :

打印带有可能参数的消息。

`**-v**`或`**--victim**`:

指定受害者网站页面的链接。它可以是网站的主页，某人的个人资料，`**.php**` **-fil** e 甚至是图片。有很大分量或者服务器很难给出的东西。选择权在你。

**`-a`** 或`**--auth**`:

绕过身份验证的参数。您的受害者可以启用基本的 HTTP 身份验证，他的网站会要求您在弹出窗口中输入登录名和密码。受害者之前可能会在 VK/FB/Twitter 和任何社交网络上发布其用户的登录和密码数据。

`**-t**` 或`**--timeout**`(默认为 10):

控制连接“n”读取超时的参数。该选项还控制终止时间。

**注意:**如果你设置`**timeout=1**`或大约 2-3 秒，慢速代理将没有任何时间连接到你的受害者的网站，甚至不会击中它。如果你确定你的代理足够快

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/JamesJGoodwin/wreckuests)