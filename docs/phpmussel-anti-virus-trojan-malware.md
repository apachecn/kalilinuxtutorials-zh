# PHPMussel:反病毒反木马反恶意软件解决方案

> 原文：<https://kalilinuxtutorials.com/phpmussel-anti-virus-trojan-malware/>

phpMussel 是共享主机环境的理想解决方案，在这种环境下通常不可能利用或安装传统的防病毒保护解决方案，它是一个 PHP 脚本，旨在根据 [ClamAV](https://www.clamav.net/) 和其他人的签名，**检测上传到您系统的文件中的特洛伊木马、病毒、恶意软件和其他威胁**。

**特性**

*   授权为 [GNU 通用公共许可证版本 2.0](https://github.com/phpMussel/phpMussel/blob/master/LICENSE.txt) (GPLv2)。
*   易于安装，易于定制，易于使用。
*   适用于任何安装了 PHP+PCRE 的系统，与操作系统无关(需要 PHP+PCRE)。
*   完全可根据您的需求进行配置。
*   共享托管服务的理想解决方案。
*   需要文件上传保护的论坛系统的理想解决方案。
*   不需要 shell 访问。
*   不需要管理权限。
*   CLI 模式可用。
*   良好、强大、稳定的支持基础。

**也读作-[Frida extract:基于 Frida.re 的 RunPE 提取工具](https://kalilinuxtutorials.com/fridaextract/)**

**如何安装**

**手动安装(用于 WEB 服务器)**

1.  在您阅读本文时，我假设您已经下载了该脚本的一个存档副本，解压缩了它的内容并把它放在了您的本地机器上。从这里开始，您需要确定在主机或 CMS 上的什么位置放置这些内容。一个像`**/public_html/phpmussel/**`或类似的目录(虽然，你选择哪个并不重要，只要它是安全的和你满意的)就足够了。*开始上传之前，请继续阅读..*
2.  将`**config.ini.RenameMe**`重命名为`**config.ini**`(位于`**vault**`内)，并且可选地(强烈建议高级用户使用，但不建议初学者或没有经验的用户使用)，打开它(该文件包含了 phpMussel 可用的所有指令；在每个选项的上方应该有一个简短的注释，描述它的作用和用途。根据适合您的特定设置，调整这些指令。保存文件，关闭。
3.  将内容(phpMussel 及其文件)上传到您之前决定的目录中(您不需要包含`***.txt**` **/** `***.md**`文件，但最重要的是，您应该上传所有内容)。
4.  将`**vault**`目录 CHMOD 为“755”(如果有问题可以试试“777”)；但是这不太安全)。通常，存储内容的主目录(您之前选择的目录)可以保持不变，但是如果您过去在系统上有权限问题，应该检查 CHMOD 状态(默认情况下，应该是类似“755”)。简而言之:为了让这个包正常工作，PHP 需要能够读写`**vault**`目录中的文件。如果 PHP 不能写入`**vault**`目录，许多事情(更新、日志记录等)将无法实现，如果 PHP 不能从`**vault**`目录读取，软件包将根本无法工作。然而，为了最佳的安全性，`**vault**`目录不能被公开访问(如果`**vault**`目录可以被公开访问，敏感信息，如`**config.ini**`或`**frontend.da**t`包含的信息，可能会暴露给潜在的攻击者)。
5.  安装您需要的任何签名。*见:[安装签名](https://github.com/phpMussel/phpMussel/blob/master/_docs/readme.en.md#INSTALLING_SIGNATURES)。*
6.  接下来，您需要将 phpMussel“挂钩”到您的系统或 CMS。有几种不同的方法可以将 phpMussel 之类的脚本“挂钩”到您的系统或 CMS，但最简单的方法是使用`**require**`或`**include**`语句将脚本包含在您的系统或 CMS 的核心文件(当有人访问您网站上的任何页面时，该文件通常都会被加载)的开头。通常，这将是存储在诸如`**/includes**`、`**/assets**`或`**/functions**`之类的目录中的东西，并且通常会被命名为类似于`**init.php**`、`**common_functions.php**`、`**functions.php**`或类似的东西。你必须找出哪一个文件适合你的情况；如果您自己在确定这一点时遇到困难，请访问 GitHub 上的 phpMussel 问题页面或 phpMussel 支持论坛寻求帮助；有可能我或另一个用户可能对你正在使用的 CMS 有经验(你需要让我们知道你正在使用哪个 CMS)，因此，可能能够在这方面提供一些帮助。为此[要使用`**require**`或`**include**` ]，将下面的代码行插入到核心文件的最开始，用`**loader.php**`文件的确切地址(本地地址，不是 HTTP 地址；它看起来类似于前面提到的保险库地址)。

`**<?php require '/user_name/public_html/phpmussel/loader.php'; ?>**`

保存文件，关闭，重新加载。

—或者说—

如果您使用的是 Apache 服务器，并且您可以访问`**php.ini**`，那么无论何时发出任何 PHP 请求，您都可以使用`**auto_prepend_file**`指令来前置 phpMussel。类似于:

`**auto_prepend_file = "/user_name/public_html/phpmussel/loader.php"**`

或者这个在`.**htaccess**` 文件中:

`**php_value auto_prepend_file "/user_name/public_html/phpmussel/loader.php"**`

1.  至此，大功告成！但是，您可能应该测试一下，以确保它工作正常。要测试文件上传保护，尝试通过您常用的基于浏览器的上传方法将`**_testfiles**`下的包中包含的测试文件上传到您的网站。(确保您已经将`**phpmussel*.*db**`签名文件包含在您的`**Active**`设置中，以便触发测试文件)。如果一切正常，phpMussel 应该会显示一条消息，确认上传被成功阻止。如果什么都没有出现，说明有些东西工作不正常。如果您正在使用任何高级功能，或者如果您正在使用该工具可能的其他类型的扫描，我建议您尝试一下，以确保它也能按预期工作。

**手动安装(用于 CLI)**

1.  在您阅读本文时，我假设您已经下载了该脚本的一个存档副本，解压缩了它的内容并把它放在了您的本地机器上。当您确定对为 phpMussel 选择的位置感到满意时，请继续。
2.  phpMussel 需要在主机上安装 PHP 才能执行。如果您的机器上没有安装 PHP，请按照 PHP 安装程序提供的说明在您的机器上安装 PHP。
3.  可选地(强烈建议高级用户使用，但不建议初学者或没有经验的用户使用)，打开`**config.ini**`(位于`**vault**`内)–该文件包含 phpMussel 可用的所有指令。在每个选项上面应该有一个简短的注释，描述它的作用和用途。根据您的具体设置，调整您认为合适的选项。保存文件，关闭。
4.  或者，您可以通过创建一个批处理文件来自动加载 PHP 和 phpMussel，从而使在 CLI 模式下使用 phpMussel 变得更加容易。为此，打开一个纯文本编辑器，如 Notepad 或 Notepad++，键入 PHP 安装目录中的`**php.exe**`文件的完整路径，后跟一个空格，再后跟 phpMussel 安装目录中的`**loader.php**`文件的完整路径，将带有`**.bat**`扩展名的文件保存在一个容易找到的位置，然后双击该文件以在将来运行 phpMussel。
5.  安装您需要的任何签名。*见:[安装签名](https://github.com/phpMussel/phpMussel/blob/master/_docs/readme.en.md#INSTALLING_SIGNATURES)。*
6.  至此，大功告成！但是，您可能应该测试一下，以确保它工作正常。要测试 phpMussel，运行 phpMussel 并尝试扫描软件包提供的`**_testfiles**` 目录。

**用 COMPOSER 安装**

phpMussel 向 Packagist 注册，因此，如果您熟悉 Composer，您可以使用 Composer 来安装 phpMussel(尽管您仍然需要准备配置、权限、签名和钩子；请参见“手动安装(对于 web 服务器)”步骤 2、4、5 和 6。

`**composer require phpmussel/phpmussel**`

**安装签名**

从 v1.0.0 开始，phpMussel 包中不再包含签名。phpMussel 需要签名来检测特定的威胁。安装签名有 3 种主要方法:

1.  使用前端更新页面自动安装。
2.  使用“SigTool”生成签名并手动安装。
3.  从“phpMussel/Signatures”下载签名并手动安装。

##### 使用前端更新页面自动安装。

首先，您需要确保前端已启用。*参见:[前端管理](https://github.com/phpMussel/phpMussel/blob/master/_docs/readme.en.md#SECTION4)。*

然后，您需要做的就是转到前端更新页面，找到必要的签名文件，使用页面上提供的选项，安装并激活它们。

##### 使用“SigTool”生成签名并手动安装。

*参见: [SigTool 文档](https://github.com/phpMussel/SigTool#documentation)。*

##### 从“phpMussel/Signatures”下载签名并手动安装。

首先，进入 [phpMussel/Signatures](https://github.com/phpMussel/Signatures) 。该存储库包含各种 GZ 压缩的签名文件。下载需要的文件，解压，将解压后的文件复制到`**/vault/signatures**`目录进行安装。在 phpMussel 配置中列出复制文件的名称到`**Active**`指令来激活它们。

[**Download**](https://github.com/phpMussel/phpMussel)