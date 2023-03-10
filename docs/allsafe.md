# Allsafe:蓄意攻击的 Android 应用程序

> 原文：<https://kalilinuxtutorials.com/allsafe/>

[![Allsafe : Intentionally Vulnerable Android Application](img/393f36496b1d1d69d43965d36305c309.png "Allsafe : Intentionally Vulnerable Android Application")](https://1.bp.blogspot.com/-BQiGpEN4Ex0/YPgZKCQ8vPI/AAAAAAAAKJc/foXhcJfY0eMWZ8afMyQgkVwqyAEcDPiIgCLcBGAsYHQ/s380/ic_launcher_round%2B%25281%2529.png)

**Allsafe** 是一个故意易受攻击的应用程序，包含各种漏洞。与其他易受攻击的 Android 应用程序不同，这款应用程序不像 CTF，更像是使用现代库和技术的现实生活中的应用程序。此外，我还包括了一些基于 Frida 的挑战，供您探索。祝你黑客生涯愉快！

**有用的弗里达脚本**

我有我的 Frida 脚本(更像模板)在其他存储库中。我敢肯定，他们可能会很方便弗里达相关的任务。看看这个:https://github.com/t0thkr1s/frida

**芙烈达**

这个库包含各种用于 Android 应用渗透测试的 Frida 脚本。我创建这个项目是为了展示 Frida 动态分析框架的能力。你可以阅读我在 Medium 上发表的“Frida 简介”博客，我在里面解释了如何在 Android 上使用 Frida。

**弗里达简介**

*Frida 是一个面向开发人员、*
*逆向工程师和安全研究人员的动态工具套件。*

**项目要求**

跟进所需的工具:

*   Java 反编译器(JD-GUI)
*   Android 模拟器(Genymotion)
*   动态仪器工具包(Frida)

你需要从这里下载 3 个文件:https://github.com/frida/frida/releases

*   Python 直译器
*   python-Frida-工具
*   弗里达-服务器-安卓

根据您的发行版，您可以很容易地安装前两个及其依赖项。至于 frida-server-android，我将带您完成安装和模拟器设置。

**安卓应用**

我创建了一个 Android 应用程序，只是为了演示和测试。我将在示例中使用它，您可以从这里下载:

https://github.com/t0thkr1s/frida

**下载**

你可以简单地克隆这个库或者直接到发布页面下载 Frida 脚本。

**git 克隆 https://github.com/t0thkr1s/frida**

**安装**

你必须在你的系统上安装 Frida。您可以简单地用

**pip3 安装 frida-tools**

**创建虚拟设备**

我用 Android 版本(API 21)添加了一个新的 Genymotion 虚拟设备。设置非常简单，就是通常的下一步、下一步和结束。是时候为 Android 客户端下载 [Frida 服务器](https://github.com/frida/frida/releases)了。不要忘记检查正确的架构！接下来，我们需要将服务器上传到模拟器。我在/opt 目录下安装了 Genymotion

**t 0 thkr 1s @ btk software:/opt/genymobile/genymotion/tools $ ls
aapt ADB glewinfo lib 64**

**上传文件**

**。/ADB push ~/Downloads/Frida _ server/data/local/tmp/**

**更改文件权限**

**。/ADB shell " chmod 755/data/local/tmp/Frida _ server "**

**以分离模式运行服务器**

**。/ADB shell "/data/local/tmp/Frida _ server&"**

现在，模拟器已经准备好了，服务器正在运行！

**逆向工程**

为了理解一个应用程序的内部工作，我们需要对它进行逆向工程。幸运的是，我们可以很容易地恢复 java 源文件。

我不打算在这里写关于逆向工程 Android 应用程序，因为我已经在我以前的帖子里做过了。

不得不承认，demo 应用的逆向工程揭示了其中隐藏的所有秘密。因此，为了使它更现实，让我们假设加密密钥是从用户提供的 PIN 码生成的，该 PIN 码用于加密应用程序中的私人数据。

在这种情况下，强行破解 PIN 码可能是危及整个应用程序安全性的一个好解决方案。这就是为什么你需要选择长而结实的大头针。

**引脚旁路**

好了，您查看了反向源代码，找到了一个方法，它检查提供的 PIN 是否正确。

> 剧透:PIN 在 strings.xml 文件中。

大多数时候，这并不容易…让我们假设，我们不知道 PIN。您发现了 *PinUtil* 类和*布尔* *checkPin(String pin)* 方法。这将检查 pin，如果 pin 正确，则返回 true，否则返回 false。

这里的想法是，我们不需要知道 pin，只要返回 true，我们就进去了。下面的 python 脚本就是这样做的。我用 Javascript API 写了一点 Javascript 代码，硬编码在 python 脚本中。基本上，它使用*PinUtil '*s*checkPin()*方法并覆盖返回值。就这么简单。接下来，您需要指定应用程序的包名来附加 Frida，然后加载脚本并等待日志消息。

**导入 frida，sys
jscode = " " "
Java . perform(function(){
console . log("[*]开始实现覆盖…)
var main activity = Java . use(" infosecadventures . Frida demo . utils . pinutil ")；
main activity . checkpin . implementation = function(PIN){
console . log("[+]PIN 检查成功绕过！”)
返回真；
}
})；
" " "
process = Frida . get _ USB _ device()。attach(' infosecadventures . Frida Demo ')
script = process . create _ script(jscode)
print('[*]运行 Frida 演示应用程序')
script . load()
sys . stdin . read()**

**销蛮力**

之前，我提到过知道 PIN 可能非常有益。在这个例子中，我将向你展示如何与弗里达蛮力。

首先，让我们假设 *PinUtil* 的 *checkPin(String pin)* 方法不是静态的。通过使用 *Java.choose，*我们可以在内存中搜索一个 *PinUtil* 实例，并在找到实例时调用 *onMatch* 。然后，我们可以在循环中使用该实例的方法来测试所有长度为 4 的数字。这其实并不是一个耗时的过程。你甚至可以尝试蛮力数字长度为 5，并在一天内完成取决于这个数字。

*PinUtil* 的类 *checkPin(String pin)* 函数是静态的。这意味着我们不需要在内存中搜索 *PinUtil* 对象，只需要使用类名调用方法。然而，我在下面的脚本中实现了两者(静态和非静态解决方案)。希望不要混淆。第二次赋值将覆盖 *jscode* 变量，并将使用该变量。

**导入 frida，sys
#为非静态类
jscode = " "
Java . perform(function(){
console . log("[*]Starting PIN 蛮力，请稍候…)；
Java . choose(" infosecadventures . Frida demo . utils . pinutil "，{
on match:function(Instance){
console . log("[*]Instance 在内存中找到:"+Instance))；
for(var I = 1000；我<9999；i++){
if(instance . checkpin(I+" ")= = true){
console . log("[+]找到正确的 PIN:"+I)；
}
}
}，
on complete:function(){ }
})；
})；
" "
# For static 类
jscode = " " "
Java . perform(function(){
console . log("[*]Starting PIN 蛮力，请稍候…)
var PinUtil = Java . use(" infosecadventures . Frida demo . utils . PinUtil ")；
for(var I = 1000；我<9999；i++)
{
if(pinutil . checkpin(I+" ")= = true){
console . log("[+]找到正确的 PIN:"+I)；
}
}
})；
" " "
process = Frida . get _ USB _ device()。attach(' infosecadventures . Frida Demo ')
script = process . create _ script(jscode)
print('[*]运行 Frida 演示应用程序')
script . load()
sys . stdin . read()**

**根检查旁路**

我之所以包括这个例子，是因为在银行和其他应用程序中，限制根设备访问是很常见的。这是一个简单的检查，非常非常类似于引脚旁路的例子。

> 我鼓励你自己写剧本，完成后再回来看看！

**寻找加密密钥**

现在，这个脚本中的所有内容您应该也很熟悉了。您可以记录方法的传入参数并正常返回。这样，我们就能够记录使用的加密密钥和明文。同样，密钥是硬编码在代码中的，但是在现实生活中你不会总是这么幸运。我是这样实现的:

**导入 frida，sys
jscode = " " "
Java . perform(function(){
console . log("[*]开始实现覆盖…)
var encryption util = Java . use(" infosecadventures . Frida demo . utils . encryption util ")；
encryption util . encrypt . implementation = function(Key，value){
console . log(" Key:")；
console.log(键)；
console . log(" Value:")；
console.log(值)；
返回 this.encrypt(key，value)；
}
})；
" " "
process = Frida . get _ USB _ device()。attach(' infosecadventures . Frida Demo ')
script = process . create _ script(jscode)
print('[*]运行 Frida 演示应用程序')
script . load()
sys . stdin . read()**

**任务/漏洞**

**不安全的日志记录**

简单的信息泄露漏洞。使用`logcat`命令行工具发现敏感信息。

###### 资源& HackerOne 报道:

*   Logcat Tool
*   比特币基地 OAuth 响应代码泄漏

**硬编码凭证**

代码中保留了一些凭据。你的任务是逆向工程的应用程序，并找到敏感信息。

###### 资源& HackerOne 报道:

*   zomato hhardcore 证书
*   8×8 硬编码凭据
*   混响 hhardcore api 秘密

**根检测**

这纯粹是为了弗里达练习。让代码相信你的设备没有根！

**任意代码执行**

用第三方应用程序安全地加载模块并不容易。编写一个 PoC 应用程序并利用漏洞！

###### 资源& HackerOne 报道:

*   通过第三方包上下文执行任意代码

**安全标志旁路**

另一个基于 Frida 的任务。这里没有真正的漏洞，只是绕过安全标志玩得开心！

###### 资源& HackerOne 报道:

*   Android FLAG _ 安全参考

**证书锁定旁路**

证书锁定是使用 OkHttp 库实现的。你必须绕过它，以查看与 Burp 套件的流量。

###### 资源& HackerOne 报道:

*   证书和公钥锁定
*   比特币基地的弱点

**不安全的广播接收器**

应用程序中有一个易受攻击的广播接收器。用正确的数据触发它，你就完成了！

###### 资源& HackerOne 报道:

*   Android 广播概述
*   ok.ru 广播接收机开发
*   易受攻击的广播接收器

**深度链接剥削**

类似于不安全的广播接收器，您需要提供正确的查询参数来完成此任务！

###### 资源& HackerOne 报道:

*   Android 深度链接
*   抓住不安全的深度链接
*   潜望镜深度链接·CSRF

**SQL 注入**

只是一个普通的 SQL 注入，你可以在网络应用程序中找到。不需要反转代码来绕过登录机制。

###### 资源& HackerOne 报道:

*   内容提供者中的 SQL 注入

**易受攻击的网络视图**

您也可以在不反编译应用程序的情况下完成这项任务。弹出警告对话框并读取文件！

###### 资源& HackerOne 报道:

*   ownCloud WebView XSS

**小打补丁**

在这个任务中，您必须通过编辑 Smali 代码来修改应用程序的执行流。最后，重建并签署 APK！

###### 资源& HackerOne 报道:

*   优步·APK 签名者

**原生库**

应用程序使用一个本地库来验证输入的密码。对库进行逆向工程以找到密码，然后使用 Frida 来挂钩本地方法。

###### 资源& HackerOne 报道:

*   Ghidra
*   切割机

[**Download**](https://github.com/t0thkr1s/allsafe)