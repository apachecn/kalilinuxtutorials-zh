# Web-Hacking-Toolkit:一个支持图形用户界面(GUI)的多平台 Web Hacking Toolkit Docker Image

> 原文：<https://kalilinuxtutorials.com/web-hacking-toolkit/>

[![](img/79230b13a95b677279147530d78357bf.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh6yeAP2zyH5gEgCKE74mPPDL18PSM8u6YYL3d9yHm2ujaC92jUgfa9x8icUL8v2YYf20R2Pbd10MRFsZroQlug5Wo1IItNQJfcsACnD0BF68mHyF7sje_Ee8qLpHzjE951x16KitvNRKgn0JCSjnECutZtLFOsBupI0E2-4Ewxo8F1t5Y0eyDFCfUr=s784)

**Web-Hacking-Toolkit** 支持图形用户界面(GUI)的多平台 web hacking toolkit Docker 图像。

**安装**

**码头工人**

从 Docker Hub 提取图像:

```
docker pull signedsecurity/web-hacking-toolkit

```

运行容器并附加外壳:

```
docker run \
	-it \
	--rm \
	--shm-size="2g" \
	--name web-hacking-toolkit \
	--hostname web-hacking-toolkit \
	-p 22:22 \
	-v $(pwd)/data:/root/data \
	signedsecurity/web-hacking-toolkit \
	/bin/bash
```

**坞站组成**

也可以使用 Docker-Compose。

```
version: "3.9"
 services:
    web-hacking-toolkit:
        image: signedsecurity/web-hacking-toolkit
        container_name: web-hacking-toolkit
        hostname: web-hacking-toolkit
        stdin_open: true
        shm_size: 2gb
        ports:
            - "22:22" # exposed for GUI support sing SSH with X11 forwarding
        volumes:
            - ./data:/root/data
        restart: unless-stopped
```

构建并运行容器:

```
docker-compose up
```

附加外壳:

```
docker-compose exec web-hacking-toolkit /bin/bash
```

**从源代码构建**

克隆此存储库并构建映像:

```
git clone https://github.com/signedsecurity/web-hacking-toolkit.git && \
cd web-hacking-toolkit && \
make build-images
```

运行容器并附加外壳:

```
make run
```

**GUI 支持**

默认情况下，没有 GUI 工具可以在 Docker 容器中运行，因为没有 X11 服务器可用。要运行它们，您必须改变这种情况。这样做需要什么取决于您的主机。如果您:

*   在 Linux 上运行，你可能有 X11
*   在 Mac OS 上运行，需要 Xquartz ( `**brew install Xquartz**`)
*   在 Windows 上运行，你有一个问题

**使用 SSH 配合 X11 转发**

如果您想这样做，可以通过 SSH 使用 X11 转发。在容器内部运行`**start_ssh**`来启动服务器，确保在启动容器时公开端口 22:`**docker run -p 127.0.0.1:22:22 ...**`，然后在连接时使用`**ssh -X ...**`(脚本打印密码)。

**已安装**

**工具**

| 种类 | 名字 | 描述 |
| --- | --- | --- |
| 发现/域 | 积累 | 深入的攻击面映射和资产发现 |
| 实用程序/任何 | 再 | 一个向文件添加新行、跳过重复行的工具 |
| 发现/参数 | 阿尔俊 | HTTP 参数发现套件。 |
| 军刀/代理 | 打嗝套件社区 | BurpSuite 项目社区版。 |
| 实用程序/HTTP | 卷曲 | 一个命令行工具和库，用于使用 URL 语法传输数据，支持 HTTP、HTTPS、FTP、FTPS、GOPHER、TFTP、SCP、SFTP、SMB、TELNET、DICT、LDAP、LDAPS、MQTT、FILE、IMAP、SMTP、POP3、RTSP 和 RTMP。libcurl 提供了无数强大的特性 |
| 发现/DNS | dnsx | dnsx 是一个快速和多用途的 DNS 工具包，允许运行多个您选择的 DNS 查询与用户提供的解析器列表。 |
| 发现/模糊 | ffuf | 用 Go 编写的快速 web fuzzer |
| 发现/域 | find domain | 最快的 |
| 浏览器 | 火狐浏览器 | 来自 Mozilla 的安全简单的网络浏览器 |
| 实用工具/镜头 | 身材高挑 | mag gowitness——一个使用 Chrome Headless 的网页截图工具 |
| 混杂的 | html 工具 | 获取 stdin 上 HTML 文档的 URL 或文件名，并提取标记内容、属性值或注释 |
| 实用程序/HTTP | httpx | httpx 是一个快速和多用途的 HTTP 工具包，允许使用 retryablehttp 库运行多个探测器，它旨在通过增加线程来保持结果的可靠性。 |
| 发现/端口 | masscan | TCP 端口扫描器，异步发送 SYN 数据包，在 5 分钟内扫描整个互联网。 |
| 发现/端口 | 纳阿布 | 一个用 go 编写的快速端口扫描器，注重可靠性和简单性。旨在与其他工具结合使用，用于在漏洞奖励和测试中发现攻击面 |
| 发现/端口 | nmap | 网络映射器。SVN 官方知识库的 Github 镜像。 |
| 军刀/扫描仪 | 核心 | Nuclei 是基于模板的可配置目标扫描的快速工具，提供了巨大的可扩展性和易用性。 |
| 发现/端口 | ps.sh | 用于端口扫描的工具包装(nmap、naabu 和 masscan)，目标是减少扫描时间、提高扫描效率和自动化工作流程。 |
| 发现/域 | sigsubfind3r | 一个子域发现工具——它使用各种在线资源被动地收集一个子域列表。 |
| 发现/URL | sigurlfind3r | 已知网址发现的被动侦察工具-它使用各种在线资源被动收集网址列表。 |
| 军刀/扫描仪 | sigurlscann3r | 一个 web 应用攻击面映射工具。它接受一个 URL 列表，然后执行大量的探测 |
| 发现/域 | subdomains.sh | 一个用于子域收集工具(amass，subfinder，findomain & sigsubfind3r)的包装器，用于提高收集效率和自动化工作流。 |
| 发现/域 | 子 finder | Subfinder 是一个子域发现工具，为网站发现有效的子域。设计为一个被动的框架，对 bug 奖励有用，对渗透测试安全。 |
| 公用事业/终端 | tmux | tmux 是一个终端多路复用器:它允许在一个屏幕上创建、访问和控制多个终端。tmux 可以从屏幕上分离，并继续在后台运行，然后再重新连接 |
| 实用程序/编辑器 | 精力 | 一个高度可配置的文本编辑器，可以非常高效地创建和更改任何类型的文本。 |
| 发现/技术 | 瓦帕里斯 | Wappalyzer 识别网站上的技术，如 CMS、web 框架、电子商务平台、JavaScript 库、分析工具等等。 |
| 实用程序/HTTP | wuzz | 用于 HTTP 检查的交互式 cli 工具 |

**词表**

| Wordlist | 描述 |
| --- | --- |
| 秘书 | SecLists 是安全测试人员的伴侣。它是安全评估期间使用的多种类型列表的集合，集中在一个位置。列表类型包括用户名、密码、URL、敏感数据模式、模糊负载、web 外壳等等。 |
| jhadix/content _ discovery _ all . txt | 内容发现 URL 和文件的主列表(最常用于 gobuster) |

[**Download**](https://github.com/signedsecurity/web-hacking-toolkit)