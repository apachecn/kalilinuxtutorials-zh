# Uac-A-Mola:安全研究人员调查新 Uac 旁路的工具

> 原文：<https://kalilinuxtutorials.com/uac-a-mola-tool-for-security-researchers-to-investigate-new-uac-bypasses/>

[![Uac-A-Mola : Tool For Security Researchers To Investigate New UAC Bypasses](img/99f21676c07b1f70379ff9d56e2f53bc.png "Uac-A-Mola : Tool For Security Researchers To Investigate New UAC Bypasses")](https://1.bp.blogspot.com/-Bvn2qm6hKRI/XbBRlqgGNXI/AAAAAAAADFA/Z82mlP9bM3IY3xrI6x2XDowldUOhREGcACLcBGAsYHQ/s1600/UAC-A-Mola%25282%2529.png)

除了检测和利用已知的旁路之外，UAC-莫拉是一个允许安全研究人员调查新 UAC 旁路的工具。UAC 莫拉有模块进行保护和减轻 UAC 旁路。

**安装**

要安装 uac-a-mola，您必须执行以下操作:

1.  **下载并安装 python 2.7.x for Windows** 考虑到您的特定基础设施，您可以在这里找到二进制文件:【https://www.python.org/downloads/】T2
2.  **将 python 路径添加到路径环境变量**中。您可以通过执行以下步骤来实现这一点:
    *   右键单击“我的电脑”,左键单击“属性”
    *   左键单击进入系统配置
    *   左键单击环境变量
    *   在“系统变量”框中，双击“路径”
    *   左键点击进入新添加以下路径:
        *   C:\Python27\
        *   C:\Python27\scripts\
3.  **从 github** 下载 uac-a-mola 工具。zip 文件或通过克隆 repo。
4.  **用 cmd 打开 uac-a-mola-master 文件夹，执行以下命令**:

**pip install-r requirements . txt**

Uac-a-mola 现在准备好摇滚了！您可以通过键入以下命令来测试其功能:

**CD uacamola
python uacamola . py**

**攻击模块**

使用攻击模块非常简单，几乎不需要解释。你唯一要做的就是使用 ***load*** 命令在框架中加载相应的模块，你可以看到选项或者输入参数使用 ***show*** 命令，用 ***run*** 命令模块被执行:

**也可阅读-[XMLRPC:用 Python 3](https://kalilinuxtutorials.com/xmlrpc-brute-forcer-wordpress-python/)T3 编写的针对 WordPress 的蛮力器**

uac-a-mola >加载。\ modules \ attack \ dll _ jacking _ wusa . py
[++]加载模块…
[+]模块已加载！【UAC-a-mola[DLL _ jacking _ wusa . py]>show

**作者**
| _ Pablo Gonzalez(Pablo @ 11 paths 或@pablogonzalezpe)
**名称**
| _ 用 wusa.py 复制 DLL
**描述**
| _ 用于复制特权路径中的 DLL(wusa 方法 win 7/8/8.1)
| _ Name _ folder = x86 _ Microsoft . Windows . common-controls _ 6595 b 64144 CCF 1 df _ 6 . 0 . 7601 . 17514 _ none _ 41e 6975 e 2 BD 6 f 2(名称文件夹)
|
| _ Destination _ path = C:\ Windows \ System32(目标路径)

UAC-a-mola[dll _ jacking _ wusa . py]>run
[+ 有根吗？😀
移除路径…
成功:完成
UAC-a-mola[dll _ jacking _ wusa . py]>

**再比如:**

uac-a-mola >加载模块\ attack \ file less _ fod helper . py
[+]加载模块…
[+]模块加载完毕！
UAC-a-mola[Fileless _ fod helper . py]>show

**作者**
| _ 圣地亚哥·埃尔南德斯·拉莫斯
**姓名**
| _ Fileless fod helper
|**描述**| _ Fileless–fod helper 绕过 UAC**选项(Field = Value)**
| _ instruction = C:\ Windows \ system3

**缓和模块**

使用缓解方法也很简单，但是它们有一个稍微复杂一些的内部结构，这将在本节中解释。关于它的使用，必须做的第一件事是加载可用的缓解模块:

uac-a-mola >加载模块\缓解\ bypass _ 缓解. py
[+]加载模块…
[+]模块已加载！
uac-a-mola[Bypass _ remediation . py]>show

**Author**
|*Santiago Hernandez Ramos Name |_ 此模块将检测所选的二进制文件并检测可能的 UAC 绕过描述| _ 绕过缓解选项(Field = Value)|*[REQUIRED]Password = None(用于连接的密码)
|
| _[REQUIRED]bin list _ File = None(包含要挂钩的二进制文件列表，每行一个)【关键字】

在这种情况下，我们需要设置一个密码，代理将使用该密码与将在 uacamola 框架中执行的监听器进行通信。我们可以在路径 *uacamola/support/agents* 中找到代理，打开那个文件我们可以看到密码:

fod helper _ ag = Agent(' fod helper . exe '，' localhost '，5555，' uacamola ')
fod helper _ ag . send _ forbidden(" Software \ Classes \ ms-settings \ Shell \ Open \ command ")

*uacamola* 将是用于认证和通信的密码，但我们可以更改它。另一个需要的参数是包含要监视的二进制文件列表的文件的路径，这个二进制文件在代理路径中必须有一个 agent.pyw 文件。

uac-a-mola[Bypass _ remediation . py]> show

**作者**
| _ Santiago Hernandez Ramos
**Name**
| _ 此模块将检测所选的二进制文件并检测可能的 UAC 旁路
**描述**
| _ 旁路缓解
**选项(Field = Value)**
| _ Password = uacamola(连接密码)
|
| _ ^

只需填写这些字段并执行 *run* 命令，uacamola 将开始监控列表中出现的二进制文件中与 UAC 旁路相关的所有活动。

如果检测到危险的活动，它会自动删除(文件系统或注册表的)危险分支，并以安全的方式执行二进制文件。要退出该模式，我们只需按下 *ENTER* 键。

[Download](https://github.com/ElevenPaths/uac-a-mola#attack-modules)