# trustjack 又一个在 windows 中劫持 dll 的 poco

> 原文：<https://kalilinuxtutorials.com/trustjack-yet-another-poc-for-hijacking-dlls-in-windows/>

TrustJack 是另一个在 windows 中劫持 dll 的 PoC 工具。

使用 cmd 可以做任何你想做的事情，对于一个弹出 cmd 的 dll，[https://github.com/jfmaes/CMDLL](https://github.com/jfmaes/CMDLL)。查看 wietze 网站中的列表，了解应该如何调用 dll。

会自动创建 c:\Windows \System32 并把你的 dll 和选择的二进制文件放在那里，然后执行。通过使用-c 标志再次运行 trustjack 进行清理。

**您可能缺少 fody 2.0，请运行 nuget package restore 进行修复(右键单击解决方案“TrustJacker”，然后选择“restore nu get packages”)**

**v 1 . 0 . 0 by https://twitter.com/Jean_Maes_1994**
**用法:**
–dllpath = VALUE 电脑上 dll 的路径
–binary = VALUE 弹出 shell 的二进制名
-c，–clean，–clean 清理伪文件夹及其内容
-h，-？，–帮助显示此帮助菜单。

[**Download**](https://github.com/jfmaes/TrustJack)