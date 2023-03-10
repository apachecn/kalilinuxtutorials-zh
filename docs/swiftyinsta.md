# SwiftyInsta : Instagram 非官方私有 API Swift

> 原文：<https://kalilinuxtutorials.com/swiftyinsta/>

[![SwiftyInsta : Instagram Unofficial Private API Swift](img/00b0b4b0420145cc626b0f069affbec3.png "SwiftyInsta : Instagram Unofficial Private API Swift")](https://1.bp.blogspot.com/-_vouunDVR-8/X6nCI0LlDXI/AAAAAAAAH9E/PoujqzEqHsEnhQqx6VK41rWe7U6gUlC7gCLcBGAsYHQ/s728/Insta%25281%2529.png)

Instagram 向开发者提供两种 API。 [Instagram API 平台](https://www.instagram.com/developer/)(功能极其有限，接近停产)，以及 [Instagram Graph API](https://developers.facebook.com/docs/instagram-api) ，仅针对*业务*和*创建者*账户。

然而， **Instagram** 应用依赖于第三种类型的 *API* ，即所谓的**私有 API** 或*非官方 API* ，而 [SwiftyInsta](https://github.com/TheM4hd1/SwiftyInsta) 则是为它们准备的一个 **iOS、macOS、tvOS 和 watchOS 客户端**，完全用 **Swift** 编写。你可以尝试为你的用户创造更好的 Instagram 体验，或者编写机器人来自动化不同的任务。

这些*私有 API* 不需要*令牌*或者 *app 注册*，但是它们没有被 Instagram】授权对外使用。使用这个你要自担风险。

**安装**

**Swift 包管理器(Xcode 11 及以上)**

*   从菜单中选择**/`Swift Packages`/`Add Package Dependency`/**`…`。
*   粘贴 **`https://github.com/TheM4hd1/SwiftyInsta.git`。**
*   按照步骤操作。

**可可布丁**

CocoaPods 是 Cocoa 项目的依赖管理器。您可以使用以下命令安装它:

**$ gem 安装 cocoapods**

要使用 CocoaPods 将 **SwiftyInsta** 集成到您的 Xcode 项目中，请在您的`Podfile`中指定:

**使用 _ 框架！

目标’<你的目标名字>做
吊舱【SwiftyInsta】，‘~>2.0’
结束**

然后，运行以下命令:

**$ pod 安装**

**SwiftyInsta** 依靠 [CryptoSwift](https://github.com/krzyzanowskim/CryptoSwift) 和 [keychain-swift](https://github.com/evgenyneu/keychain-swift) 。

**登录**

`**Credentials**`

```
// these need to be strong references.
self.credentials = Credentials(username: /* username */, password: /* password */, verifyBy: .text)
self.handler = APIHandler()
handler.authenticate(with: .user(credentials)) {
    switch $0 {
    case .success(let response, _):
        print("Login successful.")
        // persist cache safely in the keychain for logging in again in the future.
        guard let key = response.persist() else { return print("`Authentication.Response` could not be persisted.") }
        // store the `key` wherever you want, so you can access the `Authentication.Response` later.
        // `UserDefaults` is just an example.
        UserDefaults.standard.set(key, forKey: "current.account")
        UserDefaults.standard.synchronize()
    case .failure(let error):
        if error.requiresInstagramCode {
            /* update interface to ask for code */
        } else {
            /* notify the user */
        }
    }
}
```

一旦用户输入了双因素身份验证代码或质询代码，您只需

```
self.credentials.code = /* the code */
```

而前面的`authenticate(with: completionHandler:)`中的`completionHandler`会自动捕捉响应。

**`LoginWebViewController` ( > =仅限 iOS 12)**

```
let login = LoginWebViewController { controller, result in
    controller.dismiss(animated: true, completion: nil)
    // deal with authentication response.
    guard let (response, _) = try? result.get() else { return print("Login failed.") }
    print("Login successful.")
    // persist cache safely in the keychain for logging in again in the future.
    guard let key = response.persist() else { return print("`Authentication.Response` could not be persisted.") }
    // store the `key` wherever you want, so you can access the `Authentication.Response` later.
    // `UserDefaults` is just an example.
    UserDefaults.standard.set(key, forKey: "current.account")
    UserDefaults.standard.synchronize()
}
if #available(iOS 13, *) {
    present(login, animated: true, completion: nil) // just swipe down to dismiss.
} else {
    present(UINavigationController(rootViewController: login),  // already adds a `Cancel` button to dismiss it.
            animated: true,
            completion: nil)
}
```

或者使用`LoginWebView`实现自己的自定义`UIViewController`，使用`.webView(/* your login web view */)`将其传递给一个`APIHandler` `authenticate`方法。

`**Authentication.Response**`

如果您已经保存了用户的`Authentication.Response`:

```
// recover the `key` returned by `Authentication.Response.persist()`.
// in our example, we stored it in `UserDefaults`.
guard let key = UserDefaults.standard.string(forKey: "current.account") else { return print("`key` not found.") }
// recover the safely persisted `Authentication.Response`.
guard let cache = Authentication.Response.persisted(with: key) else { return print("`Authentication.Response` not found.") }
// log in.
let handler = APIHandler()
handler.authenticate(with: .cache(cache)) { _ in
    /* do something here */
}
```

**用途**

从您的`APIHandler`实例可以很容易地访问所有端点。

```
let handler: APIHandler = /* a valid, authenticated handler */
// for instance you can…
// …fetch your inbox.
handler.messages.inbox(with: .init(maxPagesToLoad: .max),
                       updateHandler: nil,
                       completionHandler: { _, _ in /* do something */ })
// …fetch all your followers.
handler.users.following(user: .me,
                        with: .init(maxPagesToLoad: .max),
                        updateHandler: nil,
                        completionHandler: { _, _ in /* do something */ })
```

此外，响应现在显示由 **API** 返回的`JSON`文件中包含的每个单个值:只需访问任意`ParsedResponse` `rawResponse`并开始浏览，或者坚持使用建议的附件(例如`User`的`username`、`name`等)。还有`Media`的`aspectRatio`、`takenAt`、`content`等。).