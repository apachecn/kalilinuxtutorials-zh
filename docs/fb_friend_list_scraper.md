# Fb_Friend_List_Scraper:一个从大型好友列表中抓取名字和用户名的工具

> 原文：<https://kalilinuxtutorials.com/fb_friend_list_scraper/>

[![](img/f7341c4aa9eb207df6d85ff8937d8ded.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhEVzs4bSUX8Yhev5_RA1WqXKXFkkCGndY2P3_lOCXltfUmJYvhaLa7qNQDrb2XCqHnmQbv88JT2dYo3WtupjvYf1E9ttSA1s6pAOORT5GxxL9uArxDuG5HiUU4cKAkSOx_J7Dyp1r-bOHWJ-lBErKx2uzbn5bT7gI9d7MA8GnQ2q1TB96Q2b-3UDzt/s728/168868887-0af568d1-fb99-409e-89c6-a779cd74924c%20(1).png)

Fb_Friend_List_Scraper 是一款从脸书的大型好友列表中抓取名字和用户名的工具，没有费率限制。

### 开始使用

*   使用 pip 安装:`**python -m pip install fb-friend-list-scraper**`
*   脚本现在安装为`**fbfriendlistscraper**`
*   使用`**-h**`或`**--help**`运行以显示使用信息。

### 用法

**用法:fbfriendlist scraper[-h]-e EMAIL[-p PASSWORD]-u USERNAME[-o OUTFILE][-w][-q][-s sleep multiplier][-I PROXY][-c CMD]
从脸书上的大型好友列表中抓取姓名和用户名的工具，不受速率限制
选项:
-h，–帮助显示此帮助消息并退出
-e EMAIL，–EMAIL
用于登录的电子邮件地址或电话号码。
-p PASSWORD，–PASSWORD PASSWORD
登录使用的密码。如果没有提供，将会提示您。出于安全原因，您真的不应该使用它。
-u 用户名，–用户名用户名
要抓取的用户的用户名。
-o OUTFILE，–OUTFILE OUTFILE
输出文件的路径。(默认值:。/screwed _ friends . txt)
-w，–在无头模式下无头运行 webdriver。
-q，–安静不要将刮蹭的用户打印到屏幕上。
-x，–Only 用户名只有用户名/id 会被写入输出文件。
-s SLEEPMULTIPLIER，–sleep multiplier sleep multiplier
将每一页之间的睡眠时间乘以 n。当很容易受到速率限制时很有用。
-i PROXY，–PROXY PROXY
用于连接的代理服务器。用户名/密码可以像这样提供:socks 5://user:pass @ host:port
-c CMD，–CMD CMD Shell 命令在每次抓取页面后运行。用于更改代理/VPN 出口。
例子:
fbfriendlistrigger-e your@email.com-p your password 123-u some username . 123-o my _ file . txt
fbfriendlistrigger-email your@email.com-username another . user-headless-S2-x
fbfriendlistrigger-e your@email.com-u username . Johnson-w-proxy socks 5://127 . 0 . 0 . 1:9050
fbfriendlistrigger-e your@email.com-u xxuserxx-headless–cmd " mull**

[Download](https://github.com/narkopolo/fb_friend_list_scraper)