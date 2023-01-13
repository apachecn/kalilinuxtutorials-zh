# frisky——帮助二进制应用反转和增强的工具

> 原文：<https://kalilinuxtutorials.com/frisky/>

Frisky 是一个辅助二进制应用程序反转和增强的工具，面向像 iOS 这样的围墙花园。大部分(如果不是全部的话)最近在 iOS 11.1.2 和 macOS 10.12.6 上进行了测试。

### **【Frida-URL-interceptor . js】**

拦截 iOS/macOS 应用程序的所有 URL，允许您在加密之前和解密之后跟踪和更改/拦截每个应用程序的所有网络流量，包括 https:

1.  iOS:首先打开感兴趣的应用程序，例如 Safari
2.  苹果电脑:`frida -U -n Safari -l frida-url-interceptor.js`
3.  它还会在 iOS 应用程序中第一次请求确认代码拦截时显示一个弹出窗口

**也读[Dejavu——开源欺骗框架](https://kalilinuxtutorials.com/dejavu-open-source-framework/)**

### **ldid / ldid2**

当构建依赖于 SHA256 签名的最新 iOS 越狱时，`ldid2`是必需的。这个 repo 将允许你轻松地编译`ldid`和`ldid2`来签署和修改 iOS 二进制文件的权限，从而越狱设备。

1.  macOS: `ldid{2} -e MobileSafari` #抛弃 MobileSafari 的权利
2.  macOS: `ldid{2} -S cat` #签猫

##### 提取 iOS 文件系统上不直接可用的应用程序所使用的共享库，用于静态分析:

*   获取打了补丁的 dyld-210.2.3-patched(包含在此 repo 中)并运行自定义 dsc_extractor(您可能需要从 xcodeproject 编译)以将 iOS' `/System/Library/Caches/com.apple.dyld/dyld_shared_cache_arm*`转储到各个 dylibs 中:
*   苹果电脑:`mkdir -p dylibs && dyld-210.2.3-patched/launch-cache/dsc_extractor /path/to/copied/dyld_shared_cache_arm* dylibs`

##### 通过 Frida 发现和修改库/框架函数调用参数和返回代码:

*   iOS:首先打开感兴趣的应用程序，例如 Twitter
*   macOS: `frida-trace -U -i "*tls*" Twitter` #为 Twitter 应用挂接所有匹配 */tls/i* 的呼叫
*   macOS:现在将生成`__handlers__/libcoretls.dylib/tls_private_key_create.js`:
    *   `onEnter`的`args[2]`是函数的第一个参数
        *   从第一个参数中提取字符串:`Memory.readUtf8String(args[2])`或`ObjC.Object(args[2]))`
    *   `onLeave`的`retval`是返回值
        *   打印出 retval: `log(retval.toInt32())`
        *   调整 retval: `retval.replace(0)`

##### 从 mac 上嗅探(非越狱/越狱)iOS 设备的网络流量:

1.  苹果电脑:`system_profiler SPUSBDataType|perl -n0e'`rvictl -s $1`if/iP(?:hone|ad):.*?Serial Number: (\S+)/s';sudo tcpdump -i rvi0`
2.  标准 tcpdump 选项/过滤器适用

##### 通过 dumpdecrypted.dylib 解密 IPA(iOS apps)/框架进行静态分析:

1.  iOS: `su mobile && mkdir -p ~/tmp && cd ~/tmp && DYLD_INSERT_LIBRARIES=/usr/lib/dumpdecrypted.dylib /var/containers/Bundle/Application/*/AppName.app/AppName`

##### 使用设备控制台在 iOS live 上查看系统日志:

1.  苹果电脑:`deviceconsole`
2.  macOS: `unbuffer deviceconsole | grep something` #保持漂亮的颜色`- requires`期望`, can be installed via` sudo 端口安装期望`or` brew 安装期望` 1

##### 伊莱克特:允许越狱补丁出现在设置中:

1.  iOS: `mv /Library/TweakInject /Library/TweakInject.bak && ln -s /Library/MobileSubstrate/DynamicLibraries /Library/TweakInject && killall -HUP SpringBoard`

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/samyk/frisky)