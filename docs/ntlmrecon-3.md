# NTLMRecon:枚举启用 NTLM 身份验证的 Web 端点的信息

> 原文：<https://kalilinuxtutorials.com/ntlmrecon-3/>

[![](img/198d7be9d767e138a4417ecb5fd108e0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjAgsabunD0W6oikwB0166NbG2H_2ql3CrIpjHjMOZoViiCBTFEobqegd6nc6-iBkHqT2RhyRbXd4-n4HtTDKJKS410QDqujgzf3iagQSdoBCz5P2aTE7AtcmzgI1VfAQt2sZrOlPayw3MOZMUMJpkpqEdEvO_lg-zDIPpK93AMkweJjkjVGzal-VVk/s728/NTML(1)%20(1).png)

NTLMRecon 是一款快速灵活的 NTLM 侦察工具，无需外部依赖。在处理大量潜在的 IP 地址和域时，查找有关 NTLM 端点的信息非常有用。

NTLMRecon 的构建考虑到了灵活性。需要运行一个单一的网址，一个 IP 地址，整个 CIDR 范围或所有这些都放在一个单一的输入文件的组合侦察？没问题！NTLMRecon 掩护你。请继续阅读。

NTLMRecon 查找启用了 NTLM 的 web 端点，发送一个假的身份验证请求，并从 NTLMSSP 响应中枚举以下信息:

*   AD 域名
*   服务器名称
*   DNS 域名
*   正式域名(Fully Qualified Domain Name)
*   父 DNS 域

由于 NTLMRecon 利用了 NTLMSSP 的 python 实现，它消除了为每次成功发现运行 Nmap NSE `**http-ntlm-info**`的开销。

每次成功发现启用了 NTLM 的 web 端点时，该工具都会枚举有关域的信息并将其保存到 CSV 文件中，如下所示:

| 统一资源定位器 | 域名 | 服务器名称 | DNS 域名 | 正式域名(Fully Qualified Domain Name) | DNS 域 |
| --- | --- | --- | --- | --- | --- |
| https://contoso.com/EWS/ | XCORP | EXCHANGE01 | xcorp.contoso.net | EXCHANGE01.xcorp.contoso.net | contoso.net |

# 装置

### 黑弓

NTLMRecon 已经为 BlackArch 打包，可以通过运行`**pacman -S ntlmrecon**`来安装

### 拱门

如果您使用的是 Arch linux 或任何基于 Arch Linux 的发行版，您可以从 Arch 用户存储库中获取最新的构建版本。

### 从源代码构建

*   克隆存储库:`**git clone https://github.com/pwnfoo/ntlmrecon/**`
*   推荐–安装虚拟设备
*   启动一个新的虚拟环境:`**virtualenv venv**`并用`**source venv/bin/activate**`激活它
*   运行安装文件:`**python setup.py install**`
*   运行 ntlmrecon : `**ntlmrecon --help**`

# 用法

**$ ntlmrecon–help
_ _*_* *| \ |*|*| | \/|*\
| | | | | | |。。|| | */ /* _
|。`| | | | | | | \/| | |/_ \/_ | ' _ \ | | | | |*| | | | | | \ \/(|()| | | | _ | _/_/_*/_ |*/_ | ^ _ ^ _ ^ _ ^ _ ^*| _ _ _ _ _ _/*| |*| ^-@ pwn foo
v . 0.4 beta–你们还在暴露 NTLM 端点吗？
Bug 报告，特性请求:https://git.io/JIR5z
用法:NTLM recon[-h][–INPUT INPUT |–INFILE INFILE][–WORDLIST WORDLIST]
[–THREADS][–output-type][–OUTFILE OUTFILE]
[–random-user-agent][–force-all][–shuffle][–f]
可选参数:
-h，–help 显示此帮助消息并退出
–INPUT INPUT，-i INPUT
PassJSON (TODO)和 CSV 支持的
(默认:CSV)
–OUTFILE OUTFILE，-O OUTFILE
设置输出文件名(默认:ntlmrecon . CSV)
–random-user-agent TODO:发送请求时随机化用户代理
(默认:False)
–Force-all 即使找到 URL 的有效端点
(默认:False)
–打乱输入文件的顺序
-f**

## 用法示例

### 侦察单个网址

`**$ ntlmrecon --input https://mail.contoso.com --outfile ntlmrecon.csv**`

### 侦察 CIDR 范围或 IP 地址

`**$ ntlmrecon --input 192.168.1.1/24 --outfile ntlmrecon-ranges.csv**`

### 对输入文件进行侦察

该工具自动检测每行的输入类型，并采取相应的措施。默认情况下，CIDR 范围是扩展的(请注意，目前还没有加入重复数据消除功能！)

输入文件可能像下面这样混乱:

**mail.contoso.com
CONTOSOHOSTNAME
10 . 0 . 13 . 2/28
192 . 168 . 222 . 1/24
https://mail.contoso.com**

要使用输入文件运行 recon，只需运行:

**$ NTLM recon–infile/path/to/input/file–outfile NTLM recon-from file . CSV**

[**Download**](https://github.com/pwnfoo/NTLMRecon)