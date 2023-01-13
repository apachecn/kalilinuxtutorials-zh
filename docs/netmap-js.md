# 网络地图。Js:基于浏览器的快速网络发现模块

> 原文：<https://kalilinuxtutorials.com/netmap-js/>

[![Netmap.Js : Fast Browser-Based Network Discovery Module](img/9311d19235359fdf2d7e4660f28e254f.png "Netmap.Js : Fast Browser-Based Network Discovery Module")](https://1.bp.blogspot.com/-wYHuIndPVv8/YF47LXT1G7I/AAAAAAAAIpM/T9MeE0fUqVklcg1PyBK2Y3SAy_Lzzk-6QCLcBGAsYHQ/s728/Net%25281%2529.png)

`**netmap.js**`提供基于浏览器的主机发现和端口扫描功能，让您能够映射网站访问者的网络。

它非常快，利用 [`es6-promise-pool`](https://github.com/timdp/es6-promise-pool) 来高效地运行浏览器允许的最大数量的并发连接。

**动机**

我需要一个基于浏览器的端口扫描器来实现我的一个想法。我认为这将是一个简单的问题，从另一个项目如 [BeEF](http://beefproject.com/) 导入一个现有的模块或复制粘贴。

结果是没有一个像样的现成的`npm`模块，BeEF 中的 [`port_scanner`](https://github.com/beefproject/beef/blob/master/modules/network/port_scanner/command.js) 模块(在撰写本文时)不准确、速度慢并且不能在 Chromium 上工作。

因此，是一个稍微优化的“ping”扫描程序和 TCP 扫描程序，可以在所有现代浏览器上工作。

**快速启动**

**安装**

**npm 安装–保存 netmap.js**

**寻找直播主持人**

让我们从家庭环境中可能的候选者列表开始，找出网站访问者网关的 IP 地址:

```
import NetMap from 'netmap.js'

const netmap = new NetMap()
const hosts = ['192.168.0.1', '192.168.0.254', '192.168.1.1', '192.168.1.254']

netmap.pingSweep(hosts).then(results => {
  console.log(results)
})
```

```
{
  "hosts": [
    { "host": "192.168.0.1", "delta": 1003, "live": false },
    { "host": "192.168.0.254", "delta": 1001, "live": false },
    { "host": "192.168.1.1", "delta": 18, "live": true },
    { "host": "192.168.1.254", "delta": 1002, "live": false }
  ],
  "meta": {}
}
```

主持人`192.168.1.1`似乎正在直播。

**扫描 TCP 端口**

*   让我们尝试在几台主机上找到一些开放的 TCP 端口:

```
import NetMap from 'netmap.js'

const netmap = new NetMap()
const hosts = ['192.168.1.1', '192.168.99.100', 'google.co.uk']
const ports = [80, 443, 8000, 8080, 27017]

netmap.tcpScan(hosts, ports).then(results => {
  console.log(results)
})
```

```
{
  "hosts": [
    {
      "host": "192.168.1.1",
      "control": "22",
      "ports": [
        { "port": 443, "delta": 15, "open": false },
        { "port": 8000, "delta": 19, "open": false },
        { "port": 8080, "delta": 21, "open": false },
        { "port": 27017, "delta": 26, "open": false },
        { "port": 80, "delta": 95, "open": true }
      ]
    },
    {
      "host": "192.168.99.100",
      "control": "1001",
      "ports": [
        { "port": 8080, "delta": 40, "open": true },
        { "port": 80, "delta": 1001, "open": false },
        { "port": 443, "delta": 1000, "open": false },
        { "port": 8000, "delta": 1004, "open": false },
        { "port": 27017, "delta": 1000, "open": false }
      ]
    },
    {
      "host": "google.co.uk",
      "control": "1001",
      "ports": [
        { "port": 443, "delta": 67, "open": true },
        { "port": 80, "delta": 159, "open": true },
        { "port": 8000, "delta": 1001, "open": false },
        { "port": 8080, "delta": 1002, "open": false },
        { "port": 27017, "delta": 1000, "open": false }
      ]
    }
  ],
  "meta": {}
}
```

*   乍一看，结果似乎是矛盾的。

*   `192.168.1.1`是本地网段上的嵌入式 Linux 机器(路由器)，唯一打开的端口是`80`。我们可以看到，与其他关闭的端口相比，浏览器在`80`上出错的时间要长 5 倍。

*   `192.168.99.100`是端口`8080`打开的纯主机虚拟机，`google.co.uk`是`443`和`80`都打开的外部主机。在这些情况下，浏览器在打开的端口上相对快速地抛出一个错误，而关闭的端口只是超时。下面的[理论](https://github.com/serain/netmap.js#theory)部分解释了这种情况何时发生。

*   为了确定端口应该标记为开放还是关闭，`netmap.js`将扫描一个被认为是关闭的“控制”端口(默认为`45000`)。然后使用`control`时间来确定其他端口的状态。如果比值`delta/control`大于设定值(默认`0.8`，则认为端口关闭(t1；dr:与控制时间的差值超过 20%意味着端口打开)。

**限制**

**端口黑名单**

浏览器会维护一个黑名单，列出它们拒绝连接的端口(如 FTP、SSH 或 SMTP)。如果您尝试使用默认协议(`http`)用`netmap.js`扫描这些端口，您将得到一个非常短的超时。短暂的超时通常是端口被关闭的标志，但是在黑名单端口的情况下，这并不意味着什么。

您可以从以下来源查看黑名单:

*   [铬源](https://github.com/adobe/chromium/blob/master/net/base/net_util.cc)
*   [Mozilla 文档](https://developer.mozilla.org/en-US/docs/Mozilla/Mozilla_Port_Blocking)
*   Edge/IE(如果找到来源，请发送链接给我)

在 [Firefox 61](https://blog.mozilla.org/security/2018/05/07/blocking-ftp-subresource-loads-within-non-ftp-documents-in-firefox-61/) (也许还有其他浏览器)之前，可以通过使用`ftp`协议代替`http`来建立连接，从而绕过这个限制。实例化`NetMap`时，可以在 options 对象中指定`protocol`。当使用`ftp`时，你应该预料到打开的端口会超时，关闭的端口会相对较快地出错。`ftp`扫描还受到本文中讨论的 TCP `RST`数据包的限制。

来自像`ftp`这样的“遗留”协议的子资源请求在 Chromium 中被阻塞了一段时间。

**“乒”的一声扫过**

`netmap.js`提供的“ping”扫描功能在快速查找本地网段上基于 live *nix 的主机(其他计算机、电话、路由器、打印机等)方面做得非常好。)

然而，由于实现的原因，当 TCP `RST`包没有被返回时，这将不起作用。通常情况下:

*   Windows 机器
*   一些外部主机
*   一些网络设置，如桥接/纯主机虚拟机

这背后的原因在下面的[理论](https://github.com/serain/netmap.js#theory)部分解释。

这种限制不会影响 TCP 扫描功能，仍然可以通过尝试在上面找到一个打开的端口来确定上面的主机是否处于活动状态。

**普遍缺乏准确性**

总的来说，我发现这个模块比我在网上找到的其他代码更准确、更快。也就是说，从浏览器绘制网络地图的整个想法天生就让人烦躁不安。您的里程可能会有所不同。

**用途**

**`NetMap`建造者**

`NetMap`构造函数接受一个选项对象，该对象允许您配置:

*   用于扫描的`protocol`(默认为`http`，请参见[端口黑名单](https://github.com/serain/netmap.js#port-blacklists)，了解您为什么要将其设置为`ftp`
*   端口连接`timeout`(默认`1000`毫秒)

```
import NetMap from 'netmap.js'

const netmap = new NetMap({
  protocol: 'http',
  timeout: 3000
})
```

`**pingSweep()**`

`pingSweep()`方法确定给定的主机阵列是否是活动的。它通过检查到端口的连接是否超时来实现这一点，在这种情况下，主机被视为离线(参见[“Ping”扫描](https://github.com/serain/netmap.js#ping-sweep)了解限制，以及[标准情况](https://github.com/serain/netmap.js#standard-case)了解理论)。

该方法采用以下参数:

*   `hosts`要扫描的主机阵列(IP 地址或主机名)
*   `options`对象有:
    *   `maxConnections`-最大并发连接数(默认情况下，Chrome 上的`10`和其他浏览器上的`17`-浏览器支持的最大并发连接数)
    *   要扫描的`port`(默认`45000`)

它回报一个承诺。

```
netmap.pingSweep(['192.168.1.1'], {
  maxConnections: 5,
  port: 80
}).then(results => {
  console.log(results)
})
```

`**tcpScan()**`

`tcpScan()`方法将对一系列目标执行端口扫描。阅读[标准案例](https://github.com/serain/netmap.js#standard-case)来理解它是如何做到这一点的。

该方法采用以下参数:

*   `hosts`要扫描的主机阵列(IP 地址或主机名)
*   `ports`要扫描的端口列表(1-65535 之间的整数，避开[黑名单](https://github.com/serain/netmap.js#port-blacklists)中的端口)
*   `options`对象有:
    *   `maxConnections`–最大并发连接数(默认情况下`6`–每个域浏览器允许的最大连接数)
    *   `portCallback`–当单个`host:port`组合完成扫描时执行的回调
    *   `controlPort`–扫描端口以确定基线关闭端口增量(默认`45000`)
    *   `controlRatio`–与被认为关闭的端口的控制增量的相似度，以百分比表示(默认`0.8`，参见[示例](https://github.com/serain/netmap.js#scan-tcp-ports)

它回报一个承诺。

```
netmap.tcpScan(['192.168.1.1'], [80, 27017], {
  maxConnections: 5,
  portCallback: result => {
    console.log(result)
  },
  controlPort: 45000,
  controlRatio: 0.8
}).then(results => {
  console.log(results)
})
```

检查[示例](https://github.com/serain/netmap.js#tcp-port-scan)以解释输出。

**理论**

本节简要介绍模块发现技术背后的理论。

**大意**

这个模块使用`Image`对象来尝试请求跨源资源(测试中的一系列`http://{host}:{port}`URL)。浏览器引发错误所花费的时间(T2)，或者在某个超时值之后没有错误，提供了对所审查的主机和端口状态的洞察。

**标准案例**

当试图连接到一个关闭的端口时，一个活的主机通常会*相对快速地响应一个 TCP `RST`包。*

 *如果端口是打开的，即使它没有运行 HTTP 服务器，由于建立完整的 TCP 连接，然后意识到它不能从提供的 URL 获取图像的开销，浏览器将花费更长的时间来产生错误。

离线主机自然不会用`RST`来响应，也不会允许建立完整的 TCP 连接。在超时之前(大约 90 秒)，浏览器仍然会尝试建立一段时间的连接。`netmap.js`默认等待 1000 毫秒后会超时。

总而言之:

*   实时主机上关闭的端口会有一个非常短的`delta`
*   活动主机上的开放端口将有一个稍长的`delta`
*   离线主机或未使用的 IP 地址将超时

标准情况由主机`192.168.1.1`在 [TCP 端口扫描](https://github.com/serain/netmap.js#tcp-port-scan)示例中说明。

**无 TCP `RST`案例**

一些主机(如`google.co.uk`或 Windows 主机)和一些网络设置(如 VirtualBox 主机专用网络)在遇到关闭的端口时不会返回 TCP `RST`数据包。

在这些情况下，关闭的端口通常会超时，而打开的端口会很快引发错误。

因此，当`RST`包没有被返回时，`pingSweep()`方法的实现是不可靠的。

总之，当 TCP `RST`数据包由于某种原因没有返回时:

*   活动主机上关闭的端口将超时
*   实时主机上的开放端口将有一个短的`delta`
*   `pingSweep()`无法区分关闭的端口超时和“死”主机超时

在 [TCP 端口扫描](https://github.com/serain/netmap.js#tcp-port-scan)示例中，主机`192.168.99.100`和`google.co.uk`说明了这种特殊情况。

**忽略 WebSockets 和 AJAX**

有充分的证据表明，您也应该能够使用 WebSockets 和 AJAX 来映射网络。

我试了一下(还调整了 BeEF，只使用 WebSockets 和 AJAX 尝试了它的`port_scanner`模块)；我发现这两种方法产生的结果完全不可靠。

请让我知道我是否在这方面遗漏了什么。

[**Download**](https://github.com/serain/netmap.js)*