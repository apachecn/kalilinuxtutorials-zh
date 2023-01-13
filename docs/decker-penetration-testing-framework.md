# Decker:声明式渗透测试编排框架

> 原文：<https://kalilinuxtutorials.com/decker-penetration-testing-framework/>

Decker 是一个渗透测试编排框架。它利用 HashiCorp 配置语言 2(与 Terraform 相同的配置语言)允许将声明性渗透测试作为代码，因此您的测试可以被版本化、共享、重用，并与您的团队或社区协作。

**decker 配置文件示例:**

//变量从环境
//ex:DECKER _ TARGET _ HOST
//它们将作为 var 在整个配置文件中可用。*
//ex:$ { var . target _ host }
variable " target _ host " {
type = " string "
}
//资源引用插件
//资源需要唯一的名称，因此插件可以多次使用
//它们用以下格式声明:' resource " plugin _ name " " unique_name " { } '
//其他人可以使用 unique _ name 格式获得它们的输出。*
//ex:nmap . 443
resource " nmap " " nmap " {
host = " $ { var . target _ host } "
plugin _ enabled = " true "
}
resource " sslscan " " sslscan " {
host = " $ { var . target _ host } "
plugin _ enabled = " $ { nmap . 443 = = " open " } "
}

**为列表中的每个项目运行插件:**

变量" target _ host " {
type = " string "
}
资源" nslookup " " nslookup " {
DNS _ server = " 8 . 8 . 4 . 4 "
host = " $ { var . target _ host } "
}
资源" metasploit " " metasploit " {
for _ each = " $ { nslookup . IP _ address } "
exploit = " auxiliary/scanner/portscan/TCP "
options = {【t10t

**for _ each 与嵌套值组合的复杂配置:**

变量" target _ host " {
type = " string "
}
资源" nslookup " " nslookup " {
DNS _ server = " 8 . 8 . 4 . 4 "
host = " $ { var . target _ host } "
}
资源" nmap " " nmap " {
for _ each = " $ { nslookup . ip _ address } "
host = " $ { each . key } "
}
//对于每个 IP，检查
//如果是，运行 metasploit 的 smtp_enum 扫描器
resource " metasploit " " metasploit " {
for _ each = " $ { nslookup . IP _ address } "
exploit = " auxiliary/scanner/SMTP/SMTP _ enum "
options = {
RHOSTS = " $ { each . key } "
}
plugin _ enabled = " $ { nmap[" $ { each . key } "]. 25 = "。

**也可以理解为-[用户世界:在 Android](https://kalilinuxtutorials.com/userland-linux-android/)T3 上运行 Linux 发行版或应用程序**

**输出格式**

有多种输出格式可供选择，并且可以同时选择多种格式。

将`**DECKER_OUTPUTS_JSON**` **或** `**DECKER_OUTPUTS_XML**`设置为`**"true"**`将分别输出`**json**`和`**xml**`格式的文件。

1.  除了纯文本之外还输出`**.json**`个文件:`**export DECKER_OUTPUTS_JSON="true"**`
2.  除了纯文本之外还输出`**.xml**`个文件:`**export DECKER_OUTPUTS_XML="true"**`

**使用 docker** 运行示例配置

**安装了两个卷:**

*   目录名为 decker——报告 decker 将为每个执行的插件输出一个文件的位置。该文件的名称将为{唯一资源名称}.report.txt。
*   包含 decker 配置文件的示例目录。挂载这个卷允许您使用您喜欢的编辑器在本地编写配置，并且仍然在容器中运行它们。

**传入一个环境变量:**

*   **德克尔 _ 目标 _ 主机**

这在配置文件中被引用为{var.target_host}。Decker 将遍历所有名为 DECKER_*的环境变量，去掉前缀，并将其余部分设置为小写。

docker run-it–RM \
-v " $(pwd)/DECKER-reports/":/tmp/reports/\
-v " $(pwd)/examples/":/DECKER-config/\
-e DECKER _ TARGET _ HOST = example . com \
stevenaldinger/DECKER:kali DECKER。/decker-config/example.hcl

当德克尔完成运行配置，看看。/decker-输出的报告。

**在没有 docker 的情况下运行示例配置**

您可能希望使用 decker_REPORTS_DIR 环境变量设置 DECKER 写入报告的目录。

像这样的东西是合适的。只要确保您设置的是一个现有的目录。

导出 DECKER _ REPORTS _ DIR = " $ HOME/DECKER-REPORTS "

如果您正在运行一个示例配置文件，您还需要设置一个目标主机。

导出 DECKER_TARGET_HOST= " "

然后运行一个配置文件。切换到此 repo 的根目录并运行:

。/德克尔。/examples/example.hcl

**开发**

为了流畅的体验，建议使用 docker 进行开发。这确保了所有依赖项都已安装并准备就绪。

有关 go 代码的概述，请参考下面的目录结构。

**快速启动**

*   (在主机上):make docker_build
*   (在主机上):make docker_run(将启动 docker 容器并打开一个交互式 bash 会话)
*   (集装箱内):dep 确保-v
*   (在容器内部):生成全部构建
*   (集装箱内):运行

**初始化 git 挂钩**

运行 make init 以添加一个预提交脚本，该脚本将在每次提交时运行林挺和测试。

**插件开发**

Decker 本身只是一个框架，它读取配置文件，确定配置文件中的依赖关系，并按照一定的顺序运行插件，以确保依赖其他插件的插件(一个插件的输出是另一个插件的输入)在它们所依赖的插件之后运行。

decker 真正的强大来自于插件。开发一个插件可以是简单的，也可以是复杂的，只要最终结果是一个包含编译后的插件代码的. so 文件和一个声明插件期望用户配置的输入的. hcl 文件在同一个目录中。

开始 decker 插件开发的推荐方法是克隆 decker-plugin 存储库，并遵循其文档中的步骤。运行“Hello World”decker 插件应该只需要几分钟时间。

**安装插件**

默认情况下，插件应该位于相对于 decker 二进制文件所在位置的目录中，即**/internal/app/DECKER/plugins//**。因此，可以通过设置 DECKER_PLUGIN_DIRS 环境变量来添加其他路径。如果设置了 DECKER_PLUGIN_DIRS，将仍然使用默认插件路径。

例:**导出德克尔 _ 插件 _ DIRS = "/路径/至/我的/插件:/附加/路径/至/插件"**

旁边应该有一个 HCL 文件。所以文件在**/internal/app/decker/plugins//。定义其输入和输出的 hcl** 。目前，仅支持字符串、列表和映射输入。每个输入都应该有一个如下所示的输入块:

input " my _ input " {
type = " string "
default = "某默认值"
}

目录结构

。
build
【ci/
【package/
【cmd】
【decker】
【main . go】
【readme . MD】
例
HCl
githook
预提交
go pkg . toml
内部
app【应用】
【依赖】
【gocty/
【HCl/
【路径/
【插件/
】

*   [cmd/decker/main.go](https://github.com/stevenaldinger/decker/blob/master/cmd/decker/main.go) 是司机。它的工作是解析给定的[配置文件](https://github.com/stevenaldinger/decker/blob/master/examples)，根据文件的`resource`块加载适当的插件，并使用指定的输入运行插件。
*   [示例](https://github.com/stevenaldinger/decker/blob/master/examples)有几个配置示例，可以让你从`decker`开始。如果你使用 kali [docker 镜像](https://hub.docker.com/r/stevenaldinger/decker/) ( `stevenaldinger/decker:kali`)的话，所有的依赖项都应该安装在所有的配置文件中，一切都应该可以顺利运行。
*   [internal/pkg](https://github.com/stevenaldinger/decker/blob/master/internal/pkg) 是大部分实际代码所在的地方。包含了 [main.go](https://github.com/stevenaldinger/decker/blob/master/cmd/decker/main.go) 导入的所有包。
    *   [dependencies](https://github.com/stevenaldinger/decker/blob/master/internal/pkg/dependencies) 负责构建插件依赖图，并返回一个拓扑排序数组，确保插件按工作顺序运行。
    *   [gocty](https://github.com/stevenaldinger/decker/blob/master/internal/pkg/gocty) 为编码和解码用于处理动态输入类型的 [go-cty](https://github.com/zclconf/go-cty) 值提供帮助。
    *   hcl 负责解析 HCL 文件，包括创建评估上下文，当程序块依赖于其他插件程序块时，让程序块正确解码。
    *   [路径](https://github.com/stevenaldinger/decker/blob/master/internal/pkg/paths)负责返回`decker`二进制文件、配置文件、插件配置文件和生成报告的文件路径。
    *   [插件](https://github.com/stevenaldinger/decker/blob/master/internal/pkg/plugins)负责确定插件是否启用并运行。
    *   [reports](https://github.com/stevenaldinger/decker/blob/master/internal/pkg/reports) 负责向文件系统写报告。
*   [internal/app/decker/plugins](https://github.com/stevenaldinger/decker/blob/master/internal/app/decker/plugins)是模块化的代码片段，编写为 [Golang plugins](https://golang.org/pkg/plugin/) ，实现了一个简单的接口，允许在运行时加载和调用插件配置文件(也在 HCL 中)中指定的输入和输出。一个例子可以在[内部/app/decker/plugins/nslookup/nslookup . HCl](https://github.com/stevenaldinger/decker/blob/master/internal/app/decker/plugins/nslookup/nslookup.hcl)找到。
*   decker 配置文件提供了一种声明式的方式来编写渗透测试。清单是用 [HashiCorp 配置语言 2](https://godoc.org/github.com/hashicorp/hcl2/hcl) 编写的，描述了测试中要使用的插件集以及它们的输入。

[**Download**](https://github.com/stevenaldinger/decker)