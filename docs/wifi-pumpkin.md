# WiFi-南瓜-流氓 Wi-Fi 接入点攻击的框架

> 原文：<https://kalilinuxtutorials.com/wifi-pumpkin/>

WiFi-Pumpkin 是一个评估 Wi-Fi 安全性的非常全面的系统。最基本的特征是制造假 AP 和制造中路进攻的能力，然而概要是非常膨胀的。

![](img/8d2633716f69432c7c9a552290df3622.png)

## **也读作[Androl4b——安卓安全虚拟机](http://kalilinuxtutorials.com/androl4b-2/)**

## **安装 WiFi-南瓜**

*   Python 2.7

```
 git clone https://github.com/P0cL4bs/WiFi-Pumpkin.git
 cd WiFi-Pumpkin
 ./installer.sh --install
```

或者下载[。要安装的 deb](https://github.com/P0cL4bs/WiFi-Pumpkin/releases) 文件

```
sudo dpkg -i wifi-pumpkin-0.8.5-all.deb
sudo apt-get -f install # force install dependencies if not install normally

```

## **特色 WiFi——南瓜**

*   流氓 Wi-Fi 接入点
*   拒绝攻击客户端 AP
*   探测请求监视器
*   DHCP 饥饿攻击
*   凭据监视器
*   透明代理
*   Windows Update 攻击
*   网络钓鱼管理器
*   部分旁路 HSTS 协议
*   支撑牛肉钩
*   ARP 病毒
*   DNS 欺骗
*   通过 MITM 修补二进制文件
*   业力攻击(支持 hostapd-法力)
*   NBT LLMNR-NS 和 MDNS 投毒者(响应者)
*   pumpkin-Proxy(Proxy server(mitm Proxy API))
*   动态捕捉图像
*   TCP 代理(带 scapy)

## **外挂**

| 插件 | 描述 |
| :-- | :-- |
| [Dns2proxy](https://github.com/LeonardoNve/dns2proxy) | 一旦您将 DNS 服务器更改为受害者，此工具将提供不同的后解释功能。 |
| [Sstrip2](https://github.com/LeonardoNve/sslstrip2) | Sslstrip 是一个 MITM 工具，实现了莫邪马林斯派克的基于版本 fork @LeonardoNve/@xtr4nge 的 SSL 剥离攻击。 |
| [塞尔吉奥 _ 代理人](https://github.com/supernothing/sergio-proxy) | Sergio Proxy(一个收集输入和输出的超级有效的记录器)是一个 HTTP 代理，它是用 Python 为 Twisted 框架编写的。 |
| [BDFProxy](https://github.com/davinerd/BDFProxy-ng) | 通过 MITM 修补二进制文件:BackdoorFactory + mitmProxy，bdfproxy-ng 是对原 BDFProxy @secretsquirrel 的一个分叉和回顾。 |
| [应答者](https://github.com/lgandx/Responder) | 响应者 LLMNR，NBT 和 MDNS 投毒者。作者:洛朗·加菲 |

## **透明代理**

![](img/c67a3d76b0775d81c78255679e12af5b.png)

透明代理(mitmproxy ),可以用来阻止和控制改变请求和响应的 HTTP 流量，允许将 javascripts 注入到经过的目标中。你可以毫不费力地实现一个模块，将信息注入页面，在目录中制作一个 python 文档“modules/expansion/”自然会被记录在 Pumpkin-Proxy 选项卡上。

#### **插件示例开发**

```
from mitmproxy.models import decoded # for decode content html
from plugins.extension.plugin import PluginTemplate

class Nameplugin(PluginTemplate):
   meta = {
       'Name'      : 'Nameplugin',
       'Version'   : '1.0',
       'Description' : 'Brief description of the new plugin',
       'Author'    : 'by dev'
   }
   def __init__(self):
       for key,value in self.meta.items():
           self.__dict__[key] = value
       # if you want set arguments check refer wiki more info. 
       self.ConfigParser = False # No require arguments 

   def request(self, flow):
       print flow.__dict__
       print flow.request.__dict__ 
       print flow.request.headers.__dict__ # request headers
       host = flow.request.pretty_host # get domain on the fly requests 
       versionH = flow.request.http_version # get http version 

       # get redirect domains example
       # pretty_host takes the "Host" header of the request into account,
       if flow.request.pretty_host == "example.org":
           flow.request.host = "mitmproxy.org"

       # get all request Header example 
       self.send_output.emit("\n[{}][HTTP REQUEST HEADERS]".format(self.Name))
       for name, valur in flow.request.headers.iteritems():
           self.send_output.emit('{}: {}'.format(name,valur))

       print flow.request.method # show method request 
       # the model printer data
       self.send_output.emit('[NamePlugin]:: this is model for save data logging')

   def response(self, flow):
       print flow.__dict__
       print flow.response.__dict__
       print flow.response.headers.__dict__ #convert headers for python dict
       print flow.response.headers['Content-Type'] # get content type

       #every HTTP response before it is returned to the client
       with decoded(flow.response):
           print flow.response.content # content html
           flow.response.content.replace('</body>','<h1>injected</h1></body>') # replace content tag 

       del flow.response.headers["X-XSS-Protection"] # remove protection Header

       flow.response.headers["newheader"] = "foo" # adds a new header
       #and the new header will be added to all responses passing through the proxy
```

#### **TCP-代理服务器**

可以放在 TCP 流中的代理。它通过(scapy 模块)引导需求和反应流，并有效地调整被 WiFi-Pumpkin 阻塞的 TCP 协议包。此模块利用模块来查看或调整被阻止的信息，这些信息可能对模块的执行要求最低，只需包括您的自定义模块“模块/分析器/”即可，因此将被记录在 TCP-Proxy 选项卡上。

```
from scapy.all import *
from scapy_http import http # for layer HTTP
from default import PSniffer # base plugin class

class ExamplePlugin(PSniffer):
    _activated     = False
    _instance      = None
    meta = {
        'Name'      : 'Example',
        'Version'   : '1.0',
        'Description' : 'Brief description of the new plugin',
        'Author'    : 'your name',
    }
    def __init__(self):
        for key,value in self.meta.items():
            self.__dict__[key] = value

    @staticmethod
    def getInstance():
        if ExamplePlugin._instance is None:
            ExamplePlugin._instance = ExamplePlugin()
        return ExamplePlugin._instance

    def filterPackets(self,pkt): # (pkt) object in order to modify the data on the fly
        if pkt.haslayer(http.HTTPRequest): # filter only http request 

            http_layer = pkt.getlayer(http.HTTPRequest) # get http fields as dict type
            ip_layer = pkt.getlayer(IP)# get ip headers fields as dict type

            print http_layer.fields['Method'] # show method http request
            # show all item in Header request http
            for item in http_layer.fields['Headers']:
                print('{} : {}'.format(item,http_layer.fields['Headers'][item]))

            print ip_layer.fields['src'] # show source ip address 
            print ip_layer.fields['dst'] # show destiny ip address 

            print http_layer # show item type dict
            print ip_layer # show item type dict

            return self.output.emit({'name_module':'send output to tab TCP-Proxy'})
```

[![https://github.com/h2non/toxy](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/P0cL4bs/WiFi-Pumpkin)