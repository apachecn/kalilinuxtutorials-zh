# Nexfil:通过用户名查找配置文件的工具

> 原文：<https://kalilinuxtutorials.com/nexfil/>

[![Nexfil : OSINT Tool For Finding Profiles By Username](img/b7d0654229e5b6bc4261729d3319f878.png "Nexfil : OSINT Tool For Finding Profiles By Username")](https://1.bp.blogspot.com/-CmuFUCiAfEg/YOxOfD6gpwI/AAAAAAAAJ9w/BIaMHOBGpm4gu_iDukVLvYc0ptKydmCpwCLcBGAsYHQ/s760/68747470733a2f2f692e696d6775722e636f6d2f52656c6f3432582e6a7067.png)

NExfil 是一个用 python 编写的 **OSINT** 工具，用于通过用户名查找个人资料。提供的用户名在几秒钟内就会在 350 多个网站上被检查。该工具的目标是快速获得结果，同时保持较低的误报率。

如果你喜欢我的工作，请**开始**这个项目😀

如果你发现任何错误或误报，或者如果你想建议更多的网站，请随时打开一个问题。

**特色**

*   **快速**，查找可在 20 秒内完成
*   **包括超过 350 个平台**
*   **成批处理

    *   可以从命令行提供用户名
    *   可以从文件中提供用户名列表** 
*   **结果自动保存在 txt 文件中**
*   **JSON 和 CSV 文件格式[即将推出]**
*   **代理支持[即将推出]**
*   **Tor 支持[即将推出]**

 ****安装**

**git 克隆 https://github.com/thewhiteh4t/nexfil.git
CD NEX fil
pip 3 install-r requirements . txt**

**用途**

**python3 nexfil.py -h
用法:NEX fil . py[-h][-U U][-D D[D…]][-F F][-L L][-T][-v]
NEX fil–在 web 上查找社交媒体简介| v1.0.0
可选参数:
-h、 –help 显示此帮助消息并退出
-u 指定用户名
-d D [D …]指定 DNS 服务器【默认:1.1.1.1】
-F F 指定包含用户名列表的文件
-l L 指定多个逗号分隔的用户名
-t T 指定超时【默认:20】
-v 打印版本
#单个用户名
python3 nexfil.py -u 用户名
#多个*逗号分隔的用户名
python3***

**演示**

![](img/d21c1ad020cf8f51a91b1d8fcbc5f3d1.png)[**Download**](https://github.com/thewhiteh4t/nexfil)**