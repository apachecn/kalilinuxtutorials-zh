# Aduket:直接的 HTTP 客户端测试，包括断言

> 原文：<https://kalilinuxtutorials.com/aduket/>

[![Aduket : Straight-forward HTTP Client Testing, Assertions Included](img/38956f08bb16a48a9f5dc7305d4cd8e8.png "Aduket : Straight-forward HTTP Client Testing, Assertions Included")](https://1.bp.blogspot.com/-nFxWEngGXHI/XkcGW7OYP0I/AAAAAAAAE-g/GblBQ8VtSJsSrNXd0Y3FekkPpa8jPw5jACLcBGAsYHQ/s1600/Aduket.gif)

**Aduket** 直接的 HTTP 客户端测试，包含断言。简单的`**httptest.Server**`包装器，上面有一点请求记录器的味道。不需要特殊的 DSL，不需要学习复杂的 API。只需创建一个服务器，像 **Hadouken** 一样发出请求，然后断言它。

**待办事项**

*   增加对 MultiRouteServer 路由的每个 RequestRecorder 的访问支持
*   提取请求()。正文请求记录器。将逻辑主体绑定到 CustomBinder
*   将徽章添加到 README.md
*   添加用于测试 API 超时的 NewServerWithTimeout
*   http。可以实现 RoundTripper 接口来模仿任意 URL
*   添加多个请求断言逻辑
*   添加示例用法
*   添加文档
*   向断言添加有意义的错误消息
*   向 NewServer 添加响应头
*   添加请求标头断言
*   向服务器添加多个路由注册

**也读作-[IPv6 tools:一个健壮的模块化框架](https://kalilinuxtutorials.com/ipv6tools/)**

**执照**

版权所有 2020 StreetByters 社区

根据 Apache 许可证 2.0 版许可(“许可证”)；除非符合许可证的规定，否则您不得使用本文件。您可以从以下网址获得许可证的副本

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

除非适用法律要求或书面同意，根据许可证分发的软件按“原样”分发，没有任何种类的明示或暗示的保证或条件。请参阅许可证，了解许可证下管理权限和限制的特定语言。

[**Download**](https://github.com/streetbyters/aduket)