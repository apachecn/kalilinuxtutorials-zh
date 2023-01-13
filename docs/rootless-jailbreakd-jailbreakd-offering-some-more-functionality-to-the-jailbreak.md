# 无根越狱-为越狱提供更多的功能

> 原文：<https://kalilinuxtutorials.com/rootless-jailbreakd-jailbreakd-offering-some-more-functionality-to-the-jailbreak/>

无根越狱是一个小的越狱，为越狱提供了更多的功能。使用 CPDisctributedMessageCenter。要编译你需要 theos(为什么？为什么不呢？我喜欢 theos。如果你足够聪明，你仍然可以很容易地手动编译它，所以是的)

**也可阅读[what web——用你的 Web 应用发现安全漏洞的工具](https://kalilinuxtutorials.com/whatweb/)**

## **设置无根越狱** 

*   获取 AppSupport 头并将它们添加到包含路径中(https://github . com/theos/headers/tree/05405174749d 912 f 7726121 fcb 5 f 27 de 73 af 08/app support)
*   在 main.m 文件中包含“app support/cpdistributedmessagingcenter . h”
*   https://github . com/Jake James/root me-tutorial/blob/master/app support . TBD 的链接
*   The general syntax follows as this:

    ```
    `CPDistributedMessagingCenter *messageCenter = [CPDistributedMessagingCenter centerNamed:@"com.jakeashacks.rootme"];
    [messageCenter sendMessageAndReceiveReplyName:@"MESSAGE_NAME" userInfo:[NSDictionary dictionaryWithObject:[NSString stringWithFormat:@"%d", getpid()] forKey:@"pid"]];`
    ```

    ## **编译**

    ```
    **./make.sh**
    ```

    ## **命令**

    目前，这些命令是可用的

    1.  “root me”:setuid(0)和 setgid(0)为您服务
    2.  “unsandbox”:清除大部分沙箱(现在这没有任何用处，因为要调用 jailbreakd，你必须先取消沙箱)
    3.  “platformize”:通过设置 TF_PLATFORM 和 CS_PLATFORM_BINARY 将二进制文件标记为平台
    4.  “setcsflags”:设置一些标志，如 CS_PLATFORM_BINARY、CS_GET_TASK_ALLOW、CS_DEBUGGED 等
    5.  “授权”:将授权设置为真或假。示例:

    ```
    **CPDistributedMessagingCenter *messageCenter = [CPDistributedMessagingCenter centerNamed:@"com.jakeashacks.rootme"];
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];**
    **[dict setValue:@"com.apple.private.skip-library.validation" forKey:@"ent"]; //entitlement name
    [dict setValue:@"true" forKey:@"value"]; //true or false
    [dict setValue:[NSString stringWithFormat:@"%d", getpid()] forKey:@"pid"];
    [messageCenter sendMessageAndReceiveReplyName:@"entitle" userInfo:dict];**
    ```

    ## **二进制需要 suid 权限还是 root 所有权？**

    不，我没费那个劲，因为

*   没有包管理器，所以所有的二进制文件都由你控制，
*   没有根重新安装，因此不会造成大混乱，
*   您需要取消装箱才能调用 jailbreakd(您通过 SSH 运行的所有二进制文件都满足这一要求),对我来说这就足够了。它来了吗？可能是的

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/jakeajames/multi_path/tree/master/multi_path/jailbreakd)