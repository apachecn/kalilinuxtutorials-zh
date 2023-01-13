# APK-MITM:安卓 APK 文件接受 HTTPS 检查

> 原文：<https://kalilinuxtutorials.com/apk-mitm-android-apk-https-inspection/>

[![APK-MITM : Android APK Files for HTTPS Inspection](img/ab8c2a425c6f60a10ca7948548338706.png "APK-MITM : Android APK Files for HTTPS Inspection")](https://1.bp.blogspot.com/-wQM53K2k1ik/Xe1VRQPiOKI/AAAAAAAAD2Y/F4D3G88PBgMELXN1sOcK-I3Oj-i_OmCpwCLcBGAsYHQ/s1600/Apk-MITM.png)

APK-MITM 是一个 CLI 应用程序，可以自动为 HTTPS 检查准备安卓 APK 文件。

使用代理检查移动应用的 HTTPS 流量可能是了解其工作原理的最简单的方法。然而，随着 Android 7 中引入的[网络安全配置](https://developer.android.com/training/articles/security-config)，以及应用程序开发者试图使用[证书锁定](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#What_Is_Pinning.3F)来防止 MITM 攻击，让应用程序与 HTTPS 代理一起工作变得相当乏味。

自动化整个过程。你只需要给它一个 APK 文件，它就会:

*   使用 [Apktool](https://ibotpeaches.github.io/Apktool/) 解码 APK 文件
*   修改应用程序的`**AndroidManifest.xml**`使其成为`**debuggable**`
*   修改应用的[网络安全配置](https://developer.android.com/training/articles/security-config)以允许用户添加证书
*   [插入`return-void`操作码](https://github.com/OWASP/owasp-mstg/blob/master/Document/0x05c-Reverse-Engineering-and-Tampering.md#patching-example-disabling-certificate-pinning)，禁用[证书锁定](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#What_Is_Pinning.3F)逻辑
*   使用 [Apktool](https://ibotpeaches.github.io/Apktool/) 对打了补丁的 APK 文件进行编码
*   使用[超级签名者](https://github.com/patrickfav/uber-apk-signer)对打了补丁的 APK 文件进行签名

你也可以使用安卓应用捆绑包来使用`apk-mitm`到[补丁应用，并且不需要**给你的手机找根**。](https://github.com/shroudedcode/apk-mitm#patching-app-bundles)

**又念——[Linux check:Linux 信息采集脚本 2019](https://kalilinuxtutorials.com/linuxcheck-linux-information-collection-script/)**

**用途**

如果您有最新版本的 [Node.js](https://nodejs.org/en/download/) (8.2+)和 [Java](https://www.oracle.com/technetwork/java/javase/downloads/index.html) (8+)，您可以运行以下命令来修补应用程序:

**$ npx apk-mitm <路径到 apk >**

所以，如果你的 APK 文件叫做`**example.apk**`，你应该运行:

$ npx APK-mitm example . apk

✔解码 apk 文件
✔修改 app 清单
✔修改网络安全配置
✔禁用证书锁定
✔编码打补丁 apk 文件
✔签名打补丁 apk 文件

完成！补丁 APK:。/example-patched.apk

你现在可以在你的 Android 设备上安装`example-patched.apk`文件，并使用像[查理斯](https://www.charlesproxy.com/)或[米特普罗斯](https://www.charlesproxy.com/)这样的代理来查看应用的流量。

**修补应用捆绑包**

你也可以通过提供一个`***.xapk**`文件(例如来自 [APKPure](https://apkpure.com/) )或一个 **`*.apks`** 文件(你可以使用 [SAI](https://github.com/Aefyr/SAI) 自己导出)来为使用和`**apk-mitm**`的[安卓应用捆绑包的应用打补丁。](https://github.com/shroudedcode/apk-mitm/blob/master/android-app-bundle)

**进行手动更改**

有时你需要手动修改一个应用程序来让它工作。在这些情况下,`**--wait**`选项就是您所需要的。启用它将使`**apk-mitm**`在重新启动应用程序之前等待，允许您对临时目录中的文件进行更改。

**注意事项**

*   如果 app 使用谷歌地图，打补丁后地图坏了，那么 app 的 API 密钥很可能是[限制在开发者的证书](https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions)。你必须[创建自己的 API 密钥](https://console.cloud.google.com/google/maps-apis/apis/maps-android-backend.googleapis.com)而不受限制，并运行`**apk-mitm**`和[`--wait`选项](https://github.com/shroudedcode/apk-mitm#making-manual-changes)来替换应用程序的`**AndroidManifest.xml**`文件中的`**com.google.android.geo.API_KEY**`值。
*   如果`apk-mitm`在解码或编码时崩溃，问题可能与 [Apktool](https://ibotpeaches.github.io/Apktool/) 有关。在 GitHub 上查看[他们的问题，寻找可能的解决方法。如果您碰巧发现一个不受这个问题影响的 Apktool 版本，您可以通过`**--apktool**`选项指定其 JAR 文件的路径来指示`**apk-mitm**`使用它。](https://github.com/iBotPeaches/Apktool/issues)

**安装**

上面的例子使用了`npx`下载并执行`apk-mitm`而没有本地安装。如果您想完全安装它，您可以通过运行:

**NPM 安装-g apk-mitm**

[**Download**](https://github.com/shroudedcode/apk-mitm)