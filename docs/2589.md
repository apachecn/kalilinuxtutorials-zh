# DroidDetective:一个面向 Android 应用的机器学习恶意软件分析框架

> 原文：<https://kalilinuxtutorials.com/droiddetective/>

[![](img/bdf7e05c754a4cb500e6d4241bc107e3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieaRUZ54n1eSReZr-5WnswlA-4mebuR5y3cgiuDKLxxKOiOTCyqazaqgLIAKSrXdCMWcuEY6c1dail0wnV5DvfbU1NJUOIocO16T4UmEHL-Lxe3SrPLZp9LgyPhwsjYaPlSVK5HfgVl0DhL_rvcH5o5S91mIj9okPFpBjMcNP-CcZAVnJ6EA5-I02p/s728/cover%20(1).png)

**DroidDetective** 是一款 Python 工具，用于分析 Android 应用程序(apk)的潜在恶意软件相关行为和配置。当提供了一个应用程序的路径(APK 文件)时，Droid Detective 将预测(使用它的 ML 模型)该应用程序是否是恶意的。Droid Detective 的特性和品质包括:

*   分析在应用程序的`**AndroidManifest.xml**`文件中指定了~330 个权限中的哪一个。
*   分析应用程序的 **`AndroidManifest.xml`** 文件中使用的标准和专有权限的数量。
*   使用随机森林机器学习分类器，从大约 14 个恶意软件家族和大约 100 个谷歌 Play 商店应用程序中训练出上述数据。

## 装置

所有 DroidDetective 依赖项可以手动安装，也可以通过需求文件安装

**pip install-r requirements . txt**

DroidDetective 已经在 Windows 10 和 Ubuntu 18.0 LTS 版上进行了测试。

## 用法

DroidDetective 可通过将 APK 作为命令行参数提供给 Python 文件来运行，例如:

**python droid detective . py myandroidapp . apk**

如果一个`**apk_malware.model**`文件不存在，那么工具将首先训练这个模型，并且将需要一个 apk 的训练集，它位于项目根目录下的一个名为 **`malware`** 的文件夹和另一个名为`**normal**`的文件夹中。成功运行后，无论模型识别出 APK 是恶意的还是良性的，结果都会打印到 CLI 上。此输出的示例如下所示:

**已分析文件“com.android.camera2.apk”，被识别为非恶意软件。**

可以向`**DroidDetective.py**`提供一个额外的参数，作为保存结果的 Json 文件。如果这个 Json 文件已经存在，那么这次运行的结果将被附加到 Json 文件中。

**python droid detective . py myandroidapp . apk output . JSON**

# 数据科学 ML 模型

DroidDetective 是一个 Python 工具，用于分析 Android 应用程序(apk)的潜在恶意软件相关行为。这是通过训练一个随机森林分类器来实现的，该分类器基于从已知恶意软件 apk 和 Android 应用商店上可获得的标准 apk 中获得的信息。这个工具是预先训练好的，但是，模型可以随时在新的数据集上重新训练。

该模型目前使用 APKs `**AndroidManifest.xml**`文件中的权限作为特性集。这是通过为每个标准的 Android 权限创建一个字典，并且如果权限存在于 APK 中，则将特性设置为 **`1`来实现的。类似地，为清单中使用的权限数量和清单中发现的未标识权限数量添加了一个功能。**

预训练模型是从位于 ashisdb 的存储库中的大约 14 个恶意软件家族(每个具有一个或多个 APK 文件)以及位于谷歌 Play 商店的大约 100 个正常应用程序中训练出来的。

以下是该 ML 模型的统计数据:

**精度:0.9310344827586207
召回:0.91666666666666666
精度:0.9166666666666666
F 值:0.916666666666666**

该模型用于识别恶意软件的前 10 个权重最高的功能(即 Android 权限)如下所示:

**" Android . permission . system _ ALERT _ WINDOW ":0.019091367939223395，
" Android . permission . access _ NETWORK _ STATE ":0.021001765263234648，
" Android . permission . access _ WIFI _ STATE ":0.02198962579120518，
" Android . permission . receive _ BOOT _ COMPLETED ":0.0263998**

[Download](https://github.com/user1342/DroidDetective)