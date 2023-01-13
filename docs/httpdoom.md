# HttpDoom:基于响应的网站检查工具

> 原文：<https://kalilinuxtutorials.com/httpdoom/>

[![HttpDoom : A Tool For Response-Based Inspection Of Websites](img/96ac21aff352f1dcf87b3bc09538ed83.png "HttpDoom : A Tool For Response-Based Inspection Of Websites")](https://1.bp.blogspot.com/-Dp5qJkzasqQ/YINNQ1EqAEI/AAAAAAAAI04/7ArHN9Y6kZsG4OLgtY6CiBhW6Cn5SmmywCLcBGAsYHQ/s728/HttpDoom%25281%2529.png)

HttpDoom 是一种以非常快的方式验证大型基于 HTTP 的攻击面的工具。深受 [Aquatone](https://github.com/michenriksen/aquatone) 的启发。

**为什么？**

当我利用 Aquatone 跳过一些主机时，由于截图功能，我遇到了一些性能问题，并且缺乏扩展功能，如用类似插件的系统验证前端技术，此外，我的代码库主要是 C#和 Rust，并且用另一种语言编写的工具的维护会导致很多问题。

有了这些想法，HttpDoom 就诞生了。

**安装**

为了安装 HttpDoom，在当前的发布周期中，由于目前没有独立于运行时的构建版本(只有 *devel* 构建版本可用)，您**必须在您的主机**中安装. NET5 运行时(或 SDK)——又名`dotnet`——并使用。NET 工具链(目前不支持 Windows 的自动安装，欢迎使用您的 PR to 安装脚本。WSL 工作正常):

**美元。/installer.sh**

安装程序脚本还会更新(删除当前安装)新版本的 HttpDoom。

这是如何工作的？

您只需要知道 CLI 的描述(`--help`):

HttpDoom:
HttpDoom 是一个基于响应的工具，用于在一个大的
表面上检查网站。
快速获取基于 HTTP 攻击概述的主机数量

**用法:**
HttpDoom【选项】

**选项:**
-d，–debug 打印调试信息
-f，–follow-redirect HTTP 客户端跟随任何自动
重定向(默认为假)
-m，–Max-redirects 启用
时的最大自动重定向深度(默认为 3)
-s –屏幕截图-分辨率设置屏幕截图分辨率(默认
为 1366×768)
-F，–capture-favicon 下载应用程序 favicon
-h，–headers 为每个请求设置默认头
User-Agent)
(默认只是一个随机的
-t，–HTTP-time out HTTP
请求的超时时间以毫秒为单位(默认为 5000)
-T，–threads 并发线程数
(默认为 20 8080 和 8433)
-P，–用于 HTTP 请求的代理 Proxy
-w，–word-List 要飞越的主机列表
(必需)
–版本显示版本信息
-？ ，-h，–help 显示帮助和用法信息

**但是它快吗？**

让我们来看看在第一个工作版本中运行的默认 HttpDoom 端口(80、443、8080 和 8433)上对 5000 台主机的飞越结果，使用 2 个线程(由通用 Amazon EC2 实例提供)对 Aquatone 1.7.0 上的相同设置:

*   **HttpDoom:**

**…
[+]天桥搞定！在 2.49 分钟内枚举了#31128 个响应
[+]总共获得了#176 个活动主机！
……**

*   **aquatone:t1]**

**…
写会话文件…时间
–开始于:2020-12-20t 08:27:43Z
–结束于:2020-12-20t 08:34:35Z
–时长:6m52s
…**

**注意**:这些测试的结果可能会因您的主机的一系列具体条件而有很大差异。在本地进行测试，并检查哪个工具提供了最佳性能。

**输出**

默认情况下，我们会创建所有必要的目录，并且我们还会随机选择它们的名称(您可以使用`-o`进行设置，如有疑问，请参见`--help`)。

在主目录中，创建一个`general.json`文件，将所有结果包含在一个文件中(以便于在一些可视化工具中进行搜索或摄取)，如下所示:

[
{
"Domain": "google.com "，
" Addresses ":[
" 2800:3f 0:4001:81a::200 e "，
"172.217.28.14"
，
" Requested ":" https://Google . com/"，
"Port": 443，
" Content ":" \ u 003 html \ u003 e \ u000 "charset = utf-8 \ u 0022 \ u003E \ n \ u003C TITLE \ u003E 301 已移动\ u003C/TITLE \ u003E \ u003C/HEAD \ u003E \ u003C body \ u003E \ n \ u003C h1 \ u003E 301 已移动\ u03c/H1 \ u003E \ n 文档已移动\ n \ u003 ca HREF = \ u 022 https://www\ r \ n \ u003C/BODY \ u003E \ u003C/HTML \ u003E \ r \ n "，
" screen shot path ":" C:\ Users \ redated \ AppData \ Local \ Temp \ C 14 obxml . kfy \ snapshot s \ 0086 EAA 9-C4 D4-4 bbf-89d 8-728 E5 D2 ff 184 . png "，
" favicon path ":" C:\ Users \ redated \ AppData \ AppData "
【值】:[

}，
{
【关键点】:" X-Frame-Options "，
【值】:[
【same origin】
]
}，
{
【关键点】:" Alt-Svc "，
"值":[
"h3-29=\u0022:443\u ma=2592000 "，
" H3-T051 = \ u 0022:443 \ u 0022；ma=2592000 "，
" H3-Q050 = \ u 0022:443 \ u 0022；ma=2592000 "，
" H3-Q046 = \ u 0022:443 \ u 0022；ma=2592000 "，
" H3-Q043 = \ u 0022:443 \ u 0022；ma=2592000 "，
" quic = \ u 0022:443 \ u 0022；ma=2592000"
]
}
，
"Cookies": []，
"StatusCode": 301
}，
/…
]

还创建了一个名为*的单个结果*的目录，根据用于请求的 URI 的名称对结果进行单独索引，如果您使用带有选项`-s`的 HttpDoom 和 favicons，如果站点有一个，如果您使用带有选项`-F`的 HttpDoom，还会创建截图:

。
31 be 8e 61-d90 B- 4b 40-bcef-640 FB 31588 e 7 . ico
4e 097 b 93-12f 2-4f 20-9582-547 cc 6d 20312 . ico
个人结果

**注**:单个结果文件的样式为`scheme:address:port`。但是`:`可能是无效字符，这取决于您使用的是什么操作系统。对于更深入的确认，检查 MSDN`Path.GetInvalidFileNameChars()`的文档。

[**Download**](https://github.com/filipi86/httpdoom)