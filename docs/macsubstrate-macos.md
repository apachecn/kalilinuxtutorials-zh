# MAC substrate——MAC OS 上的进程间代码注入工具

> 原文：<https://kalilinuxtutorials.com/macsubstrate-macos/>

**MacSubstrate** 是 macOS 上进程间代码注入的平台工具，功能与 iOS 上的 [Cydia Substrate](http://www.cydiasubstrate.com/) 类似。使用 macSubstrate，你可以将你的插件(`.bundle`或`.framework`)注入到 mac 应用程序(包括沙盒应用程序)中，在运行时对其进行调整。

*   你所需要的就是为你的目标应用程序获取或创建插件。
*   原始目标应用程序的修改和共同设计没有问题。
*   目标应用程序更新后不再工作。
*   超级容易安装或卸载插件。
*   每当目标应用程序重新启动时自动加载插件。
*   提供一个 GUI 应用程序，使注射更加容易。

**也可阅读[IDB——简化 iOS Pentesting 一些常见任务的工具&研究](https://kalilinuxtutorials.com/idb-ios-pentesting/)**

## **MacSubstrate 用法**

*   [下载](https://github.com/wzqcongcong/macSubstrate/releases/latest) macSubstrate.app，放入`/Applications`并启动。
*   如果需要，授予授权。
*   通过导入或拖动到 macSubstrate 来安装插件。
*   启动目标应用程序。*``*

 `*T2`step 3 and step 4 can be switched`*

**插件一旦被 macSubstrate 安装，就会立即生效。但如果你想让它在目标应用重新启动或 macOS 重启时工作，你需要让它保持运行，并允许它在登录时自动启动。**

*   当你不再需要一个插件时，卸载它。

## **插件**

它支持 **`.bundle`** 或 **`.framework`** 的插件，所以你只需要创建一个有效的`.bundle`或`.framework`文件。最重要的是在`info.plist`中添加一个键 **`macSubstratePlugin`** ，用字典值:

| 钥匙 | 价值 |
| --- | --- |
| **T2`TargetAppBundleID`** | 目标应用的`CFBundleIdentifier`，这告诉它要注入哪个应用。 |
| **T2`Description`** | 插件的简要描述 |
| **T2`AuthorName`** | 插件的作者姓名 |
| **T2`AuthorEmail`** | 插件的作者电子邮件 |

详情请查看演示插件 [demo.bundle](https://github.com/wzqcongcong/macSubstrate/blob/master/macSubstratePluginDemo) 和 [demo.framework](https://github.com/wzqcongcong/macSubstrate/blob/master/macSubstratePluginDemo2) 。

##### **Xcode 模板**

macSubstrate 还提供了 [`Xcode Templates`](https://github.com/wzqcongcong/macSubstrate/blob/master/macSubstratePluginTemplate) 来帮助你方便地创建插件:

*   `**ln -fhs ./macSubstratePluginTemplate ~/Library/Developer/Xcode/Templates/macSubstrate\ Plugin**`
*   启动 Xcode，会有 2 个新的插件模板给你。

##### **我的插件**

*   收到*红包*消息时给你发通知。
*   当您收到包含自定义关键字的邮件时，向您发送通知。
*   反召回信息并向您发送通知。

欢迎自己插件对插件的拉取请求。

## **安全**

1.  SIP 是 macOS 上的一项新的安全策略，它将帮助您远离潜在的安全风险。禁用它意味着您将失去 SIP 的保护。
2.  如果你安装了一个开发者的插件，你应该对插件的安全性负责。如果你不信任它，请不要安装它。macSubstrate 会帮助验证一个插件的代码签名，我建议你用 VirusTotal 扫描一下。反正 macSubstrate 只是一个工具，安装什么插件是你自己的选择。

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/wzqcongcong/macSubstrate)`