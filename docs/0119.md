# 洋葱 nmap 扫描隐藏的洋葱服务

> 原文：<https://kalilinuxtutorials.com/onion-nmap-scan-hidden-services/>

利用 nmap 扫描 Tor 网络上隐藏的“洋葱”优势。鉴于高架无意义的图片，利用 proxychains 包装 nmap。Tor 和 dnsmasq 通过 s6 保持作为守护进程运行，proxychains 包装 nmap 以利用端口 9050 上的 Tor SOCKS 中介。

Tor 同样设计为通过 DNSPort 秘密解析对端口 9053 的 DNS 请求。dnsmasq 被安排使用这个 localhost:9053 作为专家 DNS 服务器。Proxychains 通过附近的解析器安排给中介 DNS，因此所有 DNS 请求都将经历 Tor，应用程序可以解析。洋葱地址。

**也可理解为 [CloudFrunt 工具，用于识别错误配置的 CloudFront 域](http://kalilinuxtutorials.com/cloudfrunt-misconfigured-domains/)**

## **洋葱 nmap 的工作原理:**

当容器启动时，它启动 Tor 和 dnsmasq 作为守护进程。然后，`tor_wait`脚本在执行您的命令之前等待 Tor SOCKS 代理启动。

### **论据:**

默认情况下，`docker run`的参数被传递给/bin/nmap，后者调用带有参数`-sT -PN -n "$@"`的 nmap，这是它在 Tor 上工作所必需的(通过 explainshell.com)。

**比如这个:**

```
docker run --rm -it milesrichardson/onion-nmap -p 80,443 facebookcorewwwi.onion
```

**将被执行为:**

```
proxychains4 -f /etc/proxychains.conf /usr/bin/nmap -sT -PN -n -p 80,443 facebookcorewwwi.onion
```

除了`nmap`的定制脚本之外，还有`curl`和`nc`的定制包装器脚本，用于将它们包装在 proxychains、at /bin/curl 和/bin/nc 中。要调用它们，只需指定`curl`或`nc`作为`docker run`的第一个参数。例如:

```
docker run --rm -it milesrichardson/onion-nmap nc -z 80 facebookcorewwwi.onion
```

**将被执行为:**

```
proxychains4 -f /etc/proxychains.conf /usr/bin/nc -z 80 facebookcorewwwi.onion
```

**和**

```
docker run --rm -it milesrichardson/onion-nmap curl -I https://facebookcorewwwi.onion
```

**将被执行为:**

```
proxychains4 -f /etc/proxychains.conf /usr/bin/curl -I https://facebookcorewwwi.onion 
```

如果你想调用任何其他命令，包括原来的`/usr/bin/nmap`或`/usr/bin/nc`或`/usr/bin/curl`，你可以将它指定为 docker run 的第一个参数，例如:

```
docker run --rm -it milesrichardson/onion-nmap /usr/bin/curl -x socks4h://localhost:9050 https://facebookcorewwwi.onion
```

### **环境变量:**

只有一个环境变量:`DEBUG_LEVEL`。如果您将它设置为除了`0`之外的任何值，将会打印更多的调试信息(特别是在等待 Tor 启动时尝试连接到 Tor)。示例:

```
$ docker run -e DEBUG_LEVEL=1 --rm -it milesrichardson/onion-nmap -p 80,443 facebookcorewwwi.onion
[tor_wait] Wait for Tor to boot... (might take a while)
[tor_wait retry 0] Check socket is open on localhost:9050...
[tor_wait retry 0] Socket OPEN on localhost:9050
[tor_wait retry 0] Check SOCKS proxy is up on localhost:9050 (timeout 2 )...
[tor_wait retry 0] SOCKS proxy DOWN on localhost:9050, try again...
[tor_wait retry 1] Check socket is open on localhost:9050...
[tor_wait retry 1] Socket OPEN on localhost:9050
[tor_wait retry 1] Check SOCKS proxy is up on localhost:9050 (timeout 4 )...
[tor_wait retry 1] SOCKS proxy DOWN on localhost:9050, try again...
[tor_wait retry 2] Check socket is open on localhost:9050...
[tor_wait retry 2] Socket OPEN on localhost:9050
[tor_wait retry 2] Check SOCKS proxy is up on localhost:9050 (timeout 6 )...
[tor_wait retry 2] SOCKS proxy UP on localhost:9050
[tor_wait] Done. Tor booted.
[nmap onion] nmap -p 80,443 facebookcorewwwi.onion
[proxychains] config file found: /etc/proxychains.conf
[proxychains] preloading /usr/lib/libproxychains4.so
[proxychains] DLL init: proxychains-ng 4.12

Starting Nmap 7.60 ( https://nmap.org ) at 2017-10-23 16:34 UTC
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  facebookcorewwwi.onion:443  ...  OK
[proxychains] Dynamic chain  ...  127.0.0.1:9050  ...  facebookcorewwwi.onion:80  ...  OK
Nmap scan report for facebookcorewwwi.onion (224.0.0.1)
Host is up (2.8s latency).

PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 4.05 seconds
```

### 备注:

*   Tor 上没有 UDP 可用
*   Tor 可能需要 10-20 秒才能启动。如果这是不可行的，另一个选择是在它自己的容器中运行代理，或者作为主进程运行它，然后运行“exec”来调用 nmap 之类的命令

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/milesrichardson/docker-onion-nmap)