# MailRipV2:改进的 SMTP 检查器/ SMTP 破解程序，具有代理支持、收件箱测试和更多功能

> 原文：<https://kalilinuxtutorials.com/mailripv2/>

[![](img/ae515d44cc3df4a53bd045ca874bbfa6.png)](https://1.bp.blogspot.com/-Fa7Ekuzrb9Y/YUyDmCMGQ1I/AAAAAAAAK7Y/0rz8Ndh6dmM8vB2aHRFPlOv9ZT78TCSUwCLcBGAsYHQ/s728/Mail.Rip-Improved-SMTP-Checker-SMTP-Cracker%2B%25281%2529.png)

**mairip v2**是用 Python 3.8 编写的 SMTP 检查器/ SMTP 破解程序。使用“smtplib”，它允许您检查有效的 SMTP 登录的公共邮件传递组合列表。它有**包括字典和列表，包含常见的电子邮件提供商的详细信息以及 SMTP 服务器最常用的端口。**如果有数据丢失，使用“DNS python”**在 MX 记录中查找未知的 SMTP 主机**。

而且，邮件。Rip V2 附带了 **SOCKS-proxy 支持**，包括一个 **proxy-scraper 和 checker** 功能。如果代理支持被激活，检查器/破解器从公共在线资源中抓取 SOCKS4 或 SOCKS5 代理，并将检查结果，然后..工作中的**代理**将被随机使用**。并且可以随时通过编辑 *library.json* 来添加新的源代码。**

 **最后但同样重要的是，邮件。Rip V2 包括一个**电子邮件发送测试/收件箱检查**来查找 SMTP 登录。对于每个有效的组合，它会尝试发送一封包含找到的 SMTP 登录名的纯文本电子邮件。所有测试邮件都会发送到您自己自定义的接收地址，测试邮件的内容是随机生成的。模板也可以在“library.json”中编辑。

**邮件。Rip V2 功能齐全，随时可用！**

**如何使用邮件。瑞普·V2**

**邮件。Rip V2** 已经用 Python 3.8 编写并测试过了。只要安装了 Python 和所有依赖项，它就可以在任何操作系统上运行。
只要按照下面的步骤去做就行了！

**安装需要的 Python 模块**

所有需要的 Python 模块/包都列在 txt-file*requirements . txt*中。为了便于安装，请键入:

**pip 3 install-r requirements . txt**

安装任何缺失的依赖项可能需要一些时间。请耐心点。

**启动检查器/破解器**

安装完所有依赖项后，您就可以启动 Mail 了。Rip V2 与:

**python3 MailRipV2.py**

不需要额外的论证。在启动 checker / cracker 之前，您只需将 combofile 复制到相同的目录中。启动后，只需按照步骤(1)至(4)。有关更多信息，请参见“主菜单中的选项”。

请注意:
您的 combofile 需要用 utf-8 编码！任何其他编码都可能导致错误。

主菜单中的 **选项**

**设置默认值**

使用此选项编辑邮件的默认值。撕裂 V2。您可以在此编辑以下内容:

*   用于检查/破解的线程数量。
*   连接的默认超时。
*   取消/激活电子邮件域的黑名单检查。
*   将您的电子邮件地址设置为测试邮件的接收者。

**取消/激活代理支持**

此选项允许您激活或停用代理支持。如果激活，您将被要求使用代理类型。只需输入*袜 4* 或*袜 5* 即可。然后刮刀自动启动。你可以通过编辑 *library.json* 来添加更多的源码。抓取完成后，会询问您是否要跳过检查器。不要跳过检查，除非你真的，真的需要立即开始攻击。

**加载组合**

选项#3 启动**组合加载器**。输入组合文件的名称，例如: *combos.txt* 。文件中的所有连击都将被加载并准备攻击。因此，Comboloader 执行以下步骤:

*   替换除“:”以外的任何其他分隔符。
*   组合中的电子邮件地址通过使用正则表达式的格式进行验证。
*   对于已验证的电子邮件地址，将根据包含在 *library.json* 中的黑名单检查该域。
*   然后，加载器检查它之前是否已经加载了给定的组合(重复检查)。

所有通过检查的连击将被载入攻击并保存到一个名为 *targets.txt* 的 txt 文件中。请确保您的组合文件使用 utf-8 编码，否则可能会出错。

**开始攻击**

这个很明显。

**各种**

有关任何提示、提示和其他信息，请参见以下部分。

**SMTP 破解/ SMTP 检查流程**

邮件。Rip V2 使用 smtplib 进行检查/破解过程。这个“魔术”是这样完成的:

1.  SMTP 破解程序/ SMTP 检查程序从加载的列表中读取下一个组合。
2.  它在“smtphost”字典中查找要攻击的 SMTP 主机的电子邮件域。
3.  对于未知主机，它会尝试从电子邮件域的 MX 记录中获取地址。
4.  在 MX 记录中找到的主机的连接端口是在试错过程中使用最常见的端口进行搜索的。
5.  然后，它建立到 SMTP 主机的连接(尝试 SSL 和非 SSL 以及 TLS)
6.  并使用目标电子邮件地址和组合中的给定密码发送登录数据。
7.  如果登录被拒绝，破解者/检查者将尝试使用用户 ID(没有@…)和密码登录。
8.  如果登录数据有效，所谓的“hit”将被保存到 txt 文件中。
9.  在最后的邮件中。Rip V2 将尝试使用找到的 SMTP 向您发送测试消息。

为了获得最佳效果，每个用户都应该在启动 Mail 之前编辑 *library.json* 中的主机信息。第一次撕开 V2。在 combolist 中添加最常见的电子邮件提供商的数据总是会加快检查/破解过程。并且它可能会在服务器端产生较少的安全标志。

改善结果的其他方法有:取消代理支持并调整默认值。事实上，**建议让代理支持保持禁用状态。**不使用 proxys，您将获得更好的结果——对于检查器和收件箱检查。

**【邮件投递测试注意事项(收件箱检查)**

邮件内容是使用“library.json”中的模板随机生成的。根据需要编辑这些模板。不时地编辑模板将提供更高的成功率。

请始终注意，由于多种原因，电子邮件传递测试可能会返回假阴性结果。它只是确认给定的 SMTP 主机可以用任何软件发送电子邮件。知名的电子邮件提供商可能会阻止或限制对 SMTP 帐户的访问，尤其是像 mail 这样的工具。撕裂 V2。此外，免费代理可能会被列入黑名单，以及某些 SMTP 帐户本身。您应该在攻击结束后再次测试传送测试失败的有效登录。

**黑名单检查笔记**

*library.json* 包含一个电子邮件域黑名单。已经有超过 500 个垃圾邮件域被加入其中。但也有一些非常受欢迎的电子邮件提供商。当你检查或破解 mailpass 组合列表时，这些电子邮件提供商通常是在浪费时间。有时他们只是阻止访问，有时他们要求进一步验证。

如果您也想攻击这些提供商，请根据您的需要编辑黑名单。

[**Download**](https://github.com/DrPython3/MailRipV2)**