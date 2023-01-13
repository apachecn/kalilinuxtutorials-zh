# Metabigor:没有任何 API 键的命令行搜索引擎

> 原文：<https://kalilinuxtutorials.com/metabigor-search-engines-api-key/>

[![Metabigor : Command Line Search Engines Without Any API Key](img/ae0a46e2c20d537052a78764903fde96.png "Metabigor : Command Line Search Engines Without Any API Key")](https://1.bp.blogspot.com/-cdkVyvYPlCE/XPdueWnUFPI/AAAAAAAAApA/4xHof3FKGvQpw2yXuHlTWR4KLhscEpbHQCLcBGAs/s1600/68747470733a2f2f696d6167652e666c617469636f6e2e636f6d2f69636f6e732f7376672f313737342f313737343435372e737667-svg.png)

Metabigor 允许你从命令行向优秀的搜索引擎(如 Shodan，Censys，Fofa 等)进行查询，而不需要任何 API 键。

但是为什么呢？

*   不要使用你的 API 密匙，这样你就不用担心 API 报价的限制。
*   在没有高级帐户的情况下从命令行进行查询。
*   获得更多的结果，没有保费帐户。
*   但是我有一个高级账户为什么我需要这个？
    *   同样，它不会失去你的 API 报价。
    *   你的查询会被优化，所以你会得到比手动或 API 键更多的结果。
    *   永远不要得到重复的结果。

**也可阅读-[phones Piot:使用开放的 ADB 端口，我们可以利用 Android 设备](https://kalilinuxtutorials.com/phonesploit-adb-ports-exploit-andriod/)**

它是如何工作的？

它会使用您的 cookie 或不模拟搜索从浏览器和优化查询，以获得更多的结果。

**目前支持的搜索引擎**

*   肖丹。
*   Censys。
*   Fofa Pro。

**安装**

**git 克隆 https://github.com/j3ssie/Metabigor
CD Metabigor
pip 3 install-r requirements . txt**

**演示**

[![](img/3e095d366928991d57110ee687b2bc7c.png)](https://asciinema.org/a/247172)

**如何使用**

**基本用法**

```
./Metabigor.py -s -q '<your_query>' [options]
```

查看[高级用法](https://github.com/j3ssie/Metabigor/wiki/Advanced-Usage),探索一些令人敬畏的选项

**示例命令**

**注意**:如果您想获得更多结果，请在`config.conf`填写您的证书或您的课程。

**。/meta Igor . py-s fofa-q ' title = " Dashboard–Confluence "&&body = "。org"'**

**。/meta Igor . py-s fofa-q ' title = " Dashboard–Confluence "&&body = "。org " '-b–disable _ pages**

**。/meta Igor . py-s shod an-q ' port:" 3389 " OS:" Windows " '-debug**

**选项**

**[*]设置会话

执行下面的命令或者直接修改 config.conf 文件
。/meta Igor . py-s shod an–cookies =
。/meta Igor . py-s censys–cookies =
。/meta Igor . py-s fofa–cookies =

[*]基本用法
。/meta Igor . py-s-q "[Options]

[*]更多选项
-d OUTDIR，–OUTDIR OUTDIR
目录输出
-o 输出，–OUTPUT 输出
输出文件名
–RAW 原始目录存储原始查询
–PROXY 代理对搜索引擎做请求例如:
http://127 . 0 . 0 . 1:8080
-b 自动暴力破解国/meta Igor . py-s fofa-q ' title = " Dashboard–Confluence "&&body = "。org"' -b
。/meta Igor . py-s fofa-q ' title = " Dashboard–Confluence "&&body = "。org " '-b–disable _ pages
。/meta Igor . py-s shod an-q ' port:" 3389 " OS:" Windows " '-debug
。/meta Igor . py-s shod an-Q list _ of _ query . txt–debug-o RDP . txt
。/meta Igor . py-s censys-q '(SCADA)和协议:" 502/Modbus " '-o something-debug-proxy socks 4://127 . 0 . 0 . 1:9050**

**免责声明**

该工具仅用于教育目的。你要对自己的行为负责。如果你在使用这个软件时搞砸了一些事情或者违反了任何法律，那是你的错，而且仅仅是你的错。

**鸣谢:**维塔利·戈尔巴乔夫和皮卡西

[**Download**](https://github.com/j3ssie/Metabigor)