# Sish : HTTP(S)/WS(S)/TCP 仅使用 SSH 建立到本地主机的隧道

> 原文：<https://kalilinuxtutorials.com/sish/>

[![Sish : HTTP(S)/WS(S)/TCP Tunnels To Localhost Using Only SSH](img/bb5df97f128059f657102db1ef9a4f7f.png "Sish : HTTP(S)/WS(S)/TCP Tunnels To Localhost Using Only SSH")](https://1.bp.blogspot.com/-6SnZx_mQBqY/YINK5Yct4DI/AAAAAAAAI0w/R4D_PGe_-9EwaGzLJU4mYyWZ7YmTAhLVACLcBGAsYHQ/s728/Sish.png)

Sish 是一个开源的 serveo/ngrok 替代品。

每次提交到 repo 时都会自动进行构建，并将其推送到 Dockerhub。使用提交 sha、分支名称、标记、最新(如果在主服务器上发布)来标记构建。你可以在这里找到一份名单[。每个版本都构建了独立的`sish`二进制文件，可以从](https://hub.docker.com/r/antoniomika/sish/tags)[这里](https://github.com/antoniomika/sish/releases)下载，用于各种操作系统/架构。您可以随意使用自动化的二进制文件或构建自己的二进制文件。如果您提交 PR，默认情况下不会构建图像，需要维护人员重新标记。

*   调出 Docker 图像

`**docker pull antoniomika/sish:latest**`

*   运行图像

**docker run-itd–name sish \-v ~/sish/SSL:/SSL \-v ~/sish/keys:/keys \-v ~/sish/pubkeys \–net = host antoniomika/sish:latest \–ssh-address =:22 \–http-address =:80 \–https-address =:443 \–https = true \–https-certificate-directory =/SSL \–authentic ation-keys-directory =/pubkeys \**

*   SSH 到您的主机以与 sish 通信

`**ssh -p 2222 -R 80:localhost:8080 ssi.sh**`

**坞站组成**

您还可以使用 Docker Compose 来设置您的 sish 实例。这包括通过让我们为你加密来处理 SSL。这使用了 [adferrand/dnsrobocert](https://github.com/adferrand/dnsrobocert) 容器来处理通过 DNS 发布通配符证书。有关如何使用它更多信息，请访问上面的链接。通常，您可以像这样部署您的服务:

**对接器-组合-f 部署/对接器-组合. yml up -d**

应该更新`**deploy/docker-compose.yml**`和`**deploy/le-config.yml**`中的域和 DNS 验证信息，以反映您的需求。您还需要创建一个符号链接，指向您的域的“让我们加密证书”,例如:

**ln-s/etc/lets encrypt/live/<你的域>/full chain . PEM deploy/SSL/<你的域>。CRT
ln-s/etc/lets encrypt/live/<你的域> /privkey.pem deploy/ssl/ <你的域>。关键**

小心:符号链接需要指向`/etc/letsencrypt`，而不是相对路径。符号链接不会在主机文件系统上解析，但是它们会在 sish 容器内部解析，因为它将 letsencrypt 文件挂载在/etc/letsencrypt，*而不是*中。/letsencrypt。

我在部署`ssi.sh`时使用了这些文件，为了保持一致性，我在这里包含了它们。

**谷歌云平台**

有一个在 Google 云平台中创建 sish 完全设置实例的教程，可以在[这里](https://github.com/antoniomika/sish/blob/main/deploy/gcloud.md)找到。可以通过[谷歌云壳](https://cloud.google.com/shell)访问。

它是如何工作的？

SSH 通常可以转发本地和远程端口。该服务实现了一个 SSH 服务器，它只处理转发，不处理其他任何事情。该服务通过 WebSocket 支持 HTTP/HTTPS 上的多路复用连接。只需将一个远程端口指定为端口`80`来代理 HTTP 流量，将端口`443`指定为代理 HTTPS 流量。如果您使用任何其他远程端口，服务器将侦听 TCP 连接的端口，但前提是该端口可用。

您可以选择自己的子域，而不是依赖随机分配的子域，方法是将`--bind-random-subdomains`选项设置为`false`，然后通过将子域添加到远程端口说明符前来选择子域:

`**ssh -p 2222 -R foo:80:localhost:8080 ssi.sh**`

如果选择的子域没有被占用，它将被分配给你的连接。

**支持的转发类型**

*   **HTTP 转发**

sish 可以通过 SSH 转发任意数量的 HTTP 连接。它还提供了一个 web 界面，用于查看对每个转发连接的完整请求和响应。每个 web 接口对于转发的连接可以是唯一的，或者使用统一的访问令牌。为了利用 HTTP 转发，使用端口`[80, 443]`告诉 sish 正在转发 HTTP 连接，并且应该为服务定义 HTTP virtualhosting。例如，假设我正在我的笔记本电脑上的端口`8080`开发一个使用 websockets 的 HTTP 服务，我想显示一个不在我附近的同事。我可以像这样转发连接:

**ssh-R hereiam:80:localhost:8080 SSI . sh**

然后将链接`https://hereiam.ssi.sh`分享给我的同事。他们应该能够通过 HTTPS 无缝地访问服务，完全的 websocket 支持工作良好。假设`hereiam.ssi.sh`不可用，那么 sish 会随机生成一个子域并给我。

*   **TCP 转发**

任何基于 TCP 的服务都可以与 sish 一起用于 TCP 和别名转发。TCP 转发将在您部署 sish 的服务器上建立一个远程端口，并通过 SSH 连接将所有连接转发到该端口和您的本地设备。例如，如果我要在我的笔记本电脑上使用端口`22`运行一个 SSH 服务器，并希望能够在`ssi.sh:2222`从任何地方访问它，我可以在我的笔记本电脑上使用 SSH 命令来转发连接:

**ssh-R 2222:localhost:22 SSI . sh**

我可以使用转发的连接从任何地方访问我的笔记本电脑:

**ssh -p 2222 ssi.sh**

*   **TCP 别名转发**

比如说，我不希望世界上的其他人可以访问这个服务，那么你可以使用一个 TCP 别名。TCP 别名是一种转发的 TCP 连接，只存在于 sish 内部。您可以通过使用带有`-W`标志的 SSH 来访问别名，这将把 SSH 进程的 stdin/stdout 转发到转发的 TCP 连接。结合身份验证，这将保证您的远程服务是安全的，因为您需要登录 sish 才能访问它。更改上面的示例意味着在我的笔记本电脑上运行以下命令:

**ssh-R my laptop:22:localhost:22 SSI . sh**

sish 不再向外界发布端口 22 或 2222，而是保留一个指针，指示在用户向`mylaptop:22`认证后从 SSH 内部建立的 TCP 连接应该被转发到转发的 TCP 隧道。然后，我可以使用转发连接从任何地方访问我的笔记本电脑:

**ssh-o proxy command = " ssh-W % h:% p SSI . sh " my laptop**

对于较新的 SSH 版本，这是什么的简写:

**ssh -J ssi.sh mylaptop**

**认证**

如果你想私下使用这个服务，它同时支持公钥和密码认证。要启用身份验证，请将`**--authentication=true**`设置为您的 CLI 选项之一，并确保根据您的喜好配置`**--authentication-password**`或`**--authentication-keys-directory**`。由`**--authentication-keys-directory**`提供的目录被监视是否有变化，并将自动重新加载授权密钥。授权证书索引在目录修改时重新生成，因此删除的公钥也将自动删除。这个目录中的文件可以是每个文件一个键，也可以是每个文件多个键，用换行符隔开，类似于`**authorized_keys**`。可以通过将`**--authentication-password=""**`设置为 CLI 选项来禁用密码验证。

我最喜欢的一种身份验证方式是这样的:

**sish @ sish 0:~/sish/pubkeys # curl https://github.com/antoniomika.keys>Antonio mika**

这将从 GitHub 加载我的公钥，把它们放在 sish 正在监视的目录中，然后加载 pubkey。这个命令一运行，我就可以正常 SSH 了，它会授权我。

**自定义域名**

sish 支持允许用户将自定义域带到服务中，但是需要启用 SSH key auth。要使用此功能，您必须为要用于转发连接的域/子域设置 TXT 和 CNAME/A 记录。CNAME/A 记录必须指向承载 sish 的域或 IP。TXT 记录必须是类似于以下内容的`key=val`字符串:

**sish=SSHKEYFINGERPRINT**

其中`SSHKEYFINGERPRINT`是用于登录服务器的密钥的指纹。您可以设置多个 TXT 记录，sish 将检查所有记录，以确保至少有一个匹配。您可以通过运行以下命令来检索您的密钥指纹:

**ssh-keygen -lf ~/。ssh/id _ RSA | awk“{ print $ 2 }”**

如果您信任连接到 sish 的用户，并希望允许任何域与 sish 一起使用(绕过验证)，有几个添加的标志对此有所帮助。这在向 sish 添加多个通配符证书时特别有用，这样就不需要自动提供加密证书了。要禁用验证，请设置`--bind-any-host=true`，这将允许使用子域/域组合。要仅允许某个域子集的子域，您可以将`--bind-hosts`设置为允许绑定的逗号分隔的域列表。

要添加供 sish 使用的证书，请将`--https-certificate-directory`标志配置为指向 sish 可访问的目录。在这个目录中，sish 将寻找类似于`name.crt`和`name.key`的文件组合。`name`在任何一种情况下都可以是任意的，它只需要对证书和密钥对是唯一的，以允许它们被加载到 sish 中。

**负载均衡**

sish 可以对任何类型的转发连接进行负载平衡，但这需要在使用`--http-load-balancer`、`--tcp-load-balancer`和`--alias-load-balancer`标志启动 sish 时启用。假设您有几个边缘节点(raspberry pis)在内部运行服务，但您希望能够从外部平衡这些设备之间的负载。通过在 sish 中启用负载平衡，当具有相同转发 TCP 端口、别名或 HTTP 子域的设备连接到 sish 时，这将自动发生。然后，连接将被平均分配给连接到 sish 且与转发的连接相匹配的任何节点。

**将 IP 列入白名单**

将 IP 范围或国家列入白名单也是可能的。可以使用`--whitelisted-ips`选项指定整个 CIDR 范围，该选项接受逗号分隔的字符串，如“192.30.252.0/22，185.199.108.0/22”。如果您想将单个 IP 列入白名单，请使用`/32`范围。

要将国家列入白名单，使用`--whitelisted-countries`和 ISO 格式的逗号分隔的国家字符串(例如，“pt”代表葡萄牙)。你还需要将`--geodb`设置为`true`。

**DNS 设置**

要使用 sish，您需要添加一个用于复用子域的通配符 DNS 记录。将带有`*`的`A`记录作为子域添加到您的服务器的 IP 地址是实现这种配置的最简单的方法。

**演示–此时，演示实例已被设置为因滥用而需要授权**

有一个演示服务(和我的私有实例)正在`ssi.sh`上运行，它不需要任何认证。该服务提供默认日志记录(错误、连接 IP/用户名和公钥指纹)。我不记录任何密码验证数据或在服务/隧道内发送的数据。我的部署使用上面列出的精确部署步骤。该实例仅用于测试和教育目的。您可以非常容易地在任何主机上部署它(Google Cloud Platform 提供了一个永远免费的实例，它应该可以完美地运行)。如果服务开始产生大量流量，我将启用身份验证，然后你可以联系我将你的 SSH 密钥列入白名单(确保它在 GitHub 上，并且你向我提供你的 GitHub 用户名)。

**注释**

1.  无论如何，这都不是生产就绪。这是一起黑客攻击，并解决了一个相当具体的用例。
    *   您可以通过提交 PRs/审查代码/编写测试等来帮助 it 做好生产准备
2.  这是一个相当简单的实现，我故意在一些地方偷工减料，使它更容易编写。
3.  如果您有任何问题或意见，请随时通过电子邮件 [me@antoniomika.me](mailto:me@antoniomika.me) 或通过 [freenode IRC #sish](https://kiwiirc.com/client/chat.freenode.net:6697/#sish) 联系我们

**升级到 1.0 版**

sish 在 1.0 之前和 1.0 之后的版本之间有许多突破性的变化。最大的变化出现在命令标志和配置参数的映射中。这些都发生了巨大的变化，但找到新的对应应该很容易。另一个变化是主机密钥授权支持 SSH 密钥。sish 继续支持大多数现代密钥，但是默认情况下，如果没有找到主机密钥，它将创建一个 OpenSSH ED25519 密钥来使用。sish 的早期版本会对这个私钥的 pem 块进行 aes 加密，但是我们已经开始使用本地的 [OpenSSH 私钥格式](https://github.com/openssh/openssh-portable/blob/master/sshkey.c)来实现 OpenSSH 工具之间的简单互操作。因此，您要么必须手动转换 AES 加密密钥，要么生成一个新密钥。

[**Download**](https://www.kitploit.com/2021/04/sish-httpswsstcp-tunnels-to-localhost.html)