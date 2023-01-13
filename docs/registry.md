# 注册表间谍:跨平台注册表浏览器的原始 Windows 注册表文件

> 原文：<https://kalilinuxtutorials.com/registry/>

[![https://blogger.googleusercontent.com/img/a/AVvXsEhAviw-wU15OnHs0D7g_WJ34WVHsZgYIu_2mKBz2rKS05ZZdfX3jqJaSEsfuaki7tg-7_iR2_A6ktyKwi7Ro8k_yg564swXjntcigZVObnYNtWzXrwbON3uwqqzyTlp0vLlC3xoJs93MIF7wAegt7mprhd4sNmHhpHBoxid38g3UEE0ixt9ZJOmgkqW=s728](img/8eeff79aeae6987b0d2090c598eb5752.png "https://blogger.googleusercontent.com/img/a/AVvXsEhAviw-wU15OnHs0D7g_WJ34WVHsZgYIu_2mKBz2rKS05ZZdfX3jqJaSEsfuaki7tg-7_iR2_A6ktyKwi7Ro8k_yg564swXjntcigZVObnYNtWzXrwbON3uwqqzyTlp0vLlC3xoJs93MIF7wAegt7mprhd4sNmHhpHBoxid38g3UEE0ixt9ZJOmgkqW=s728")](https://blogger.googleusercontent.com/img/a/AVvXsEhAviw-wU15OnHs0D7g_WJ34WVHsZgYIu_2mKBz2rKS05ZZdfX3jqJaSEsfuaki7tg-7_iR2_A6ktyKwi7Ro8k_yg564swXjntcigZVObnYNtWzXrwbON3uwqqzyTlp0vLlC3xoJs93MIF7wAegt7mprhd4sNmHhpHBoxid38g3UEE0ixt9ZJOmgkqW=s728)

**Registry-Spy** 是一款免费、开源的跨平台 Windows 注册表查看器。这是一个快速，现代，多才多艺的原始注册表文件的浏览器。

功能包括:

*   快速、动态解析意味着没有前期开销
*   一次打开多个蜂窝
*   搜索
*   十六进制浏览器
*   修改时间戳

**要求**

*   Python 3.8 以上版本

**安装**

从发布页面下载最新版本。或者，使用下列方法之一。

**皮普(推荐)**

*   `**pip install registryspy**`
*   `**registryspy**`

**手动**

*   `**pip install -r requirements.txt**`
*   `**python setup.py install**`
*   `**registryspy**`

**单机**

*   `**pip install -r requirements.txt**`
*   `**python registryspy.py**`

**截图**

**主窗口**

![](img/9045c0cbe63be5bf54f7f5e416833ccc.png)

**查找对话框**

![](img/97b3f66c2e25c968ad627e4cfeb55ad5.png)

**大楼**

依赖关系:

*   PyInstaller 4.5+

常规建筑:`**pyinstaller registryspy_install.spec**`

创建单个文件:`**pyinstaller registryspy_onefile.spec**`

[**Download**](https://github.com/andyjsmith/Registry-Spy)