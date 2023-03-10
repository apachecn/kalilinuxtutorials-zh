# Guardedbox:用于安全存储和秘密共享的在线客户端管理器

> 原文：<https://kalilinuxtutorials.com/guardedbox/>

[![Guardedbox : Online Client-Side Manager For Secure Storage & Secrets Sharing](img/da365adc276ed6be149333d7f18305a9.png "Guardedbox : Online Client-Side Manager For Secure Storage & Secrets Sharing")](https://1.bp.blogspot.com/-wmEVvNv9XDo/XsyoX7ZJ5II/AAAAAAAAGfY/kK7ch6qa44gFJ7Z-qxjle4UV72fhEnABgCLcBGAsYHQ/s1600/guardedbox%25281%2529.png)

GuardedBox 是一个用于安全存储和秘密共享的开源在线客户端管理器。

它允许用户将秘密上传到中央服务器，并在任何时间和任何地点检索它们。它还允许用户单独或通过群组与其他用户分享他们的秘密。

秘密存储在加密的服务器端。JavaScript 代码在客户端执行加密。它基于 ECC-Curve25519 非对称加密和 AES256-GCM 对称加密。ECC 密钥对是在注册和登录过程中通过 PBKDF2 从用户登录凭证中生成的。

服务器知道每个用户的公钥。任何用户都可以检索任何其他用户的公钥，并为她加密一个秘密，只有该用户能够使用从其凭证生成的自己的私钥来解密它。这都是由 JavaScript 代码在客户端完成的，最大限度地减少了对服务器的信任，并在用户之间使用端到端(E2E)加密。

服务器在登录过程中不会收到用户密码。相反，加密挑战涉及使用基于 ECC-EDDSA 和 ED25519 的数字签名。当用户想要执行登录时，服务器向他发送一个挑战。用户必须用自己的私钥签名，然后将其发送回服务器。同样，这都是由 JavaScript 代码在客户端完成的。

**也可阅读-[say cheese:通过链接](https://kalilinuxtutorials.com/saycheese/)抓取目标的网络摄像头照片 **

**在线服务**

GuardedBox 在线部署。官方详细信息、通知和沟通渠道、版本信息(和 changelog)和文档以及在线服务的参考资料可从以下网址获得:

*   [https://www . guarded box . es](https://www.guardedbox.es)(西班牙语)
*   https://www.guardedbox.eu (英文–即将发布)

它对任何人都是免费服务:个人、公司和组织！

**技术文档&本地部署**

这是一个 JavaScript 和 Java/Spring-Boot 项目:

*   后端基于 Java/Spring-Boot。请参见“pom.xml”文件和“java”文件夹(在“src/main”内)。
*   前端基于使用 ReactJS 的 JavaScript。参见“前”文件夹(在“src/main”内)。
*   数据库是 MySQL。请参见“sql”文件夹(在“src/main”中)。

该项目可以通过 Maven 在其根目录下使用以下命令来构建:

**mvn 全新安装**

一个 JAR 文件(jar)将在“目标”文件夹中生成。

可以从项目根目录使用以下命令运行该项目:

**Java-jar target/guarded box-1 . 0 . 0 . jar–spring . config . location = file:。/config-example/应用程序.属性**

它需要一个 MySQL 数据库实例，其模式在文件“sql/guardedbox.sql”中描述(在“src/main”中)。

它还需要一个外部属性文件(前面命令中的“application.properties”引用)。在“config-example”文件夹中可以找到一个属性文件的示例，以及一个用于 HTTPS 的服务器数字证书。

该项目也被记录在案。该映像是在 Maven 生命周期中构建的。可以使用项目根目录中的以下命令在本地运行该容器:

**坞站-合成**

确保秘密路径(指向属性文件)在“docker-compose.yml”文件中是正确的。

该图片可从 Docker Hub 获得:

*   [https://hub . docker . com/r/S3 curitybug/guards box/](https://hub.docker.com/r/s3curitybug/guardedbox/)

如上所述，它仍然需要一个 MySQL 数据库实例和一个属性文件，以及一个用于 HTTPS 的服务器数字证书。

[**Download**](https://github.com/s3curitybug/guardedbox)