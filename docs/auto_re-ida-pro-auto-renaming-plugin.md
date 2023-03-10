# Auto_Re:带有标签支持的 IDA PRO 自动重命名插件

> 原文：<https://kalilinuxtutorials.com/auto_re-ida-pro-auto-renaming-plugin/>

[![Auto_Re : IDA PRO Auto-Renaming Plugin With Tagging Support](img/0896c0dcc92c4344d721561ce61ca5ca.png "Auto_Re : IDA PRO Auto-Renaming Plugin With Tagging Support")](https://1.bp.blogspot.com/-rAztiiWLeT0/Xax3AtqmB0I/AAAAAAAADBQ/JFPsAD74U7ct1n70Hl1lQxn27zdrRvmcQCLcBGAsYHQ/s1600/auto_re-1%2B%25281%2529.png)

**Auto_re** 虚拟命名的函数，有一个 API 调用或跳转到导入的 API。

**在**之前

![](img/56c33a03cbf7217cd0011a1c607c5c49.png)

之后

**![](img/82e41e05d621184ba8e38cd1c95feefa.png)

**也可阅读-[UniFuzzer:一个基于 Unicorn 的闭源二进制文件的模糊工具&LibFuzzer](https://kalilinuxtutorials.com/unifuzzer/)**

*   根据内部调用的 API 指示符为函数分配标签
    *   将标记设置为可重复的函数注释，并在单独的视图中显示标记树

标签视图的一些截图:

![](img/973542aaa71d975430066d7dbf75cef8.png)![](img/786f6b6427baebefa7fd6436300c86e9.png)

标签在未探索的代码中的外观:

![](img/6441e1f44c0d69f5b7760b48793105c6.png)

您可以使用上下文菜单或按下`n`热键轻松重命名功能:

![](img/8166026fffd1973e112ad9484f2be116.png)

**安装**

只需将`**auto_re.py**`复制到`**IDA\plugins**`目录，就可以通过`**Edit -> Plugins -> Auto RE**`菜单访问

[**Download**](https://github.com/a1ext/auto_re)**