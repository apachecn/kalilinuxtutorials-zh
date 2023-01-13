# uDork:使用高级谷歌搜索技术的工具

> 原文：<https://kalilinuxtutorials.com/udork/>

[![uDork : Tool That Uses Advanced Google Search Techniques](img/801eafc74e8b0edff65ffead7b77cee3.png "uDork : Tool That Uses Advanced Google Search Techniques")](https://1.bp.blogspot.com/-oYf0h1s6BAE/XywvQeyLWII/AAAAAAAAHM0/FUS9KntikyAbO_yQFz9iPeDKU04ho7JhQCLcBGAsYHQ/s728/uDork_9_7%25281%2529.png)

**uDork** 是一个用 Bash Scripting 编写的脚本，它使用先进的 Google 搜索技术来获取文件或目录中的[敏感信息](https://www.kitploit.com/search/label/Sensitive%20Information)，查找物联网设备，检测 web 应用程序的版本，等等。

它不攻击任何服务器，它只使用预定义的呆子和/或来自 exploit-db.com 的官方名单(谷歌黑客数据库:[https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database))。

**下载&安装**

$ git 克隆 https://github.com/m3n0sd0n4ld/uDork
$ CD uDork
$ chmod+x uDork . sh

![](img/b66fd1616c41eeaf0edd067f1b9d0bf5.png)

**$。/uDork.sh -h**

**获取 Cookie 的步骤&配置 Cookie**

*   登录 facebook.com
*   现在，我们将访问[www.messenger.com](http://www.messenger.com)(它是脸书的消息应用程序)并点击“继续为…”按钮。

![](img/0f1666892d16fed3cbe11c3f88c5bfff.png)

*   一旦我们进去了，我们所要做的就是得到两个使 uDork 工作所需的 cookies。

*   **用火狐:**
    *   右键单击“检查”。

![](img/ec989874fb6c83a20a5bfbb2fbc04969.png)![](img/38c67fa0bfe856ab5447ed2075dd97b7.png)

于是:cookies = " c _ user = XXXXXXxs = XXXXXX"

*   使用谷歌浏览器
    *   右键单击“检查”。

![](img/ec34b3b95fd30e00bbb19054ec3fbc3a.png)![](img/b43c3ecf9c1ba6778923cdf868c7a58e.png)

于是:cookies = " c _ user = XXXXXXxs = XXXXXX"

**Docker 版本**

*   **确认**

推特:[@ interh4ck](https://twitter.com/interh4ck)GitHub:(【https://github.com/interhack86】T2)

$ git 克隆 https://github . com/m3 n 0 SD 0n 4 LD/udrk
$ CD udrk
$ docker build-t udrk。
$ dock run–RM-it-e c _ user = XXXXXX-e xs = XXXXXX udark-h

**使用**

*   菜单

![](img/15b95e69649db6088d034192ee4f3fe3.png)

*   **搜索 pdf 文件的示例**

![](img/2bd4fb891727350eaa8f8cdd897b1abb.png)

*   **搜索默认扩展名列表的示例。**

![](img/a040c63f265e43ea7b12d513e98ff1b3.png)

*   **使用“密码”搜索路线的示例**

![](img/04af26e8772d82632e793b2378e138a8.png)

*   **呆瓜清单**

![](img/78f6fa75847ff0bb2f9a14961b2c2e58.png)

*   **使用呆瓜大规模的例子**

![](img/b5ca3b482c33ff1ef2ae0f07ec8deeda.png)[**Download**](https://github.com/m3n0sd0n4ld/uDork)