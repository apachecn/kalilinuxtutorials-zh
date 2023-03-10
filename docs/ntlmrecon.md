# NTLMRecon:从启用 NTLM 身份验证的 Web 端点枚举信息的工具

> 原文：<https://kalilinuxtutorials.com/ntlmrecon/>

[![NTLMRecon : Tool To Enumerate Information From NTLM Authentication Enabled Web Endpoints](img/ca57415916b83d5d312c07efa2834032.png "NTLMRecon : Tool To Enumerate Information From NTLM Authentication Enabled Web Endpoints")](https://1.bp.blogspot.com/-0sZOYAACaQE/XmaZMwcYczI/AAAAAAAAFWw/TDxYsGnPwy80oeV2f2NFKdlbjygUAGkGgCLcBGAsYHQ/s1600/NTML%25281%2529.png)

NTLMRecon 在构建时就考虑到了灵活性。一个快速灵活的 NTLM 侦察工具，无需外部依赖。在处理大量潜在的 IP 地址和域时，查找有关 NTLM 端点的信息非常有用。

需要运行一个单一的网址，一个 IP 地址，整个 CIDR 范围或所有这些都放在一个单一的输入文件的组合侦察？没问题！它掩护了你。

**演示**

[![](img/bdc045d4569c46500cda97921890aa9a.png)](https://asciinema.org/a/e4ggPBbzpJj9cIWRwK67D8xnw)

**概述**

它查找启用了 NTLM 的 web 端点，发送一个假的身份验证请求，并从 NTLMSSP 响应中枚举以下信息:

*   AD 域名
*   服务器名称
*   DNS 域名
*   正式域名(Fully Qualified Domain Name)
*   父 DNS 域

由于它利用了 NTLMSSP 的 python 实现，因此消除了每次成功发现时运行 Nmap NSE `http-ntlm-info`的开销。每次成功发现启用了 NTLM 的 web 端点时，该工具都会枚举有关域的信息并将其保存到 CSV 文件中，如下所示:

| 统一资源定位器 | 域名 | 服务器名称 | DNS 域名 | 正式域名(Fully Qualified Domain Name) | DNS 域 |
| --- | --- | --- | --- | --- | --- |
| [https://contoso.com/EWS/](https://contoso.com/EWS/) | XCORP | EXCHANGE01 | xcorp.contoso.net | EXCHANGE01.xcorp.contoso.net | contoso.net |

**安装**

**拱门**

如果你使用的是 Arch linux 或者任何基于 Arch Linux 的发行版，你可以从 [AUR](https://aur.archlinux.org/packages/ntlmrecon/) 获得最新版本

**通用安装**

*   克隆存储库—`**git clone https://github.com/sachinkamath/ntlmrecon/**`
*   推荐–安装 virtualenv `**pip install virtualenv**`
*   启动一个新的虚拟环境—`**virtualenv venv**`并用`**source venv/bin/activate**`激活它
*   运行设置文件-`**python setup.py install**`
*   运行 NTLM recon–`**ntlmrecon --help**`

**也可理解为-[特权检查:用于 Windows](https://kalilinuxtutorials.com/privesccheck/)T3 的特权提升枚举脚本**

**用途**

**用法:**NTLM recon[-h][–INPUT INPUT |–INFILE INFILE][–WORDLIST WORDLIST]
[–THREADS][–output-type]–OUTFILE OUTFILE
[–random-user-agent][–force-all][–shuffle][-f][-f]
**可选参数:**
-h，–help 显示此帮助消息并退出
–INPUT 输入传递输入作为 IP 地址、URL 或 CIDR 来枚举
NTLM 端点支持 JSON (TODO)和 CSV
(默认值:CSV)
–OUTFILE OUTFILE 设置输出文件名(默认值:ntlmrecon . CSV)
–random-user-agent TODO:发送请求时随机化用户代理
(默认值:False)
–Force-all 即使找到 URL 的有效端点
(默认值:False)
–打乱输入文件的顺序
-f，–强制替换文件

**示例用法**

*   **侦察单个网址**

**$ NTLM recon–输入 https://mail.contoso.com–输出 ntlmrecon.csv**

*   **侦察 CIDR 范围或 IP 地址**

**$ NTLM recon–输入 192 . 168 . 1 . 1/24–输出 ntlmrecon-ranges.csv**

*   **检查输入文件**

NTLM 侦察自动检测每行的输入类型，并自动给你结果。即使从文本文件中读取，CIDR 范围也会自动扩展。

输入文件可能像下面这样混乱:

mail.contoso.com 10 . 0 . 13 . 2/28
192 . 168 . 222 . 1/24
https://mail.contoso.com

要使用输入文件运行 recon，只需运行:

**$ NTLM recon–infile/path/to/input/file–outfile NTLM recon-from file . CSV**

[**Download**](https://github.com/sachinkamath/ntlmrecon/)