# Onionservice:在类似 Unix 的操作系统上通过 CLI 或 TUI 管理您的 Onion 服务

> 原文：<https://kalilinuxtutorials.com/onionservice/>

[![](img/c77e0d23bbc04974b3eff0ea1cf2d80c.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhdD8QIDxwa1R8nRbFwQOiPYI3sXeg53onrnigMy8yxdBxYK3BH0X16srvDK3-dPhEhU2iYHAGW0TgAeTgSh6CRoD_2o4WbYaBxT9IKezVIyO5mBmOlRsPE4H_0bM3gpdmaUIBDl_TlTnk_0aJ82lQ2GLY0SRROoKvDOr4xPSZD4tmzieWHh7JJEHqy=s728)

Onionservice 是一个最低要求的、可移植的脚本和文档集合，用于帮助服务操作员处理(管理)他的洋葱。

**警告:** `**do not trust this repo yet**` **，请将您的 hs 密钥备份到另一个位置。此项目尚未发布，应考虑仅用于开发。**

**历史**

这个项目是在看到令人惊叹的 OnionShare CLI python 脚本后开始的，这些脚本有可能成为短暂的 onion 服务，永远不会接触到磁盘，可以轻松地在 Tails 或 Whonix 上运行。在看到 Raspberry Pi 的 RaspiBlitz onion 服务 bash 脚本后，将它移植到任何 Debian 发行版的想法开始了。随着想法的发展，使用 GNU Bash 和 Linux 是一个单一的失败点 1 2，因此使脚本 POSIX 兼容任何类似 Unix 的系统是一个明确的目标。

**目标**

该项目的目标是:

*   简化 onion 服务管理，从激活服务到为其添加客户端授权，提供手动编辑文件的全部功能，但操作更简单。
*   向展示管理洋葱服务不仅仅是使用网页服务器。
*   分发，从源代码级别(FOSS)到允许任何人在任何操作系统、shell 或服务管理器上运行代码所产生的效果。从单点故障中缓解

从单点故障中缓解:

*   **内核**从占主导地位的`**Linux**`到同样的`**BSD**`和任何其他类 Unix 系统。
*   **外壳**从主要的`**Bash**`到任何 POSIX 外壳如 **`ksh`、`(y,d)ash`** 和`**Zsh**`(仿效 sh)。
*   **服务经理**从主要`**Systemd**`到同时`**RC**`、`**OpenRC**`、`**SysVinit**`、`**Runit**`。

编辑 tor 配置文件(torrc)并不困难，但是自动化解决了错误配置和以下问题:

*   运行单行命令花费的时间更少
*   在应用之前拒绝无效配置，从而避免停机
*   完全一致
*   帮助新手的图形界面

**特色**

*   **启用服务**–如果目录不存在，则创建目录(HiddenServiceDir)，选择洋葱版本(HiddenServiceVersion)，自定义套接字类型为 unix 或 tcp，虚拟端口数量不限，目标也不限(HiddenServicePort)。
*   **禁用服务**–从 torrc 中移除服务配置，该服务将不再可用，但您可以随时再次启用它。可以选择清除服务，删除其配置和目录，这将永久删除其密钥。
*   **更新服务地址**–专注于私有洋葱服务，如果您泄露了它的地址，您可以更改它的主机名，小心您的所有授权客户端将被断开连接，服务密钥将被永久删除。
*   **凭证**–显示主机名、客户端、torrc 块、二维码主机名。
*   **洋葱认证**–仅适用于 v3 洋葱服务。这取决于客户端和服务器端的配置，并使用一个密钥对，客户端持有由自己生成(更安全)或由服务运营商给出的私钥部分，而洋葱服务运营商持有公钥部分。如果有的话如果
    *   **服务器**–生成密钥对或添加公共部分，从`**<HiddenServiceDir>/authorized_clients/<client>.auth**`开始列出客户端名称及其公共密钥。如果配置了任何客户端，未经身份验证将无法访问该服务。
    *   **客户端**–生成密钥对或添加公共部分，列出您的`**<ClientOnionAuthDir>/<SOME_ONION>.auth_private**`。
*   **onion-Location**–对于公共的 Onion 服务，您可以使用 nginx、apache2 和 html 头属性指南将您的 plainnet 用户重定向到您的 Onion 服务。
*   **后援**——最好安全。
    *   **创建**–备份包含隐藏服务配置的`**torrc**`行，以及`**HiddenServiceDir**`和`**ClientOnionAuthDir**`的所有目录。
    *   **集成**–将`**torrc**`和目录`**HiddenServiceDir**`和`**ClientOnionAuthDir**`中的隐藏服务线路配置集成到您当前的系统中。在创建备份并导入到当前主机后，应使用此选项。
*   **op sec**–操作安全
    *   Vanguards–这个插件可以防止安全发现和相关的流量分析攻击。防护发现攻击使对手能够确定 Tor 客户端和/或 Tor 洋葱服务使用的防护节点。一旦知道了保护节点，可以使洋葱服务(或洋葱服务用户)失去匿名性的流量分析攻击就变得更加容易。
    *   **Unix 套接字**–支持在 Unix 套接字上启用洋葱服务，以避免本地主机旁路。
*   **Web 服务器**–使用 Nginx 或 Apache2 web 服务器通过您的隐藏服务提供文件。
*   **可用性**——有两个与项目兼容的对话框，`**dialog**`和 **`whiptail`。**
*   **Bulk**–一些命令可以使用参数`**@all**`进行扩展，以包括所有服务或客户端，具体取决于选项`**--service**`或`**--client**`，列出启用的参数`[**SERV1,SERV2,...]**`和`**[CLIENT1,CLIENT2,...]**`，命令将循环变量并应用组合。
*   **防呆**–脚本尽力过滤无效命令和不正确的语法。这些命令并不难，但乍一看可能会吓到你。不用担心，如果无效就不会运行，避免 tor 守护进程因为配置无效而无法重新加载。如果运行无效命令，请打开一个问题。

**要求**

*   常规:
    *   类 Unix 系统。
    *   使用`**doas**`或`s**udo**`作为 root 和 tor 用户调用命令的超级用户权限。
*   必需的程序:
    *   **sh**–任意 POSIX shell: `**das**h` 0.5.4+，`**bash**` 2.03+，`**ksh**` 88+，`**mksh**` R28+，`**yash**` 2.29+，busybox `**ash**` 1.1.3+，`**zsh**` 3.1.9+ ( `**zsh --emulate sh**`)等。
    *   **doas** / **sudo** (必须已经配置)
    *   **tor** > = 0.3.5.7
    *   **抓到了** > =0.9
    *   **sed**
    *   **焦油**(备份)
    *   **openssl** > = 1.1(客户端授权——需要算法 x25519，所以不能是 LibreSSL)
    *   **basez** > = 1.6.2(客户端授权)
    *   **git**  (Vanguards)
    *   **python(3)-stem**>= 1 . 8 . 0(先锋)
    *   **对话框** / **鞭尾** (TUI)
    *   **nginx**/**Apache 2**(Web 服务器)
*   可选程序:
    *   **(lib)qrencode** > = 4.1.1(列表)
*   发展计划:
    *   pandoc (手动)
    *   **外壳检查**(审查)

如果使用 Vanguards，`**python2.6**`是阀杆的最低要求，但默认情况下不会安装。

**指令**

**克隆存储库**

**git 克隆 https://github.com/nyxnor/onionjuggler.git
CD on 杂耍者**

**et 自定义变量**

您不应修改`**/etc/onionjuggler/onionjuggler.conf**`上的默认配置，它将在每次更新时被修改。您的本地配置应该在`**/etc/onionjuggler/conf.d/*.conf**`上。

要为变量赋值，您可以:

*   用您喜欢的编辑器打开提到的配置文件:
*   **" $ { EDITOR:-VI } "/etc/onion 杂耍者/cond.d/local.conf**

或者用 tee 将配置插入到文件的末尾:

**printf " su _ cmd = \ " sudo \ " \ n " | tee-a/etc/onion 杂耍者/cond.d/local.conf**

或者用 sed 编辑:

**sed -i" "s|^su_cmd=.* | su _ cmd = \ " doas \ " | "/etc/onion 杂耍者/cond.d/local.conf**

**设置环境**

从克隆的存储库内部运行以创建 tor 目录，创建手册页并将脚本复制到路径:

。**/configure . sh–安装**

**用途**

**configure.sh**

**configure.sh** 通过将脚本和手册页添加到 path 并检测您的操作系统以符合其默认配置，来设置 onion 杂耍器的环境。它也可以用于卸载。常见的开发用途是创建手册页、检查 shell 语法并执行上述所有操作，以及为要提交的文件提供 git 状态。更新选项是原始的，目前只推荐用于开发。

**安装**

**configure . sh–install # #-I**

**卸载**

**configure . sh–uninstall # #-d**

**更新**

**configure . sh–update # #-u**

**推**

**onionspetcher-tui**将 CLI 包装在终端用户界面中。一些 TUI 选项将允许您编辑授权文件，建议将您最喜欢的文本编辑器设置为一个环境变量，将按以下顺序尝试: **`DOAS_EDITOR` / `SUDO_EDITOR`** ，如果为空将尝试`**VISUAL**`，如果为空将尝试`**EDITOR**`，如果为空将回退到`**Vi**`。

阅读 tui 手册

男人变戏法-推

要使用 TUI，只需运行:

**洋葱杂耍者-推**

cli

onionstappler-CLI 是管理隐藏服务的主要脚本。看看`docs`文件夹中的文档，有许多其他的洋葱服务管理指南。阅读:

不要忘记 cli 手册和 conf 手册的高级用法:

**man onion 杂耍者-CLI
man onion 杂耍者. conf**

要创建名为`**terminator**`的服务，尽可能简单:

洋葱杂耍者-cli 激活-s 终结器-p 80

但是也可以像指定所有参数一样高级:

**onionstaller-CLI activate–服务终结器–socket UNIX–版本 3–端口 80，127.0.0.1:80**

[**Download**](https://github.com/nyxnor/onionjuggler)