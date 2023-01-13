# kaiju:Ghidra 软件逆向工程套件的二进制分析框架扩展

> 原文：<https://kalilinuxtutorials.com/kaiju/>

[![Kaiju : A Binary Analysis Framework Extension For The Ghidra Software Reverse Engineering Suite](img/6ee9b476f08a611f686962bd150205a8.png "Kaiju : A Binary Analysis Framework Extension For The Ghidra Software Reverse Engineering Suite")](https://1.bp.blogspot.com/-kSJwEoPKXmc/YMTBHbOM6VI/AAAAAAAAJfM/iwYaiAWboO4it36LVNtMfSDtusL52tZvQCLcBGAsYHQ/s728/Ghidra%25281%2529.png)

CERT **Kaiju** 是为 [Ghidra](https://ghidra-sre.org/) 开发的二进制分析工具的集合。这是对 [CERT Pharos 二进制分析框架](https://github.com/cmu-sei/pharos)的一些特性的 Ghidra/Java 实现，特别是函数哈希和恶意软件分析工具，但预计会随着时间的推移增加新的工具和功能。

由于这是一个新的尝试，这个实现还不具备与基于 ROSE 的原始 C++实现完全对等的特性；然而，迁移到 Java 和 Ghidra 实际上启用了一些原始框架中没有的新特性——特别是改进了对非 x86 架构的处理。由于正在对框架和工具进行一些重要的重新架构，并且迁移到 Java 和 Ghidra 实现了与 C++实现不同的功能，所以决定使用新的品牌，这样在讨论不同的工具和功能时，实现之间的混淆会更少。

我们打算在不久的将来同时维护最初的 Pharos 框架和 Kaiju，因为两者都能提供独特的特性和功能。

警告:作为一个原型，在评估这个插件创建的函数散列时，可能会出现许多问题。例如，与 Pharos 实现不同，Kaiju 的函数散列模块将为非常小的函数创建散列(例如，像 RET 这样的单个指令会导致更多意外冲突的函数)。因此，这个插件和 Pharos fn2hash 之间的分析结果可能会有所不同。

**快速安装**

[预建的 Kaiju 包](https://github.com/certcc/kaiju/releases)可用。只需下载与您的 Ghidra 版本相对应的 ZIP 文件，并按照下面的说明进行安装。建议通过 Ghidra 的图形界面安装，但也可以手动解压到适当的目录进行安装。

CERT Kaiju 需要以下运行时依赖项:

*   [Ghidra](https://ghidra-sre.org/) 9.1+(推荐 9.2+)
*   Java 11+(我们推荐 [OpenJDK 11](https://openjdk.java.net/install/) )

**注意**:也可以自己构建扩展包并安装。请参阅下面“自己构建 Kaiju”部分的说明。

**图形化安装**

启动 Ghidra，从打开的窗口中，从菜单中选择: **`File > Install Extension`** 。单击扩展窗口顶部的加号，导航并选择。在文件浏览器中压缩文件，然后点击确定。该扩展将被安装，并且在窗口中该扩展的名称旁边会有一个复选框，让您知道它已经安装并准备就绪。

界面会要求你重启 Ghidra 来开始使用扩展。只需重新启动，然后 Kaiju 的额外功能将可用于互动或脚本。

某些功能可能需要启用 Kaiju 插件。为此，打开代码浏览器，然后导航至菜单 **`File > Configure`** 。在弹出的窗口中，点击“CERT Kaiju”类别图标下方的`**Configure**`链接。一个弹出窗口将显示所有可用的公开发布的 Kaiju 插件。检查你想要激活的插件，然后点击 OK。你现在可以使用交互式插件功能了。

如果一个插件在启用后没有立即可见，您可以在代码浏览器的`**Window**`菜单下找到该插件。

如果你想测试的话，未来工具的实验“alpha”版本可以从“实验”类别中获得。然而，这些插件肯定是实验性的，不受支持，不建议生产使用。尽管如此，我们还是欢迎早期反馈！

**手动安装**

像 Kaiju 这样的 Ghidra 扩展也可以通过将扩展内容解压到 Ghidra 安装的适当目录中来手动安装。更多信息，请参见[GHI DRA 安装指南](https://ghidra-sre.org/InstallationGuide.html#Extensions)。

**用途**

Kaiju 的工具既可以以交互式图形方式使用，也可以通过更适合批处理作业的“无头”模式使用。根据工具的性质，有些工具可能只能用于图形或无头使用。

**交互式图形界面**

Kaiju 利用 Java Swing 和 Ghidra 的插件架构在 Ghidra 中创建了一个交互式图形界面(GUI)。

Kaiju 的大多数工具实际上是分析插件，当选择“自动分析”选项时，或者在导入新的可执行文件以进行反汇编时，或者通过直接从代码浏览器窗口选择`**Analysis > Auto Analyze...**`来自动运行。您将看到自动分析工具中默认选择的几个证书分析插件，但是您可以根据需要启用/禁用任何插件。

然而，在各种 GUI 工具工作之前，必须运行分析工具。在某些情况下，运行两次自动分析甚至会有所帮助，以确保生成所有元数据来创建正确的分区和反汇编信息，这反过来会影响散列结果。

分析仪在 Ghidra 的分析阶段自动运行，包括:

*   与标准的 Ghidra 分区相比，改进了反汇编的功能分区。
*   **Fn2Hash** =计算程序中所有函数的函数哈希，并用于生成程序的 YARA 签名。

GUI 工具包括:

*   函数散列查看器(Function Hash Viewer)=一个插件，显示一个程序中函数和几种类型散列的交互列表。分析师可以使用它将程序中的一个或多个函数导出到 YARA 签名中。
    *   如果该工具不可见，从菜单中选择`**Window > CERT Function Hash Viewer**`开始使用该工具。将出现一个新窗口，显示哈希表和其他数据。窗口顶部的按钮可以刷新表格或将数据导出到文件或 YARA 签名。这个窗口也可以停靠在主 Ghidra 代码浏览器中，以便与其他插件一起使用。使用该工具时，可以在 Ghidra 的`**Help > Contents**`菜单中找到更广泛的使用文档。
*   OOAnalyzer JSON Importer =一个插件，可以加载、解析 Pharos 生成的 OOAnalyzer 结果，并将其应用于 Ghidra 项目中面向对象的 C++可执行文件。启动时，插件将提示用户由 OOAnalyzer 生成的 JSON 输出文件，其中包含有关恢复的 C++类的信息。加载 JSON 文件后，OOAnalyzer 找到的恢复的 C++数据类型和符号会在 Ghidra 代码浏览器中更新。插件的设计和实现细节在我们 SEI 的博客文章[中有描述，使用 OOAnalyzer 对 Ghidra](https://insights.sei.cmu.edu/sei_blog/2019/07/using-ooanalyzer-to-reverse-engineer-object-oriented-code-with-ghidra.html) 的面向对象代码进行逆向工程。
    *   从菜单中选择 **`CERT > OOAnalyzer Importer`** 开始使用该工具。一个简单的弹出对话框将要求您找到想要导入的 JSON 文件。使用该工具时，可以在 Ghidra 的`**Help > Contents**`菜单中找到更广泛的使用文档。

**命令行“无头”模式**

Ghidra 还支持“无头”模式，允许工具在某些情况下运行，而无需使用交互式 GUI。因此，这些命令可用于大量文件的脚本和“批处理模式”作业。

无头工具很大程度上依赖于 Ghidra 的 GhidraScript 功能。

无头工具包括:

*   **fn2hash** =在给定程序上自动运行 fn2hash，并将所有散列导出到指定的 CSV 文件中
*   **fn2yara** =在给定程序上自动运行 Fn2Hash，并将所有散列数据作为 yara 签名导出到指定的文件中
*   **fnxrefs** =分析一个程序，并根据入口点地址导出一系列函数，这些函数在数据或程序的其他部分中有交叉引用

已经包含了一个名为`**kaijuRun**`的简单 shell 启动脚本来运行这些用于简单场景的无头命令，比如输出单个可执行文件中每个函数的函数散列。假设设置了`**GHIDRA_INSTALL_DIR**`变量，例如，可以在单个可执行文件上运行启动脚本，如下所示:

**$ GHI DRA _ INSTALL _ DIR/GHI DRA/Extensions/kaiju/kaijuRun fn2 hash example.exe**

该命令会将结果输出到一个自动命名为 **`example.exe.Hashes.csv`的文件中。**

运行以下命令可获得 **`kaijuRun`** 脚本的基本帮助:

**$ GHI DRA _ INSTALL _ DIR/GHI DRA/Extensions/kaiju/kaijuRun–help**

有关使用该模式和`**kaijuRun**`启动器脚本的更多信息，请参见存储库中的 **`docs/HeadlessKaiju.md`** 文件。

**更多文档和帮助**

更全面的文档和帮助有两种格式。

参见 **`docs/`** 目录，获取所有 Kaiju 工具和组件的 Markdown 格式文档和帮助。这些文档易于维护、编辑和阅读，甚至可以从命令行进行。

或者，您可以在 Ghidra 的内置帮助系统中找到相同的文档。要访问这些帮助文档，从 Ghidra 菜单，转到`**Help > Contents**`，然后从帮助窗口左侧的树形导航中选择`**CERT Kaiju**`。

请注意，Ghidra 帮助文档与`**docs/**`目录中的降价文件内容完全相同；多亏了一个树内 gradle 插件，gradle 将在构建过程中自动解析 Markdown 并导出到 Ghidra HTML 中。这使得维护更加简单(只在一个地方而不是两个地方更新文档),并使两者保持同步。

所有新文档都应添加到`**docs/**`目录中。

**使用 Gradle 自己构建 Kaiju】**

除了预编译的包，你也可以自己编译和编译 Kaiju。

**构建依赖关系**

CERT Kaiju 需要以下构建依赖项:

*   [Ghidra](https://ghidra-sre.org/) 9.1+(推荐 9.2+)
*   [gradle](https://gradle.org/install/) 6.4+(推荐最新的 gradle 6.x，不支持 7.x)
*   GSON 2 . 8 . 6
*   Java 11+(我们推荐 [OpenJDK 11](https://openjdk.java.net/install/) )

**关于 gradle 的注意事项**:请确保 GRADLE 的构建版本与 Ghidra 在您的系统上使用的 JDK 版本相同，否则您可能会遇到安装问题。

**关于 GSON** 的注意事项:大多数情况下，Gradle 会自动为你获取这个。如果发现需要手动获取，可以下载 [gson-2.8.6.jar](https://repo1.maven.org/maven2/com/google/code/gson/gson/2.8.6/gson-2.8.6.jar) ，放在`**kaiju/lib**`目录下。

**构建指令**

一旦安装了依赖项，就可以使用`**gradle**`构建工具将 Kaiju 构建为 Ghidra 扩展。建议首先按照 Ghidra 安装说明设置一个 Ghidra 环境变量。

简而言之:首先将`**GHIDRA_INSTALL_DIR**`设置为环境变量，然后不带任何选项运行`**gradle**`:

**导出 GHIDRA _ INSTALL _ DIR =<GHIDRA 安装目录>的绝对路径
gradle**

**注意**:你的 Ghidra 安装目录是包含`ghidraRun`脚本的目录(将 Ghidra 发行版解压到你选择的位置后的顶级目录。)

如果由于某种原因，您的环境变量没有设置或无法设置，您也可以在命令中指定它，例如使用:

**gradle-PGHIDRA _ INSTALL _ DIR =<Ghidra 安装目录的绝对路径** >

在这两种情况下，新建的 Kaiju 扩展名将以. zip 文件的形式出现在 **`dist/`** 目录中。文件名将包括“Kaiju”，构建它所依据的 Ghidra 版本，以及它的构建日期。如果一切顺利，您应该会看到如下消息，告诉您构建的插件的名称。

**在/kaiju/dist 中创建了 ghidra _ X . y . z _ PUBLIC _ YYYYMMDD _ kaiju . zip**

其中 **`X.Y.Z`** 是你正在使用的 Ghidra 版本，`**YYYYMMDD**`是你构建这个 Kaiju 扩展的日期。

##### **可选:使用自动测试运行测试**

虽然不是必需的，但您可能希望使用 Kaiju 测试套件来验证正确的编译，并确保在测试新代码时或在生产环境中安装 Kaiju 之前没有回归。

为了运行 Kaiju 测试套件，您需要首先获得 AUTOCATS(自动化代码分析测试套件)。AUTOCATS 包含许多可执行文件和相关数据，用于在 Kaiju 中执行测试和检查回归。这些测试用例与 Pharos 二进制分析框架共享，因此 AUTOCATS 位于一个单独的 git 存储库中。

使用以下内容克隆 AUTOCATS 存储库:

**git 克隆 https://github.com/cmu-sei/autocats**

我们建议将 AUTOCATS 库克隆到与 Kaiju 相同的父目录中，但是您可以在任何您希望的地方克隆它。

然后，测试可以在以下条件下运行:

**gradle -PKAIJU_AUTOCATS_DIR=path/to/autocats/dir test**

其中当然提供了到克隆的 AUTOCATS 存储库目录的正确路径。如果按照建议克隆到与 Kaiju 相同的父目录，该命令将类似于:

**gradle -PKAIJU_AUTOCATS_DIR=../autocats test**

如果不提供此路径，测试将无法运行；如果你真的忘记了，gradle 会中止并给出一个关于提供这个路径的错误信息。

Kaiju 只在运行测试时依赖于 [JUnit 5](https://junit.org/junit5/) 。Gradle 应该会自动检索并使用 JUnit，但如果需要，您也可以下载 JUnit 并手动放入 Kaiju 的 **`lib/`** 目录中。

每当你获取最新的 Kaiju 源代码时，你都需要运行 update 命令，以确保它们保持同步。

**首次基于梯度的“无头”安装**

如果您编译并构建了自己的 Kaiju 扩展，您也可以通过使用 gradle 直接在命令行上安装该扩展。确保首先将`**GHIDRA_INSTALL_DIR**`设置为环境变量(如果您也构建了 Kaiju，那么您应该已经定义了这个变量)，然后运行 **`gradle`** ，如下所示:

**导出 GHIDRA _ INSTALL _ DIR =<GHIDRA 安装目录>的绝对路径
gradle 安装**

或者如果您不确定是否设置了环境变量，

**gradle-PGHIDRA _ INSTALL _ DIR =<Ghidra 安装目录的绝对路径> install**

应该自动复制扩展文件。在 Ghidra 重新启动后，Kaiju 将可供使用。

**注意**:在使用 gradle 安装之前，请确保 Ghidra 没有运行。我们知道，如果在 Ghidra 运行时安装缓存，会出现缓存无法正确更新的情况，从而导致一些奇怪的错误。如果您遇到这种情况，只需退出 Ghidra 并尝试重新安装。

**考虑先移除您的旧安装**

在更新到新版本之前，先完全删除旧版本的 Kaiju 可能会有所帮助。我们已经看到一些情况，旧版本的 Kaiju 文件卡在缓存中，由于冲突导致有趣的错误。通过首先删除旧的安装，您将确保干净的重新安装和易于使用。

如果您启用此功能，gradle build 进程现在可以自动删除以前安装的 Kaiju。要启用自动删除，请将“KAIJU_AUTO_REMOVE”属性添加到您的安装命令中，例如(假设环境变量可能如前一节所述进行了设置):

**gradle -PKAIJU_AUTO_REMOVE 安装**

如果您希望手动删除旧安装，请执行如下命令:

RM-RF $ GHI DRA _ INSTALL _ DIR/Extensions/GHI DRA/*开居*。zip $ GHI DRA _ INSTALL _ DIR/GHI DRA/Extensions/kaiju

[**Download**](https://github.com/cmu-sei/kaiju)