# RomBuster:一个允许泄露网络路由器管理员密码的路由器利用工具

> 原文：<https://kalilinuxtutorials.com/rombuster/>

[![RomBuster : A Router Exploitation Tool That Allows To Disclosure Network Router Admin Password](img/2b9e0b82dd5f2bec13692e3c35bec940.png "RomBuster : A Router Exploitation Tool That Allows To Disclosure Network Router Admin Password")](https://1.bp.blogspot.com/-PPxjXw-KVwU/YN7ovkXAfcI/AAAAAAAAJyY/208H4-PBEL4giR5f4wc97g99CW0B7VQ3gCLcBGAsYHQ/s728/RomBuster.png)

RomBuster 是一个路由器利用工具，允许泄露网络路由器管理员密码。

**特性**

*   利用最流行的路由器中的漏洞，如`D-Link`、`Zyxel`、`TP-Link`和`Huawei`。
*   经过优化，可同时利用列表中的多个路由器。
*   简单的 CLI 和 API 用法。

**安装**

**pip3 安装 git+https://github . com/enty sec/RomBuster**

**基本用法**

要使用 RomBuster，只需在终端中输入 **`rombuster`** 。

**用法:RomBuster[-h][-o OUTPUT][-I INPUT][-a ADDRESS][–shod an shod an]
[–zoo meye zoo meye][-p PAGES]
RomBuster 是一款路由器利用工具，允许泄露网络
路由器管理员密码。
可选参数:
-h，–help 显示此帮助信息并退出
-o OUTPUT，–OUTPUT OUTPUT
将结果输出到文件。
-i 输入，–INPUT 输入
输入文件的地址。
-一个地址，–地址地址
单个地址。
–SHODAN SHODAN SHODAN API 密钥，用于通过互联网利用设备。
–zoo meye zoo meye zoo meye 用于通过互联网利用设备的 API 密钥。
-p PAGES，–PAGES PAGES
你想从 ZoomEye 获取的页数。**

**例题**

**利用单路由器**

让我们黑我的路由器，只是为了好玩。

192.168.99.1

**利用互联网上的路由器**

让我们尝试使用 Shodan 搜索引擎来开发互联网上的路由器。

**分手——shodan PSK t1 gyxggecyz 2191 h2jos 9 qvgd**

**注:**给出的 Shodan API key ( `PSKINdQe1GyxGgecYz2191H2JoS9qvgD`)是我的 PRO API key，你可以使用这个 key 或者你自己的，可以自由使用我们所有的资源免费。

**从输入文件中利用路由器**

让我们试着使用开放的路由器数据库。

**rombuster-I routers . txt-o passwords . txt**

**注意:**会根据地址利用`**routers.txt**`列表中的所有路由器，并将获得的所有密码保存到 **`passwords.txt`。**

**API 使用**

RomBuster 也有自己的 Python API，可以通过将 RomBuster 导入到您的代码中来调用。

**从 rombuster 导入 RomBuster**

**基本功能**

有所有 RomBuster 的基本功能，可以用来利用特定的路由器。

`**exploit(address)**`–通过给定地址利用单个路由器。

**例题**

**利用单路由器**

**从 rombuster 导入 RomBuster
RomBuster = RomBuster()
creds = RomBuster . exploit(' 192 . 168 . 99 . 100 ')
print(creds)**

[**Download**](https://github.com/EntySec/RomBuster#features)