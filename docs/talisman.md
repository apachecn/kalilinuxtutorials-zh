# Talisman:通过挂钩 Talisman 来验证传出的变更集是否有可疑之处

> 原文：<https://kalilinuxtutorials.com/talisman/>

[![](img/6709dbc817e760e2e315e192fbf155d7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhxgVK24vo1rGfy2BDrB24ywC0Q1PJm3AHRanO6V6rnca0VZ1xQhboMPZ2fis92Ye_EQ6SlriAxxvmFdv4VQR6ev1oskoo27_XrFGTNJkFdbcyB6cL66HTkbVSJ81NF-S70pKUBtjHYGsh_jkoBRv9m42rWfpWqagh_pcm_MsQ0Y-GmTZNnKh2DsMJK/s728/talisman%20logo%20(1).png)

**Talisman** 是一个工具，它给你的存储库安装一个钩子，确保潜在的秘密或敏感信息不会离开开发者的工作站。

它为看起来可疑的东西验证传出的变更集——比如潜在的 SSH 密钥、授权令牌、私有密钥等。

# 安装

Talisman 支持 MAC OSX、Linux 和 Windows。

Talisman 可以通过以下方式安装和使用:

*   作为 git 钩子作为全局 git 钩子模板和 CLI 实用程序(用于 git 回购扫描)
*   作为一个 git 挂钩到单个 git 存储库

Talisman 可以在 git 存储库上设置为预提交或预推送挂钩。

找到下面的说明。

免责声明:Talisman 无法检测到通过 git 存储库中的强制推送悄悄进入的秘密。强制推送以其自身的方式被认为是臭名昭著的，我们建议 git 存储库管理员应用适当的措施来授权这样的活动。

## 【推荐方法】

## 作为全局钩子模板安装

我们建议将 Talisman 安装为一个**预提交 git 挂钩模板**，因为这将使 Talisman 不仅存在于您现有的 git 存储库中，还存在于您‘初始化’或‘克隆’的任何新存储库中。

*   在您的终端上运行以下命令，在$HOME/下载并安装二进制文件。护身符/垃圾桶

作为提交前挂钩:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/install . bash>/tmp/install _ talisman . bash&&/bin/bash/tmp/install _ talisman . bash**

运筹学

作为预推钩:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/install . bash>/tmp/install _ talisman . bash&&/bin/bash/tmp/install _ talisman . bash 预推**

*   如果您的`**$PATH**`中没有设置 TALISMAN_HOME，将会询问您一个合适的位置来设置它。选择您在机器上设置配置文件源的选项号。

记得执行路径文件上的*源*或者重启你的终端。如果您选择稍后设置`$PATH`，请导出 TALISMAN_HOME=$HOME/。通往小路的护身符/垃圾箱。

*   选择一个基础目录，Talisman 应该在这个目录中扫描所有 git 存储库，并设置一个 git 挂钩(预提交或预推送，如步骤 1 中所选)作为符号链接。这个脚本不会破坏预先存在的钩子。如果你有现成的钩子，想办法把护身符拴在上面。

*   您可以在执行安装之前使用基目录的路径设置 SEARCH_ROOT 环境变量，这样您就不需要在安装过程中手动输入它

### 处理现有吊钩

Talisman 在全球范围内的安装不会破坏存储库上已经存在的钩子。如果安装脚本找到任何现有的挂钩，它只会在控制台上显示出来。
为了实现运行多个钩子，我们建议(但不限于)使用以下两种工具

*   预提交(Linux/Unix)

使用预提交工具管理所有现有的钩子和 Talisman。在建议中，它会提示将下面的代码包含在。预提交配置文件

**repo:local
hooks:
id:TALISMAN-pre commit
name:TALISMAN
entry:bash-c ' if[-n " $ { TALISMAN _ HOME:-} "]；然后$ { TALISMAN _ HOME }/TALISMAN _ hook _ script 预提交；else echo“护身符不存在。考虑从 https://github.com/thoughtworks/talisman 安装。如果您已经安装了 talisman，请确保 TALISMAN_HOME 变量设置为 talisman_hook_script 所在的位置，例如 TALISMAN_HOME=${HOME}/。护身符/bin”；fi '
language:system
pass _ filenames:false
types:[text]
verbose:true**

*   Husky (Linux/Unix/Windows)

husky 是一个用于管理 git 挂钩的 npm 模块。为了使用哈士奇，请确保您已经将 TALISMAN_HOME 设置为`**$PATH**`。

*   **现有用户**

如果您已经在使用 husky，请在 package.json 中将以下行添加到 husky 预提交中

Windows

**" bash-c ' \ " % TALISMAN _ HOME % \ $ { TALISMAN _ BINARY _ NAME } \ "–git hook 预提交' "**

Linux/Unix

**$ TALISMAN _ HOME/TALISMAN _ hook _ script 预提交**

*   **新用户**

如果您想将 husky 与 talisman 一起使用，请将下面的代码片段添加到您的 json 包中。

Windows

{
"husky": {
"hooks": {
"预提交":" bash-c ' \ " % TALISMAN _ HOME % \ $ { TALISMAN _ BINARY _ NAME } \ "–git hook 预提交' "& &"其他-脚本"
}
}

Linux/Unix

**{
"哈士奇":{
"钩子":{
"预提交":" $ TALISMAN _ HOME/TALISMAN _ hook _ script 预提交"& &"其他-脚本"
}
}
}**

## 安装到单个项目

**#下载 talisman 安装程序脚本
curl https://thoughtworks.github.io/talisman/install.sh>~/install-talisman . sh
chmod+x ~/install-talisman . sh**

作为预推挂钩
#~/install-talisman.sh
或预提交挂钩
#~/install-talisman.sh 预提交

### 处理现有吊钩

护身符将需要与任何现有的 git 挂钩链接。您可以使用预提交 git 钩子框架来处理这个问题。

将这个添加到您的`**.pre-commit-config.yaml**`(确保更新`**rev**`以指向一个真正的 git 修订版！)

https://github.com/thoughtworks/talisman
rev:" #更新我！
钩子:
或者`commit`或者`push`支持
id:talisman-commit
id:talisman-push

# 升级

从 v0.4.4 版本开始，Talisman **在钩子被调用时(在预提交/预推送时，根据设置)自动将二进制文件更新到最新版本。所以，只要坐好，放松，继续使用最新的护身符，没有任何额外的努力。**

可以设置以下环境变量:

*   TALISMAN_SKIP_UPGRADE:如果你想跳过自动升级检查，设置为 true。默认值为 false
*   TALISMAN _ UPGRADE _ CONNECT _ time out:取消升级前的最大连接超时(秒)。默认值为 10 秒。

如果您需要手动升级，以下是步骤:
【推荐】将 Talisman 二进制文件和 hook 脚本更新到最新版本:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/update _ talisman . bash>/tmp/update _ talisman . bash&&/bin/bash/tmp/update _ talisman . bash**

通过执行以下命令仅更新 Talisman 二进制文件:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/update _ talisman . bash>/tmp/update _ talisman . bash&&/bin/bash/tmp/update _ talis**man . bash talisman-binary

# 护身符在行动

安装成功后，Talisman 将在每次提交或推送(安装时选择)前自动检查明显的秘密。如果检测到任何安全漏洞，talisman 将显示错误的详细报告:

$ git push
talisman report:
+————————————————————————————————————-
——**| file | errors |
+————————————————————————————————————————————————-+
| danger . PEM |文件名" danger.pem" |
| |检查失败+.PEM $ |
+————————————————————————+
| danger . PEM |期望文件不包含十六进制编码的文本，例如:|
| | awsSecretKey = c 64 e 8 c 79 aa cf 5 DDB 02 f 1274 db 2d 973 f 363 f 4 f 553 ab 1692d 8d 203 B4 cc 09692 f 7**

在上面的示例中，由于以下原因，文件 *danger.pem* 被标记为安全漏洞:

*   文件名与预先配置的模式之一匹配。
*   该文件包含一个 awsSecretKey，Talisman 会对其进行扫描和标记

如果你已经安装了 Talisman 作为预提交钩子，它将在每次提交时只扫描 *diff* 。这意味着它将只报告文件中被更改的部分的错误。

如果你已经安装了 Talisman 作为预推挂钩，它将扫描整个文件中的变化。如上所述，建议你使用 Talisman 作为**预提交钩子**。

## 验证

以下检测器针对变更集执行，以检测机密/敏感信息:

*   **编码值**–扫描 Base64、hex 等编码的秘密。
*   **文件内容**–扫描文件中可能是潜在机密或密码的可疑内容
*   **文件大小**–扫描可能包含密钥或其他秘密的大文件
*   **熵**–扫描可能包含密码的高熵内容
*   **信用卡号码**–扫描可能是潜在信用卡号码的内容
*   **文件名**–扫描文件名和扩展名，这些文件名和扩展名可能表明它们可能包含秘密，如密钥、凭证等。

## 忽略文件

如果你*真的*确定你想要推送那个文件，你可以把它配置到项目根目录下的`**.talismanrc**`文件中。Talisman 将在 Talisman 错误报告后立即在控制台上打印忽略失败文件所需的内容:

如果您绝对确定要忽略 talisman 检测器中的上述文件，请考虑将以下格式粘贴到。项目根
中的 talismanrc 文件 fileignoreconfig:

*   **文件名:danger.pem
    校验和:cf 97 Abd 34 cebe 895417 EB 4d 97 FBD 7374 aa 138 dcb 65 B1 Fe 7 f 6 b 6 cc 1238 aa F4 d 48
    忽略 _ 检测器:[]**

在`**.talisman**rc`文件中输入该值将确保只要校验和与`**checksum**`字段中提到的值匹配，Talisman 就会忽略`**danger.pem**`文件。

### 互动模式

**仅适用于非 Windows 用户**

如果继续复制内容太麻烦的话。每当你遇到 talismanrc 的错误时，你可以启用交互模式，让 talismanrc 帮助你提示添加要忽略的文件。只需遵循简单的步骤:

*   打开设置了环境变量的 bash 概要文件。bashrc，。bash_profile，。简档或任何其他位置)
*   您将在`**# >>> talisman >>>**`下看到`**TALISMAN_INTERACTIVE**`变量
*   如果尚未设置为真，添加`**export TALISMAN_INTERACTIVE=true**`
*   不要忘记保存和源文件

就是这样！每次 Talisman hook 在预推送/预提交期间发现错误时，只要按照 Talisman 建议的说明进行操作即可。注意不要在没有验证内容的情况下忽略文件。你必须确信没有秘密被泄露出去。

### 忽略特定的探测器

以下是可配置到`**.talismanrc**`文件中的各种字段的详细描述:

*   `**filename**`:该字段应该提到完全限定的文件名。
*   `**checksum**`:该字段应始终具有 Talisman 在上面显示的消息中指定的值。如果在任何时候，一个新的变化，该文件，这将导致一个新的校验和和 Talisman 将扫描文件再次为任何潜在的安全威胁。
*   `**ignore_detectors**`:该字段将禁用特定文件的特定检测器。例如，如果您的`**init**-**env.sh**`文件名触发了一个警告，您只能禁用此警告，同时在其他事情出错(例如文件内容)时仍会收到警告:

f **ileignoreconfig:
文件名:测试
允许 _ 模式:[key]
允许 _ 模式:
关键字
通过**

注意:这里 init-env.sh 的文件名和文件大小检测器都被忽略，但是文件内容检测器仍然会在`**init-env.sh**`激活

此刻，你可以忽略

*   `**filecontent**`
*   `**filename**`
*   `**filesize**`

### 忽略特定关键字

因为您的某些文件可能包含不一定与机密相关的关键字，如`**key**`或`**pass**`，所以您可能希望忽略这些关键字以减少误报的数量。这可以通过使用文件级和/或存储库级的`**allowed_patterns**`字段来实现:

**fileignoreconfig:
文件名:测试
allowed _ patterns:[key]
allowed _ patterns:
关键字
pass**

在前面的例子中，`**test**`文件中允许使用`**key**`，在存储库级别允许使用`**keyword**`和`**pass**`。

`**allowed_patterns**`字段也支持 Golang 正则表达式。下面是一个 Golang 正则表达式有用的简单代码示例:

**export AWS _ ACCESS _ KEY _ ID = akia io 5 fodnn 7 example
export AWS _ ACCESS _ KEY _ ID = $(vault read-field = value path/to/AWS-ACCESS-KEY-ID)**

默认情况下，Talisman 会对两条线发出警报。在第二行中，我们从 Hashicorp Vault 中提取 AWS 访问密钥 ID，这不会将秘密暴露给代码。如果这种用法在您的代码中很常见，您可能希望告诉 Talisman 在使用保险库时不要发出警报。这可以通过以下配置实现:

a**allowed _ patterns:
export \ AWS[\ w]*KEY[\ w]*=。*金库\读取。***

### 忽略多个相同类型的文件(带通配符)

您可以选择忽略某一类型的所有文件，因为您知道它们将始终是安全的，并且您不希望 Talisman 扫描它们。

步骤:

*   为要忽略的文件设置通配符格式。例如，`***.lock**`
*   使用校验和计算器输入模式并获得集体校验和。例如，`**talisman --checksum="*.lock"**`
*   将控制台上打印的文件配置块复制到。护身符档案。

如果任何文件被修改，talisman 将再次扫描文件，除非您重新计算新的校验和并将其替换。护身符档案。

### 通过指定语言范围忽略文件

您可以通过在 talismanrc 中指定项目的语言范围来选择忽略文件。

**scopeconfig:
范围:go
范围:节点
范围:图像**

Talisman 配置为根据指定的范围忽略某些文件。例如，在 scopeconfig 中提到节点范围将阻止 talisman 扫描诸如 yarn.lock 或 package-lock.json 之类的文件。

您可以指定多个范围。

目前。talismanrc 只支持 scopeconfig 对 go、node 和 images 的支持。其他范围将很快添加。

### 自定义搜索模式

您可以指定要在当前存储库中查找的自定义正则表达式模式

**自定义 _ 图案:
图案 1
图案 2**

***注**:的用法。talismanignore 已被弃用。文件。护身符代替它是因为:*

*   。talismanrc 有更清晰的 yaml 格式
*   它还带来了更安全的做法，对具有潜在敏感值的文件的每次修改都要进行审查
*   新格式还带来了可扩展性，以引入新的可用功能。继续关注更多

## 配置严重性阈值

每个验证都与一个严重性相关联

*   低的
*   中等
*   高的

您可以在您的。护身符:

**阈值:中等**

这将报告所有中严重性问题和更高严重性问题(低于阈值的潜在风险将在警告中报告)

*   可以在此配置文件中找到所有风险及其严重级别的列表。
*   默认情况下，阈值设置为低。
*   您添加的任何自定义搜索模式都被视为高严重性。

## 配置自定义严重性

您可以在中自定义 Talisman 提供的检测器的安全级别。护身符文件:

**自定义 _ 严重性:
检测器:base64 内容
严重性:中
检测器:hex 内容
严重性:低**

通过使用自定义的严重性和严重性阈值，Talisman 可以配置为仅根据您的环境发出重要警报。这有助于减少误报的数量。

## 作为 CLI 实用程序的 Talisman

如果您在命令行上执行`**talisman**`，您将能够查看您可以传递的所有参数选项

**-c，–校验和字符串校验和计算器计算校验和并给出建议。talismarc 格式
-d，–debug 启用调试模式(警告:非常详细)
-g，–git hook 字符串预推送或预提交(默认为“预推送”)
–ignore history 扫描器扫描当前头上的所有文件，不会扫描 git 提交历史记录
-i，–交互式交互式更新 talismarc(仅与-g/–git hook 一起使用才有意义)
-p，–要扫描的文件的模式字符串模式(类似 glob)(忽略 githooks)
-r，–r –scan scanner 扫描 git 提交历史以寻找潜在的秘密
-w，–scanwitHtml 生成 html 报告(确保您已经安装了 talisman_html_report 以使用它，如自述文件中所述)
-v，–version 显示 talisman 的当前版本**

### 对话方式

当您经常有太多的文件被 talisman hook 标记时，您知道应该可以签入，您可以使用此功能让 talisman 为您简化这个过程。互动模式将允许 Talisman 提示您直接添加您想要忽略的文件。直接从命令提示符。要启用这个特性，您需要在 bash 文件中将 TALISMAN_INTERACTIVE 变量设置为 true。

您可以通过以下两种方式之一在交互模式下调用 talisman:

*   打开你的 bash 文件，并添加
    `**export TALISMAN_INTERACTIVE=true**`
    不要忘记为变量提供 bash 文件的源代码，以使变量生效！
*   或者，您也可以通过使用 CLI 实用程序
    (用于使用预提交钩子)
    `**talisman -i -g pre-commit**`来调用交互模式

*注意*:如果使用 IDE 的版本控制集成进行 git 操作，这个特性将不起作用。您仍然可以使用建议的文件名和校验和来输入。手动创建护身符文件。

### Git 历史扫描仪

您现在可以从 CLI 执行 Talisman，并可能将它添加到您的 CI/CD 管道中，以扫描您的存储库的 git 历史来查找任何敏感内容。这包括扫描中列出的文件。护身符档案也是。

**步骤**:

*   进入要扫描的 git 目录路径`**cd <directory to scan>**`
*   运行扫描命令`**talisman --scan**`

*   运行该命令将在当前目录的根目录下创建一个名为 *talisman_reports* 的文件夹，并将报告文件存储在那里。
*   您也可以通过提供一个附加参数来指定报告的位置，如*–报告目录*或*–研发*T5，例如`**talisman --scan --reportdirectory=/Users/username/Desktop**`

您可以使用上面给出的其他选项进行扫描。

Talisman 目前不支持忽略文件进行扫描。

### 校验和计算器

Talisman 校验和计算器给出了 yaml 格式，您可以直接复制和粘贴。talismanrc 文件，以便忽略 talisman 检测器的特定文件格式。

要运行校验和，请“cd”到您的存储库的根目录，并运行以下命令

例如:`**talisman --checksum="*.pem *.txt"**`

*   该命令查找所有。pem 文件，计算所有这些文件的集合校验和，并输出一个. talismanrc 的 yaml 格式。txt 文件。
*   多个文件名/模式可以用空格分隔。

示例输出:

**。给定文件名/模式的 talismanrc 格式
fileignoreconfig:
文件名:'*。' pem '校验和:f 731 b 26 be 086 FD 2647 c 40801630 e 2219 ef 207 CB 1 AAC 02 f 9 BF 0559 a 75 c 0855 a 4 ignore _ detectors:[]文件名:'*。txt'
校验和:d 9 e 9 e 94868d 7 de 5 B2 a 0706 b 8d 38d 0 f 79730839 E0 EB 4 de 4 e 9 a2 a5a 014 c 7 c 43 f 35
忽略 _ 检测器:[]**

注意:校验和计算器在计算文件的集体校验和时会考虑转移文件。

# 护身符 HTML 报告

*由提供动力*

Talisman CLI 工具`**talisman**`还具有提供详细且可共享的 HTML 报告的能力。一旦你安装了 Talisman，请按照 talisman-html-report 中提到的步骤，在`**.talisman**`文件夹中安装报告包。要生成 html 报告，请运行:

*   `**talisman --scanWithHtml**`

这将扫描存储库，并在扫描的存储库下创建一个文件夹`**talisman_html_report**`。我们需要在这个存储库中启动一个 HTTP 服务器来访问报告。下面是启动 HTTP 服务器的推荐方法:

*   `**python -m SimpleHTTPServer <port> (eg: 8000)**`

现在，您可以通过导航到以下位置来访问该报告:

`**http://localhost:8000**`

# 卸载

卸载过程取决于你如何安装 Talisman。您可以选择作为一个全局钩子模板安装，或者安装在一个单独的存储库中。

请根据您在安装时选择的选项执行以下步骤。

## 从全局钩子模板卸载

在您的终端上运行以下命令，从您的机器上全局卸载 talisman。

对于提交前挂钩:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/uninstall . bash>/tmp/uninstall _ talisman . bash&&/bin/bash/tmp/uninstall _ talisman . bash**

对于预推挂钩:

**curl–silent https://raw . githubusercontent . com/thoughtworks/talisman/master/global _ install _ scripts/uninstall . bash>/tmp/uninstall _ talisman . bash&&/bin/bash/tmp/uninstall _ talisman . bash 预推送**

这将

*   问你所有仓库的基本目录，找到里面所有的 git 仓库，并移除护身符挂钩
*   从…上取下护身符钩。git 模板
*   从中央安装位置($HOME/)移除 talisman。护身符/垃圾箱)。

*你必须从你的环境变量中手动删除 TALISMAN _ HOME】*

## 从单个存储库卸载

当您安装 Talisman 时，它必须在安装期间在您的存储库中创建一个预提交或预推送挂钩(根据选择)。

您可以通过从中删除 Talisman 预提交或预推送挂钩来手动删除挂钩。仓库中的 git/hooks 文件夹。

[**Download**](https://github.com/thoughtworks/talisman)