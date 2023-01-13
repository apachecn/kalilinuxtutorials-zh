# Twitter shadow ban v2:Twitter shadow ban 测试

> 原文：<https://kalilinuxtutorials.com/twittershadowbanv2/>

[![TwitterShadowBanV2 : Twitter Shadowban Tests](img/f801200f86794f4396c9847e219da105.png "TwitterShadowBanV2 : Twitter Shadowban Tests")](https://1.bp.blogspot.com/-jHxbKSZE27Q/XRlSxm1efqI/AAAAAAAABJ0/SapdnU3dy-AkvnSeX5bQHw9Qck83ECMNQCLcBGAs/s1600/twitter.png)

TwitterShadowBanV2 是一款单页网络应用，测试 Twitter 用户的传统和 QFD 影子银行。浏览器兼容性需要移植。没什么特别的，只是普通的巴别塔魔法。

**git 克隆 https://github.com/shadowban-eu/TwitterShadowBanV2&CD twittershadowbanv 2 NPM 安装**

因为我们使用 php 后端进行请求代理，所以您也需要 PHP。gulp 脚本使用 php-cli 的 web 服务器。

Debian

**apt-get 安装 php7.2-cli**

最后，使用`default` gulp 任务启动 PHP-CLI web 服务器，并观察文件变化。

**也可阅读-[Ponce:IDA Pro 插件，为用户提供执行污点分析的能力&符号执行](https://kalilinuxtutorials.com/ponce-ida-pro-plugin/)**

**npm 开始**

**部署**

跑`npm start build`！这会创建一个丑陋的脚本包，并使用第三方脚本的缩小版本。然后把`dist/`的内容复制到你的 server_root。

**杂项**

检查正在运行的服务器(当然，PID 不同)

**pgrep PHP-f
>20748 PHP-s localhost:8080-t。/dist/**

如果您需要在另一个端口上运行 php-cli webserver，您必须在第 72 行左右的`gulpfile.babel.js`中手动更改它。

**const args = ['-S '，' localhost:8080 '，'-t '，'。/距离/']；**

[**Download**](https://github.com/shadowban-eu/TwitterShadowBanV2)