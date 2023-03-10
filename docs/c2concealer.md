# C2 隐藏器:命令行工具，生成随机 C2 延展性配置文件，用于钴罢工

> 原文：<https://kalilinuxtutorials.com/c2concealer/>

[![](img/e771d1a853106713c9cba03924729005.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjh98RkPL9ItyuINfBVl8a0oCkzjlwKe5vjNB8gBGjSFfNdKFiTdJYODkfO9sl_OE0wkn11x4ry5W0q9vw9yvq3LA7JEdPniuXXNu1WnUFKcRJl18YC3h14HsPcyJ4WOnRovlob6enLjcl2nHEG2fdrzX1GGZWx4cCP5jyd2Z7vaCSqxc13YWC3wwX-/s728/images.png)

**C2concealer** 是一个命令行工具，可生成随机 C2 延展性配置文件，用于钴击。

## 装置

**chmod u+x install.sh
。/install.sh**

## 构建码头工人形象

docker build-t C2 遮瑕膏。

## 使用 Docker 运行

`**docker container run -it -v <cobalt_strike_location>:/usr/share/cobaltstrike/ C2concealer --hostname google.com --variant 3**`

## 用法举例

**用法:
$ C2 隐藏器–主机名 google.com–变体 3
标志:
(可选)
–主机名
HTTP 客户端和服务器端设置中使用的主机名。默认值为无。
–variant
一个整数，定义要生成的 HTTP 客户端/服务器变量的数量。
推荐 1 到 5 之间。最多 10 个。**

## 控制台输出示例

**root @ kali:~ # C2 concealer–variant 1–hostname google.com
[I]在您的系统上搜索 c2lint 工具(Cobalt Strike 的一部分)。可能需要 10-20 秒。
【我】在/opt/cobaltstrike/c2lint 目录下找到了 c2lint。
选择一个 SSL 选项:
自签名 SSL 证书(只需输入几个细节)
LetsEncrypt SSL 证书(需要一个临时的 A 记录，用于将相关域指向这台机器)
现有的密钥库
没有 SSL
【？]选项[1/2/3/4]:**

## 它是如何工作的

我们仔细阅读了 Cobalt Strike 文档，并定义了对每个概要文件属性有意义的值的范围。有时候，数据就像某个范围内的随机整数一样简单，而其他时候，我们需要从 python 字典中选取一个随机值。无论哪种方式，我们都是从定义数据开始创建工具的，这些数据将构成有效的概要文件。

然后，我们将每个有延展性的型材(或砌块)分成单独的。py 文件，它包含为每个属性随机绘制适当值的逻辑，然后为该配置文件块输出格式化字符串。我们将所有的剖面块连接在一起，运行一些快速一致性检查，然后通过 Cobalt Strike linter (c2lint)运行剖面。输出是*应该*为您的约定工作的概况。我们始终建议在运行活动之前测试概要文件(包括流程注入和生成)。

如果您正在研究代码，我们建议从这两个文件开始:/C2concealer/ **main** 。py 和/C2concealer/profile.py。查看注释后，检查文件夹:/C2concealer/components 中的个人轮廓块生成器。

## 定制工具

这是至关重要的。这是一个工具的开源版本，我们已经私下使用了大约一年。我们的私有回购有几个额外的 IOC 和一个完全不同的数据集。虽然运行该工具为构建钴冲击韧性剖面提供了一个良好的开端，但我们建议深入以下领域，以自定义随机填充该工具的数据:

/C2 遮瑕膏/数据/

*   dns.py(自定义 dns 子域)
*   file_type_prepend.py(自定义 http-get-server 响应的外观…也称为 c2 控制指令)
*   params.py(包含公共参数名和通用单词列表的两个字典)
*   post _ ex . py(spawn _ to process list…一定要改这个)
*   reg_headers.py(典型的 http 头，如用户代理和服务器)
*   smb.py(通信通过 smb 时使用的 smb 管道名)
*   stage.py(用于更改与 stager 相关的 IOC 的数据)
*   transform.py(有效负载数据转换…无需更改)
*   urls.py(在整个工具中用于构建 URIs 的文件类型和 url 路径组件…一定要改变这一点)

此外，您可以在整个概要文件生成过程中定制各种属性。例如，在文件“/C2 concealer/components/stage block . py”中，您可以更改 PE 图像大小值的绘制范围(在第 73-74 行附近)。请浏览组件目录中所有不同的文件。

如果您已经做到了这一步，那么我们知道您将会从这个工具中获得很多用处。我们建议查看此工具的方式是，我们已经构建了自动生成这些配置文件的框架代码，现在由您来考虑哪些值对您的活动的每个属性有意义，并更新数据源。

[**Download**](https://github.com/FortyNorthSecurity/C2concealer)