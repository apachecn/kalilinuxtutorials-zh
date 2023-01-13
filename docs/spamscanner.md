# Spamscanner:垃圾邮件扫描程序是最好的反垃圾邮件、电子邮件过滤和防钓鱼服务

> 原文：<https://kalilinuxtutorials.com/spamscanner/>

[![](img/5774c077664598ff4409fd534eebd9e8.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiBGJj6TDcURS0rad8vPnsoLlBf0k8AdHX4cTYIkoDDDlbe3357VD6_XGZqdm13Vye8-VjQuQW0lWNkPcZyty0Z3gRPZewEjIVdafxNYdVbvEjgkqNkHO12A71KAIWfpCBsf1U1vtzM-LNyKV5rkcf22dFX9yD_FXmvBvkJo-bxaMdpPmGrJc2BF5E-=s1127)

Spamscanner 是@niftylettuce 在现有垃圾邮件检测解决方案遇到无数障碍后开发的工具和服务。换句话说，这是我们目前针对垃圾邮件的计划。

我们的目标是构建并利用一个可扩展的、高性能的、简单的、易于维护的强大 API，用于我们的转发电子邮件服务，以限制垃圾邮件并提供其他措施来防止对我们用户的攻击。

最初我们尝试使用 SpamAssassin，后来评估了 rspamd——但最终我们了解到，所有现有的解决方案(甚至除此之外的解决方案)都非常复杂，缺少必需的功能或文档，配置起来非常困难；进入门槛高，或者拥有专有的存储后端(可以在未经您同意的情况下存储和读取您的邮件),这限制了我们的可扩展性。

对我们来说，我们重视数据和用户的隐私和安全——具体来说，我们对存储任何类型的日志或元数据采取“零容忍政策”(请参阅我们的隐私政策了解更多相关信息)。这些解决方案都没有遵守这一隐私政策(没有删除基本的垃圾邮件检测功能)，所以我们必须创建自己的工具——因此“垃圾邮件扫描器”诞生了。

我们创建的解决方案提供了几个特性，并且完全可以根据您的喜好进行配置。你可以在下面了解更多的实际算法。欢迎投稿。

**特色**

垃圾邮件扫描程序包括现代、基本和高性能的功能，有助于减少垃圾邮件、网络钓鱼和可执行文件攻击。

**朴素贝叶斯分类器**

我们的朴素贝叶斯分类器在这个存储库 npm 包中可用，并且随着它从转发电子邮件中获得上游匿名 SHA-256 散列数据而频繁更新。

它使用一个由垃圾邮件、垃圾邮件和滥用报告格式(“ARF”)数据组成的非常大的数据集进行训练。这个数据集是从多个来源私下编译的。

**垃圾内容检测**

提供现成的训练有素的朴素贝叶斯分类器(使用朴素贝叶斯和引擎盖下的自然)，它来自成千上万的垃圾邮件和业余爱好者的电子邮件。该分类器依赖于将标记化和词干化的单词(也与电子邮件的语言相关)分为两类(“垃圾邮件”和“火腿”)。

**钓鱼内容检测**

强大的网络钓鱼检测方法，可防止域名交换、IDN 同形异义词攻击等。

**可执行链接和附件检测**

链接和附件检测技术，检查邮件中的链接、“内容类型”标题、文件扩展名、幻数，并防止对文件名的同形异义攻击，所有这些都是针对可执行文件扩展名列表的。

**病毒检测**

它使用 ClamAV 扫描电子邮件附件(包括嵌入的 CID 图像)中的特洛伊木马、病毒、恶意软件和/或其他恶意威胁。

**NSFW 图像探测**

我们计划增加 NSFW 图像检测和选择加入毒性检测。

**算法**

简而言之，垃圾邮件扫描程序算法是这样工作的:

1.  邮件被传递给垃圾邮件扫描程序，称为“源”。
2.  以并行和异步的方式，将源代码传递给检测以下内容的函数:
    *   分类
    *   网络钓鱼
    *   可执行的
    *   武断的
    *   病毒
3.  在所有函数完成后，如果有任何函数返回一个指示它是垃圾邮件的值，那么该源就被认为是垃圾邮件。提供了详细的结果对象，用于检查原因。

我们已经广泛地记录了 API，它提供了对这些函数如何工作的深入了解。

**要求**

请注意，您可以在 https://spamscanner.net 免费使用垃圾邮件扫描 API，而不必独立维护和托管自己的实例。

| 属国 | 描述 |
| --- | --- |
| 节点. js | 您必须安装 Node.js 才能使用此项目，因为它是基于 Node.js 的。我们建议使用 nvm 并使用`**nvm install --lts**`安装最新版本。如果你只是想使用垃圾邮件扫描 API，请访问 https://spamscanner.net 网站了解更多信息。 |
| 云耀斑 | 您可以选择将`**1.1.1.3**`和`**1.0.0.3**`设置为您的 DNS 服务器，因为我们使用 DNS over HTTPS 来执行链接查找，如果 DNS over HTTPS 请求失败，可以回退到系统本身设置的 DNS 服务器。我们使用 Cloudflare for Family 来检测网络钓鱼和恶意软件链接。 |
| ClamAV | 您必须在您的系统上安装 ClamAV，因为我们用它来扫描病毒。参见下面的 ClamAV 配置。 |

**ClamAV 配置**

**Ubuntu**

1.  安装 ClamAV

**sudo apt-get 更新
sudo apt-get install build-essential clamav-daemon clamav-fresh clam clamav-official-sigs-QQ
sudo service clamav-daemon start**

如果你在检查 **`sudo service clamav-daemon status`、**时收到错误，你可能需要运行`**sudo freshclam -v**`，但这不太可能，取决于你的发行版。

配置 ClamAV:

**sudo ven/etc/clamav/clamd . conf**

**-Example
+# Example
-# stream maxlength 10M**
**+stream maxlength 50M
+#这个文件路径可能在你的 OS 上不一样(没关系)
-# local socket/tmp/clamd . socket
+local socket/tmp/clamd . socket**

**sudo ven/etc/clamav/fresh hclam . conf**

**-例
+#例**

确保 ClamAV 在引导时启动:

**system CTL enable fresh clamd
system CTL enable clamd
system CTL start fresh clamd
system CTL start clamd**

**苹果电脑**

1.  安装 ClamAV:

**brew 安装 clamav**

配置 ClamAV:

**如果你在英特尔 MAC OS
sudo mv/usr/local/etc/clamav/clamd . conf . sample/usr/local/etc/clamav/clamd . conf
如果你在 M1 macOS(或安装到`/opt/homebrew`的更新 brew)
sudo mv/opt/home brew/etc/clamav/clamd . conf . sample/opt/home brew/etc/clamav/clamd . conf**

**-Example
+# Example
-# stream maxlength 10M
+stream maxlength 50M
+#这个文件路径可能在你的 OS 上不一样(没关系)
-# local socket/tmp/clamd . socket
+local socket/tmp/clamd . socket**

**如果你在英特尔 MAC OS
sudo mv/usr/local/etc/clamav/fresh clam . conf . sample/usr/local/etc/clamav/fresh clam . conf
如果你在 M1 macOS(或安装到`/opt/homebrew`的更新 brew)
sudo mv/opt/home brew/etc/clamav/fresh clam . conf . sample/opt/home brew/etc/clamav/fresh clam . conf**

**如果你在英特尔 MAC OS
sudo vim/usr/local/etc/clamav/fresh clam . conf
如果你在 M1 macOS(或安装到`/opt/homebrew`的更新 brew)
sudo vim/opt/home brew/etc/clamav/fresh clam . conf**

**-例
+#例**

**新鲜蛤蜊**

确保 ClamAV 在引导时启动:

**sudo vim/Library/launch daemons/org . clamav . clamd . plist**

启用它并在引导时启动它:

**sudo launch CTL load/Library/launch daemons/org . clamav . clamd . plist
sudo launch CTL start/Library/launch daemons/org . clamav . clamd . plist**

您可能希望定期运行`**freshclam**`来更新配置，或者为`**launchctl**`配置一个类似的`**plist**`配置。

**安装**

npm:

**npm 安装垃圾邮件扫描器**

**用途**

**const fs = require(' fs ')；
const path = require(' path ')；
const spam scanner = require(' spam scanner ')；
const scanner = new spam scanner()；
/
//注意:`source`参数是要扫描的完整 raw 邮件
//你可以以字符串、缓冲区、或者有效文件路径
//
const source = fs . read file sync(
path . join(_ _ dirname，' test '，' fixtures '，' spam . EML ')
)；
// async/await 用法
(async()=>{
try {
const scan = await scanner . scan(source)；
console.log('scan '，扫描)；
} catch(err){
console . error(err)；
}
})；
//然后/捕捉用法
扫描仪
。【扫描(源)】T24。然后(scan = > console.log('scan '，scan))
。catch(console . error)；
//回调用法
if (err)返回 console . error(err)；
scanner.scan(source，(err，scan) = > {
if (err)返回 console . error(err)；
console.log('scan '，扫描)；
})；**

**API**

### `**const scanner = new SpamScanner(options)**`

`**SpamScanner**`类接受一个可选的`**options**`options 对象来配置正在创建的垃圾邮件扫描器实例。它返回一个通常被称为`**scanner**`的新实例。

我们已经配置了扫描仪默认值，以利用默认的分类器和合理的选项来确保扫描正常工作。

有关所有选项及其默认值的列表，请参见该存储库根目录下的 index.js 文件。

### `**scanner.scan(source)**`

**注意:**这是该 API 最有用的方法，因为它返回扫描消息的扫描结果。

接受必需的`**source**`(字符串、缓冲区或文件路径)参数，该参数指向(或者是)完整的原始 SMTP 消息(例如，它包括标题和完整的电子邮件)。通常这被称为“eml”文件类型，包含扩展名`**.eml**`，但是您可以传递一个字符串或缓冲区表示来代替文件路径。

该方法返回一个承诺，当扫描完成时，该承诺用一个`**scan**`对象进行解析。您还可以将此方法与第二个回调参数一起使用。

扫描结果作为具有以下属性的对象返回(下面列出了每个属性的描述):

**{
is_spam: Boolean，
message: String，
results:{
class ification:Object，
phishing: Array，
executables: Array，
arbitrary: Array
}，
links: Array，
token:Array，
mail: Object
}**

| 财产 | 类型 | 描述 |
| --- | --- | --- |
| `**is_spam**` | 布尔代数学体系的 | 如果`**results.classification**`对象的`**category**`属性被确定为`**"spam"**`，`**results.phishing**`不为空，或者`**results.executables**`不为空，则返回`**true**`的值，否则其值为`**false**` |
| `**message**` | 线 | 一条友好的消息，指示为什么`**source**`被分类为垃圾邮件或 ham(例如，来自 **`results.classification`、`results.phishing`** 和`**results.executables**`的所有消息/原因被结合在一起) |
| `**results**` | 目标 | 提供扫描详细信息的属性对象(对调试非常有用) |
| `**results.classification**` | 目标 | 基于朴素贝叶斯分类器对`**source**`的分类返回具有`**category**`(字符串)和`**probability**`(数字)值的对象 |
| `**results.phishing**` | 排列 | 表示在`**source**`上检测到的网络钓鱼企图的字符串数组 |
| `**results.executables**` | 排列 | 表示在`**source**`上检测到的可执行攻击的字符串数组 |
| `**results.arbitrary**` | 排列 | 表示在`**source**`上检测到的任意垃圾邮件检测机制的字符串数组 |
| `**links**` | 排列 | 一个字符串数组，包含在`**source**`上检测到的所有经过解析和规范化的链接。这对 URL 信誉管理非常有用。 |
| `**tokens**` | 排列 | **Debug only:** 一组内部使用(用于分类器分类)并为调试而公开的标记化和词干化单词(根据确定的区域设置从`**source**`解析而来)。只有当实例中的`**debug**`选项设置为`**true**`时，才会返回该属性。 |
| `**mail**` | 目标 | **Debug only:** 一个被解析的`**mailparser.simpleParser**`对象，在内部使用，为调试而公开。只有当实例中的`**debug**`选项设置为`**true**`时，才会返回该属性。 |

### `**scanner.getTokensAndMailFromSource(source)**`

接受电子邮件消息(如`**.eml**`文件)的`**source**`参数(字符串、缓冲区或文件路径)。如果`**source**`参数是一个字符串并被确定为有效路径，这个方法将自动在内部调用`**fs.readFile**`。

该方法使用 mailparser 的`**simpleParse**r`函数解析`**source**`电子邮件消息。

然后，它对消息的主题、html 和文本部分(根据消息的 i18n 确定语言，例如 **`en`、`es`、`jp`、`ru`** 等)进行标记化和词干化。参见`**getTokens**`方法文档，了解如何确定语言。

目前，垃圾邮件扫描程序支持以下语言环境进行标记化、词干分析和停用词删除。注意，我们根据在`**source**`中检测到的语言选择特定的分词器、词干分析器和停用词。

| 名字 | 现场 |
| --- | --- |
| 阿拉伯语 | `**ar**` |
| 丹麦的 | `**da**` |
| 荷兰人 | `**nl**` |
| 英语 | `**en**` |
| 芬兰人的 | `**fn**` |
| 现代波斯语 | `**fa**` |
| 法语 | `**fr**` |
| 德国人 | `**de**` |
| 匈牙利的 | `**hr**` |
| 印度尼西亚的 | `**in**` |
| 意大利的 | `**it**` |
| 日本人 | `**ja**` |
| 挪威的 | `nb`，`nn` |
| 抛光剂 | `po` |
| 葡萄牙语 | `pt` |
| 西班牙语 | `es` |
| 瑞典的 | `sv` |
| 罗马尼亚的 | `ro` |
| 俄语 | `ru` |
| 泰米尔人 | `ta` |
| 土耳其的 | `tr` |
| 越南人 | `vi` |
| 中国人 | `zh` |

这个方法返回一个用`**{ tokens, mail }**`对象解析的承诺。您还可以将此方法与第二个回调参数一起使用。

注意，`**tokens**`是经过解析的标记化和词干化单词的数组，`**mail**`是经过解析的`**simpleParser**`邮件对象。

这是用于构建单词袋模型的核心内部方法，然后将单词袋模型提供给分类器进行分类。

有关此方法的示例实现，请参见 classifier.js(例如，在生成默认分类器数据集时使用的方法)。

### `scanner.getClassification(tokens)`

接受从来自`**scanner.getTokensAndMailFromSource**`的对象中返回的`**tokens**`属性解析的`**tokens**`令牌数组(见上文)。

该方法返回一个承诺，该承诺根据 naivebayes 确定的分类进行解析。

为了抵御无意义的攻击媒介，分类被限制在有限的单词包中。默认值是每个类别的`**20000**`个单词。换句话说最常见的`**20000**`垃圾词和 **`20000`** 常见的火腿词被用来确定原始来源的分类。

我们计划进一步完善分类器，通过对维基媒体(或谷歌人工智能)每种语言的单词字典数据集进行测试，去除所有的胡言乱语。这不是一个容易完成的壮举，但是我们有具体的计划来实现这个目标。

### `**scanner.getPhishin**gResults(mail)`

接受一个`**mailparser.simpleParser**`解析的邮件对象。

此方法返回一个承诺，该承诺通过一组消息(如果有)来解析，这些消息指示从消息中解析的链接被检测为网络钓鱼企图。您还可以将此方法与第二个回调参数一起使用。

该方法还防止了常见的 IDN 单应性攻击。如果*任何*链接被检测到以字符串`**xn--**`开始(例如，在从`**punycode.toASCII**`转换之后)，那么它被检测为网络钓鱼。

一个常见的例子是`**рaypal.com**`的链接，当它被转换成 ASCII 码时是`**xn--aypal-uye.com**`——但是当它被渲染时看起来几乎和`**paypal.com**`一样(如果不是完全一样的话)。

此方法针对 Cloudflare for Families 服务器检查成人相关内容、恶意软件和网络钓鱼。这意味着我们通过 HTTPS 对针对恶意软件的`**1.1**.1.2`请求和针对成人相关内容的`**1.1.1.3**`请求执行两个独立的 DNS。如果需要分析是否要在应用程序中标记成人相关内容，可以分析包含“成人相关内容”的消息的消息结果数组。

如果您使用要求)中提到的 Cloudflare for Family DNS 服务器，那么如果出现任何 DNS HTTPS 请求错误，它将回退到使用系统上设置的 DNS 服务器进行查找，从而使用 cloud flare for Family DNS。(使用 DNS over HTTPS，回退 DNS . resolve 4)-如果它返回`**0.0.0.0**`，则认为它是网络钓鱼。

我们实际上在 2020 年 8 月帮助 Cloudflare 更新了他们的文档，以说明对于在 FQDN 和 IP 查找中恶意发现的内容，会返回`**0.0.0.0**`的结果。

### `scanner.getExecutableResults(mail)`

接受一个`**mailparser.simpleParser**`解析的邮件对象。

请注意，该方法使用“内容类型”头检测、文件扩展名检测和幻数检测来检测(关于 executables.json。

此方法返回一个承诺，该承诺通过一组消息(如果有)来解析，这些消息指示从消息中解析的链接和/或附件是危险的(例如，包含的可执行文件或指向可执行文件的链接)。您还可以将此方法与第二个回调参数一起使用。

该方法还考虑到文件扩展名和名称可能会受到通过在文件名上使用 **`punycode.toASCII`** 的同形异义攻击。

它还会扫描邮件本身中的链接，查找指向可执行文件的链接。

### `scanner.getTokens(str, locale, isHTML = false)`

接受一个`str`(字符串)和可选的`**locale**`(字符串——根据 i18n 语言环境有效的 i18n 语言环境)和`**isHTML**`参数。如果`**isHTM**L`被设置为`**true**`，那么这表明作为`**str**`传递的字符串是 HTML 格式的。

根据传递的、检测到的或默认的区域设置，返回 SHA-256 哈希标记化单词和词干单词的数组。如果`**config.debug**`为`**true**`，则值不会作为散列值返回(例如，这在测试和调试中很有用)。

请注意，这是“智能”的，因为它将解析消息的“内容-语言”报头、HTML 消息的`**<meta http-equiv="Content-Language" content="en-us">**`的 **`content`** 属性或`**<html lang="en">**`的`**lang**`属性。

在解析消息的语言之后，它将使用包 franc 尝试确定消息的语言(只要消息至少有 150 个字符，这是可配置的)。

**最重要的是**以下类型的令牌被替换为加密生成的随机散列:

*   表情符号(这包括用 Markdown 编写的 Github 风格的表情符号和所有 Unicode 表情符号)
*   MAC 地址
*   信用卡
*   比特币地址
*   电话号码
*   十六进制颜色
*   首字母缩略词
*   缩写
*   电子邮件地址
*   链接
*   整数和浮点值
*   货币

请注意，在执行词干提取时，这些类型的令牌的替换会被列入白名单。

缩写也被扩展，例如“他们是”变成两个标记，“他们”和“是”，然后相应地被词干化。

### `scanner.getArbitraryResults(mail)`

接受一个`**mailparser.simpleParser**`解析的邮件对象。

该方法将针对任意垃圾邮件检测原因(如 GTUBE)测试邮件。

返回一组消息(如果有的话),表明由于任意原因，部分消息被检测为与垃圾邮件相关。您还可以将此方法与第二个回调参数一起使用。

### `scanner.getVirusResults(mail)`

接受一个`**mailparser.simpleParser**`解析的邮件对象。

此方法返回一个承诺，该承诺通过一组消息(如果有)来解析，这些消息表明从消息中解析的附件是危险的(例如，包含特洛伊木马、病毒、恶意软件和/或其他恶意威胁)。您还可以将此方法与第二个回调参数一起使用。

ClamAV 在内部使用此方法，以便扫描附件(并行)。

### `scanner.parseLocale(locale)`

接受一个`**locale**`，并将其作为移除了附加本地化的小写字符串返回(例如，`**en-US**`变成了`**en**`，而`**en_US**`也变成了`**en**`)。

**缓存**

默认情况下，通过一个`**memoiz**e`配置选项，对成人内容和恶意软件查找进行无限限制。

您可以配置`**memoize**`或`**client**`选项，其中`**memoize**`是传递给 memoizee 的选项对象，而`**client**`是 Redis 的实例，比如用@ladjs/redis 创建的实例。

请参考测试中两种实现的示例。如果您采用`**memoize**`的方法，那么您应该设置一个`**size**`选项，例如:

const scanner = new spam scanner({
//…
memoize:{
//由于 memoizee 不支持提供 mb 或 gb 的缓存大小
//我们可以计算出最大值可能是多少
//域名的最大长度是 253 个字符(字节)
//如果我们想在内存中存储 1 GB，那就是
/`Math.floor(bytes('1GB') / 253)`= 4244038(域)
//注意这是 所以如果你有 4 个核心服务器
//你会有 4 个线程，因此需要 4 GB 的空闲内存
size:math . floor(bytes(' 1GB ')/253)
}
})；

请注意，在转发电子邮件时，我们使用`**client**`方法，因为我们在多个服务器上运行多个线程，内存缓存效率不高。

[**Download**](https://github.com/spamscanner/spamscanne)