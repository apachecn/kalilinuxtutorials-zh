# ARDT : Akamai 反射式 DDoS 工具

> 原文：<https://kalilinuxtutorials.com/ardt-akamai-reflective-ddos-tool/>

攻击 Akamai 边缘主机背后的原始主机，绕过 Akamai 服务提供的 DDoS 保护。

**工作原理**

基于在 [NCC](https://dl.packetstormsecurity.net/papers/attack/the_pentesters_guide_to_akamai.pdf) 完成的研究

Akamai 在世界各地拥有大约 100，000 个边缘节点，这些节点提供负载平衡、web 应用程序防火墙、缓存等功能，以确保最少量的请求实际上到达受保护的原始 web 服务器。

然而，缓存的问题是你不能缓存不确定的东西，比如搜索结果。之前没有被请求的搜索可能不在高速缓存中，并且将导致高速缓存未命中，并且 Akamai 边缘节点从源服务器本身请求资源。

**亦读-**[**m 提取:内存提取器&分析器 2019**](https://kalilinuxtutorials.com/mxtract-memory-extractor-analyzer/)

该工具的作用是，在提供 Akamai 边缘节点列表和有效缓存缺失请求的情况下，产生多个请求，这些请求通过 Akamai 边缘节点到达源服务器。

可以想象，如果您控制着 50 个 IP 地址，以每秒大约 20 个的速度发送请求，有 100，000 个 Akamai 边缘节点列表，一个请求导致 10KB 的流量到达源服务器，如果我的计算正确，大约 976MB/ps 的流量到达源服务器，这是一个巨大的流量。

**寻找 Akamai 边缘节点**

为了查找 Akamai 边缘节点，包含了以下脚本:

**python ardt _ aka mai _ edge node _ finder . py**

这可以很容易地编辑，以找到更多，然后它会自动保存 IP。

[**Download**](https://github.com/m57/ARDT)