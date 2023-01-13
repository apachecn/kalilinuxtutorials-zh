# Droopescan:一个基于插件的扫描器，帮助安全研究人员

> 原文：<https://kalilinuxtutorials.com/droopescan/>

[![](img/18ca891c6e1657fb130c184e1a045c78.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1GbQV8h_1hruyT033Ri5yOj3tetBSdQcKZh9VzPGEqINyLVyyBIwjgodqnPAGyI0Cz39hJ-o8tbJ7YM1vTYVRcBmyjQXzggDt00BD4gHYLHcOwiZHSuZjYfO27nvR8q4wLmIGGBkYtKQ9LaszJAArnWTnYmwo5dEfxEkfRxm1lWhX63uF137EyVBo/s875/DmL03Y6XgAApbhT.png)

Droopescan 是一款基于插件的扫描器，可以帮助安全研究人员识别多个 CMS 的问题。

未经双方事先同意，使用 droopescan 攻击目标是非法的。最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。请注意，虽然 droopescan 输出远程主机上安装的最可能的 CMS 版本，但版本号和漏洞之间的任何关联都必须由用户手动完成。

支持的 CMS 有:

*   银色条纹
*   wordpress 软件
*   Drupal

部分功能用于:

*   Joomla(仅版本枚举和感兴趣的 URL)
*   Moodle(插件和主题非常有限，小心)

计算机:~/droopescan$ droopescan 扫描 Drupal-u http://example.org/-t 32
[+]没有找到主题。
[+]找到可能感兴趣的 URL:
默认的 changelog 文件–https://www.example.org/CHANGELOG.txt
默认的 admin–https://www.example.org/user/login
[+]可能的版本:
7.34
[+]找到插件:
查看 https://www.example.org/sites/all/modules/views/
https://www.example.org/sites/all/modules/views/README.txt
https://www.example.org/sites/all/modules/views/LICENSE.txt
令牌 https://www.example.org/sites/all/modules/token/
https://www.example.org/sites/all/modules/token/README.txt
https://www.example.org/sites/all/modules/token/LICENSE.txt
path auto https://www . example . org/sites/all/modules/path auto/
https://www . example . org/org/T15
https://www . example . org/sites/all/modules/ctools/changelog . txt
https://www . example . org/sites/all/modules/ctools/license . txt
https://www.example.org/sites/all/modules/ctools/API.txt
特色 https://www.example.org/sites/all/modules/features/
https://www . example . org/sites/all/modules/features/changelog . txt
https://www . example . org/sites/all/modules/features/README . txt
https

您可以通过运行以下命令获得选项的完整列表:

**dropescan–帮助
dropescan 扫描–帮助**

# 为什么不是 X？

因为下垂扫描:

*   很快
*   很稳定
*   是最新的
*   允许同时扫描多个站点
*   是 100%蟒蛇皮

# 安装

## 带 pip(推荐)

使用 pip 易于安装:

**apt-get 安装 python-pip
pip 安装 droopescan**

## 来源

手动安装如下:

**git 克隆 https://github.com/droope/droopescan.git
CD droops can
pip install-r requirements . txt
。/droopescan 扫描–帮助**

主分支对应于最新的版本(pypi 中的内容)。开发分支不稳定，所有拉取请求都必须针对它。

## 黑弓

BlackArch 软件包安装(由第三方维护):

**sudo pacman-S dropescan**

## 码头工人

您可以构建 docker 映像并从 Docker 运行 droopescan:

**git 克隆 https://github . com/droopo/droopex scan . git
CD droopex scan
dock build-t droopo/droopex scan。
显示帮助
对接器运行──RM droopo/dromescan
例扫描 drupal 站点
对接器运行──RM droopo/dromescan Drupal-u https://Drupal . example . com**

# 特征

## 扫描类型

Droopescan 的目标是在默认情况下最准确，同时不会由于过多的并发请求而使目标服务器过载。由于这个原因，默认情况下，大量的请求将由四个线程发出；分别使用`**--number**`和`**--threads**`参数更改这些设置。

该工具能够执行四种测试。默认情况下，运行所有测试，但是您可以使用`**-e**`或`**--enumerate**`标志指定以下测试之一:

*   p — *插件检查*:执行几千个 HTTP 请求，并返回发现安装在目标主机上的所有插件的列表。
*   t — *主题检查*:同上，但针对主题。
*   v — *版本检查*:下载几个文件，根据这些文件的校验和，返回所有可能版本的列表。
*   i — *感兴趣的 url 检查*:检查感兴趣的 URL(管理面板、自述文件等)。)

## 目标规格

您可以通过传递`**-u**`或`**--url**`参数来指定要扫描的特定主机:

**dropescan 扫描 Drupal-u example.org**

也可以省略`**drupal**`参数。这将触发“CMS 识别”，就像这样:

**dropescan 扫描-u example.org**

利用`**-U**`或`**--url-file**`参数可以扫描多个 URL。此参数应该设置为包含 URL 列表的文件的路径。

**droopescan 扫描 drupal -U list_of_urls.txt**

本例中还可以省略 **`drupal`** 参数。对于每个站点，它将发出几个 GET 请求，以便执行 CMS 识别，如果该站点被认为是受支持的 CMS，它将被扫描并添加到输出列表中。这可能很有用，例如，在您组织的所有站点上运行`**droopescan**`。

**droopescan scan-U list _ of _ URLs . txt**

下面的代码块包含一个 URL 列表示例，每行一个:

**http://localhost/Drupal/6.0/
http://localhost/Drupal/6.1/
http://localhost/Drupal/6.10/
http://localhost/Drupal/6.11/
http://localhost/Drupal/6.12/**

对于 URL 文件，包含 URL 和一个用制表符或空格分隔的用于覆盖默认主机头的值的文件也是可以的。在对大范围的主机进行扫描时，如果您希望防止不必要的 DNS 查询，这将非常方便。为了澄清，下面举一个例子:

**192 . 168 . 1 . 1 example.org
http://192 . 168 . 1 . 1/example.org
http://192 . 168 . 1 . 2/Drupal/example.org**

通过扫描官方网站(例如 wordpress 的`**wordpress.org**`)来测试扫描仪是否适用于特定的 CMS 是很诱人的，但官方网站很少运行各自 CMS 的 vainilla 安装或做非正统的事情。例如，`**wordpress.org**`运行的是 wordpress 的最新版本，它根本不会被`**droopescan**`识别为 wordpress，因为校验和与任何已知的 wordpress 版本都不匹配。

## 认证

应用程序完全支持`**.netrc**`文件和`**http_proxy**`环境变量。

使用. netrc 文件进行基本身份验证。一个示例 netrc(一个名为`**.netrc**`的文件，位于您的根目录下)文件可能如下所示:

**机器 secret.google.com
登录 admin@google.com
密码 Winter01**

## 输出

这个应用程序支持“标准输出”和 JSON，前者是供人类使用的，后者更适合机器使用。这个输出在主要版本之间是稳定的。

这可以用 **`--output`** 标志来控制。一些示例 JSON 输出如下所示(去掉多余的空格):

**" themes ":{
" is _ empty ":true，
"finds": [
]
}，
"有趣的 URL ":{
" is _ empty ":false，
" finds ":[
{
" URL ":" https:\/\/www . Drupal . org \/CHANGELOG . txt "，
"description ":"默认的 changelog 文件。"
}、
{
“URL”:“https:\/\/www . Drupal . org \/user \/log in”，
“描述”:“默认管理员。”
}
]
}，
【版本】:{
【is _ empty】:false，
【发现】:[
【7.29】，
【7.30】，
【7.31】
]
}，
【插件】:{
【is _ empty】:false，
【发现】:[
{

。**

如果部分扫描没有运行，JSON 对象中可能会缺少一些属性。

这是多站点输出的样子；每行包含一个有效的 JSON 对象，如上所示。

**$ droopescan 扫描 Drupal-U six _ and _ above . txt-e v
{ " host ":" http://localhost/Drupal-7.6/，" version": {"is_empty": false，" finds ":[" 7.6 "]} }
{ " host ":" http://localhost/Drupal-7.7/，" version": {"is_empty": false，" finds": ["7.7"]}}
{"host ":" " finds ":[" 7.14 "]}
{ " host ":" http://localhost/Drupal-7.15/，" version": {"is_empty": false，" finds ":[" 7.15 "]} }
{ " host ":" http://localhost/Drupal-7.16/，" version": {"is_empty": false，" finds ":[" 7.16 "]}
{ " host ":" http " finds ":[" 7.24 "]} }
{ " host ":" http://localhost/Drupal-7.25/"，" version": {"is_empty": false，" finds ":[" 7.25 "]} }
{ " host ":" http://localhost/Drupal-7.26/"，" version": {"is_empty": false，" finds ":[" 7.26 "]}
{ " host ":" http:/**

## 调试

当事情不尽如人意时，您可以使用`**--debug-requests**`命令来检查原因。

一些输出可能如下所示:

**【head】http://localhost/framework/…403
【head】http://localhost/CMS/CSS/layout . CSS…404
【head】http://localhost/framework/CSS/upload field . CSS…200
【head】http://localhost/misc/test/error/404/is present . html…404
【head】http://localhost/widgetextensions/…
[+]扫描完成(0:00:00.058** 422 已过)

## 统计数据

通过运行以下命令，您可以获得关于扫描程序功能的最新报告

**droopescan 统计数据**

一些示例输出可能如下所示:

“drupal”可用的功能:

*   **枚举插件(XXXX 插件。)**
*   **列举主题(XXXX 主题。)**
*   **枚举感兴趣的网址(X 个网址。)**
*   **枚举版本(直到版本 X.X.X-alphaXX，X.XX，X . XX)
    可用于‘Joomla’的功能:**
*   **枚举感兴趣的网址(X 个网址。)**
*   **枚举版本(直到版本 XX。X，X.X.X，X.X.XX.rcX.)
    可用于‘WordPress’的功能:**
*   **枚举感兴趣的网址(X 个网址。)**
*   **枚举版本(最高版本为 X . X . X . X，X.X.X.)
    可用于“silverstripe”的功能:**
*   **枚举插件(XXX 插件。)**
*   **列举主题(XX 个主题。)**
*   **枚举感兴趣的网址(X 个网址。)**
*   **枚举** te 版本(直到版本 X.X.XX，X.X.XX，X.X.XX)

[**Download**](https://github.com/SamJoan/droopescan)