# RMS:运行时移动安全

> 原文：<https://kalilinuxtutorials.com/rms/>

[![RMS : Runtime Mobile Security](img/45a3e9d649753e543bdcb5ce43841fc0.png "RMS : Runtime Mobile Security")](https://1.bp.blogspot.com/-LuuErajzvig/Xq7Zz2eKPUI/AAAAAAAAGJQ/gVTsAc1ePzkY07HHCAB5GUfXmMdoxOqygCLcBGAsYHQ/s1600/RMS%25281%2529.png)

**RMS(运行时移动安全)**是一个强大的 web 界面，帮助您在运行时操作 Android Java 类和方法。您可以轻松地转储所有已加载的类和相关方法，动态挂钩所有内容，跟踪方法参数和返回值，加载自定义脚本和许多其他有用的东西。

**一般信息**

运行时移动安全(RMS)目前仅支持 Android 设备。

它已经在 MacOS 和以下设备上进行了测试:

*   AVD emulator
*   Genymotion 仿真器
*   亚马逊火棒 4K

它应该也能在 Windows 和 Linux 上很好地工作，但可能需要一些小的调整。

不要同时连接多个设备。RMS 目前还没那么聪明。

**先决条件**

FRIDA 服务器在目标设备上启动并运行

参考 FRIDA 官方指南进行安装:[https://frida.re/docs/android/](https://frida.re/docs/android/)

**已知问题**

*   有时 RMS 无法加载复杂方法。出现这种情况时使用过滤器，或者随意改进算法(default.js)。
*   代码未优化

**改进**

*   iOS 支持
*   请随时通过 Pull 请求将您最好的 JS 脚本发送给我。我很乐意在下一个 RMS 版本中捆绑所有最好的默认脚本。例如
    *   根检测旁路
    *   ssl 锁定旁路
    *   反射检测
    *   等等…

**也可阅读-[项目 iKy v 2 . 5 . 0-从电子邮件中收集信息的工具](https://kalilinuxtutorials.com/project-iky-v2-5-0-tool-that-collects-information-from-an-email/)**

**安装**

**(可选)**创建 python 虚拟环境
pip 3 install-r requirements . txt
python 3 mobile security . py

**用途**

*   **只需插入软件包名称**即可运行您最喜爱的应用程序

**注意** : RMS 附加了一个名为 **com.android.systemui** 的持久化进程，以在目标应用程序启动之前获取已经加载到内存中的所有类的列表。如果您对此有问题，请尝试找到一个在您的设备上运行良好的不同软件包。您可以通过 Config 选项卡或简单地编辑 config.json 文件来设置另一个默认包。

![](img/2209267c8a4f4cb6acc53af780c525bf.png)

*   **检查哪些类和方法已经加载到内存中**

![](img/85658cdf9a616498447b30ca88094c92.png)

*   **动态挂钩类/方法并跟踪它们的参数和返回值**

![](img/d1094a8f52b372e26e02bda65f5bba4c.png)

*   **在堆上搜索特定类的实例，并调用其方法【BETA】**

![](img/d62692735ec365cadb16b6a64908ce3d.png)

*   **选择一个类，并为它的所有方法动态生成一个钩子模板**

![](img/c2f440e8af55fe08c5122d449e2a19b0.png)

*   **轻松检测已经加载到内存中的新类**

![](img/8311de0f12a4e674317e2067063ac7fc.png)

*   **即时注入您最喜欢的 FRIDA 定制脚本**

只需添加您的。js 文件放在 custom_script 文件夹中，它们将由 web 界面自动加载，准备执行。

![](img/21a5624148ea74a09292279a11afc99a.png)

**学分**

特别感谢以下开源项目带来的灵感:

*   [芙烈达](https://github.com/frida/frida)
*   [反对意见](https://github.com/sensepost/objection)
*   [房子](https://github.com/nccgroup/house)

**演示应用:**

[RootBeer Sample](https://play.google.com/store/apps/details?id=com.scottyab.rootbeer.sample) 是用来展示 RMS 如何工作的演示应用。 [RootBeer](https://github.com/scottyab/rootbeer) 是一个**惊人的根检测库**。我决定使用示例应用程序作为演示，只是为了表明，由于每个客户端只检查，如果不与服务器端验证结合，它的根检测逻辑很容易被绕过。

[抗弗里达](https://github.com/b-mueller/frida-detection-demo)弗里达检测实例。

[**Download**](https://github.com/m0bilesecurity/RMS-Runtime-Mobile-Security)