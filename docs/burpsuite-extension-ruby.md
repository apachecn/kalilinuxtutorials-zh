# BurpSuite 扩展 Ruby:使用 Ruby 加速构建 Burp 扩展的模板

> 原文：<https://kalilinuxtutorials.com/burpsuite-extension-ruby/>

由于缺乏 BurpSuite 扩展 Ruby 的实例和实现，我们决定让所有 Ruby 爱好者能够轻松、自信、快速地开始为 InfoSec 社区构建有用的扩展。

这个库是一个 Burp 套件扩展的模板集合，关注于 [Burp 套件 API](https://portswigger.net/burp/extender/api/) 功能，并通过 JRuby 简化 Java 语言使用。

在这里，我们试图使它尽可能简单。你只需要专注于你的想法，节省大量的时间去寻找例子和扩展。

这里有几个消息，一个是好消息，一个是坏消息:

**好消息是**，所有编写的扩展，无论是用 Java、Ruby 还是 Python 编写的，对你来说都是非常有用的资源。

**坏消息是**，你必须阅读和理解 Java 的一个*位*。这是好消息的关键😉

**注意:**为了使用前清晰起见，一些扩展已经支持动画截图。

**也读作[MalwareCMDMonitor——显示在混合分析](https://kalilinuxtutorials.com/malwarecmdmonitor/)** 上分析的最新实例使用的命令行

## **囊状延伸红宝石**

### **打嗝 GUI**

| 延长 | 描述 |
| --- | --- |
| send_alert_pure.rb | 向警报选项卡发送消息的纯实现 |
| popup_msg_pure.rb | 弹出 GUI 消息框的纯实现 |
| suite_itab_pure.rb | 套件选项卡(ITab)的纯实现 |
| editor_tab_pure.rb | 编辑器选项卡的纯实现(除了请求和响应选项卡之外) |
| 上下文 _ 菜单 _pure.rb | 上下文菜单(右键菜单)的纯实现 |
| suite_itab_subtab.rb | 套件选项卡和子选项卡(子面板)的纯实现 |
| suite_itab_subtab_icon.rb | 带有图标的套件选项卡和子选项卡(子面板)的纯实现 |
| 上下文 _ 菜单 _pure.rb | 带有一些动作的自定义菜单和子菜单的纯实现 |
| tab_tree.rb | 选项卡的实现包含一个项目树 |
| – | – |

### 资源

*   定制 Burp 套件–充分利用 Burp 扩展[ [Link](http://www.slideshare.net/AugustDetlefsen/burp-extensions)
*   谷歌呆子: **`burp extension site:github.com`**

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/KINGSABRI/Burp_Suite_Extension_Ruby)