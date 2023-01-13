# Badlnk:在快捷方式文件(.lnk)

> 原文：<https://kalilinuxtutorials.com/badlnk/>

[![Badlnk : Reverse Shell In Shortcut File (.lnk)](img/a6866400bcd3b0873f1a3dab5a1dae61.png "Badlnk : Reverse Shell In Shortcut File (.lnk)")](https://1.bp.blogspot.com/-MvHqU2iDUW8/XsTSbZfkF3I/AAAAAAAAGYk/VIDbRfNQ23gV6bf6RoJzxh6ZQD-9LtBHwCLcBGAsYHQ/s1600/BADlnk%25281%2529.png)

**Badlnk** 是快捷方式文件(。lnk)。

它是如何工作的？

快捷文件(Microsoft Windows 9.x) LNK 是 Microsoft Windows 用来指向可执行文件的快捷文件的文件扩展名。LNK 代表链接。快捷方式文件用作可执行文件的直接链接，而不是必须导航到可执行文件。

LNK 文件包含一些基本属性，比如可执行文件的路径和“起始”目录。LNK 文件使用弯曲的箭头表示它们是快捷方式，并且文件扩展名是隐藏的(即使在 Windows 资源管理器中禁用“隐藏已知文件类型的扩展名”之后)。

该脚本创建一个. lnk 文件，该文件指向用户的“cmd.exe”文件(位于默认文件夹 C:\Windows\System32\cmd.exe 中),以通过参数运行反向 shell。

特征

使用 Ngrok.io 进行反向 TCP 端口转发

**要求**

*   ngrok Authtoken(TCP 隧道):在 https://ngrok.com/signup 注册
*   您的授权令牌在您的仪表板上可用:https://dashboard.ngrok.com
*   安装您的 auhtoken:。/ngok authtype token
*   安装后，目标必须重新启动/重新登录。注册文件

**也可阅读-[wifi mpkin 3:流氓接入点攻击的强大框架](https://kalilinuxtutorials.com/wifipumpkin3/)**

**用途**

git 克隆 https://github.com/thelinuxchoice/badlnk
CD badlnk
bash badlnk . sh

**免责声明**

未经双方同意使用 BADlnk 攻击目标是非法的。最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责