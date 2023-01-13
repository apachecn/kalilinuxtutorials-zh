# little 下士:一个 C#自动化 Maldoc 生成器

> 原文：<https://kalilinuxtutorials.com/littlecorporal/>

[![](img/8740b2026d403bcda895435e1ec18a24.png)](https://1.bp.blogspot.com/-ZGTZ62sqg3Y/YVSXPK7l2JI/AAAAAAAAK_I/5wGmDMFqhc8fcscQHlFEtQmr2B8jD3xrwCLcBGAsYHQ/s728/maldoc%2B%25281%2529.png)

**file 下士**接受一个用户提供的参数，用于将一个进程注入到一台*远程*机器上，您计划在该机器上执行恶意的 Word 文档，并且还接受一个以`**.bin**`格式存储的本地外壳代码文件的路径——比如运行 little 下士的机器上的一个 Beacon Stageless 外壳代码 blob。因此，如果您想要使用从这个项目生成的 maldoc，您将需要在您想要运行 maldoc 的机器上指定一个已经运行的进程(无论是本地机器还是不同的机器。`**explorer.exe**`总是有一个实例，所以如果你不在乎注入哪个进程，就使用这个。

little 下士将外壳代码和目标进程名嵌入到`**Loader.cs**`中，将`**Loader.cs**`动态编译成. NET `**.exe**`工件，然后利用线程劫持进行远程进程注入。的。NET `**.exe**`工件，也就是线程劫持加载器，通过 Donut 发送，生成位置无关的外壳代码，执行`**.exe**`。Donut 生成的外壳代码然后进行 base64 编码，生成一个 Word 文档，最终的 Donut blob 存储在 InlineShape 中。AlternativeText Word 属性，它能够保存整个有效负载。这是通过在 Word 文档中插入一个图像(当前是一个空白图像，使文档具有“空白”外观)属性来实现的，作为图像上的可选文本，它包含有效负载。file 下士然后利用 VBA“模板”，包含在这个项目中作为一个文本文件，并将这个宏注入到新生成的 Word 文档中。该宏被命名为`**autoopen**`，因此它在文档打开时打开，然后被配置为提取先前生成的图像的替换文本的值，该值包含最终的有效负载，base64 对其进行解码，最后在 VBA 使用 Windows API 调用来执行将*本地*注入到 Word 中。本质上，这个项目在 VBA 使用一个简单的“加载器”来执行到 Word 的本地注入，这比远程进程注入要少一点审查，然后使用来自简单本地注入注入的执行来执行 Donut 外壳代码，这是另一个*加载器，它执行线程劫持，用于将用户提供的外壳代码最终远程进程注入到用户指定的进程中。这一切都是以自动化的方式完成的，包括 Word 文档的生成。*

**要求和限制**

*   小下士组装了。NET 线程劫持神器使用。NET v2。请确认。NET v2 安装在您用来生成 Word 文档的机器上(确保`**C:\Windows\Microsoft.NET\Framework64\v2.0.50727\**`存在)和您计划运行文档的目标机器上。
*   您还必须在计划运行`**LittleCorporal.exe**`的机器上安装 Office。这是因为 little 下士需要通过 COM 与 Word 进行交互。还请注意，生成的 Word doc 从互联网上拉下一个空白图像——这意味着你需要在你计划引爆 Word doc 的远程机器上用*和*运行 LittleCorproal 的计算机上接入互联网。
*   不幸的是，little 下士只能在 64 位版本的 Word 中使用*。这是为什么呢？只有 64 位系统才能识别线程劫持加载程序功能中使用的结构——例如 64 位`**CONTEXT**`结构，它具有 64 位特定数据类型。这是因为线程劫持目前仅在 64 位系统上受支持，因为它需要自定义外壳代码，该代码特别遵守`**__fastcall**`调用约定。我不打算实现 32 位版本的线程劫持功能，但如果最终有一个 32 位支持的拉请求，因为许多 Microsoft Word 安装都是 32 位的，我不会完全排除这种可能性。从逻辑角度来看，这目前不应该是一个大的修复，当从`**__fastcall**`移动到`**__stdcall**`并计算新的偏移量时，这个问题成为维护堆栈跟踪的负担和麻烦。从技术角度来看，这并不复杂，但是有点费力。*
*   *线程劫持代码首先检查执行 Word 文档的机器是否加入了域。如果在未加入域的机器上运行，请在运行 **`LittleCorporal.exe`** 生成 Word 文档之前，将该行代码编辑为`**bool FUNC1 = true;**`*

 ***推荐**

如果您计划将此项目用于活动的 red team 操作，请考虑将外壳代码的“退出”功能设置为使用线程退出来执行“干净”退出，而不是完全终止外壳代码所在的进程。这可以通过`**EXITFUNC=thread**`用 msfvenom 配置，也可以通过 Aggressor 在钴击中配置。

**用法**

*   为了使用，您必须获取整个项目！little 下士使用额外资源的相对路径，如 Donut。
*   一旦获得整个项目，将你的工作目录更改为`**bin\Release**`目录(`**cd**` **`C:\Path\to\LittleCorporal\bin\Release` )** )。如果您选择重新编译此项目，建议您使用发布版本而不是调试版本。
*   在您执行`**LittleCorporal.exe**`的机器上指定 shellcode 文件的路径，并在您想要执行 Word 文档的机器上指定已经运行的进程。(`**LittleCorporal.exe C:\Path\To\Shellcode.bin explorer.exe**`)
*   little 下士然后将输出最终 Word 文档的路径
*   要“清理”工件目录，使用下面的命令:`**LittleCorporal.exe clean**`

[**Download**](https://github.com/connormcgarr/LittleCorporal)*