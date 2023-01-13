# 微软博斯克编程语言

> 原文：<https://kalilinuxtutorials.com/microsoft-bosque-programming-language/>

Bosque 编程语言是微软研究院的一个项目，该项目正在研究编写简单、明显、易于人类和机器推理的代码的语言设计。

该语言的关键设计特性提供了在开发和编码过程中避免意外复杂性的方法。

结果是提高了开发人员的工作效率，提高了软件质量，并带来了一系列新的编译器和开发人员工具体验。

下面是给出示例风格的小代码示例([代码片段](https://github.com/Microsoft/BosqueLanguage#Code-Snippets))。在[语言概述章节 0](https://github.com/Microsoft/BosqueLanguage/blob/master/docs/language/overview.md#0-Highlight-Features) 中提供了博斯克语的显著和/或独特特征的概要。

要了解这种语言如何在大的中工作和流动*,请查看一个[简单井字游戏](https://github.com/Microsoft/BosqueLanguage/blob/master/ref_impl/src/test/apps/tictactoe/main.bsq)程序的代码，该程序支持用用户提供的移动来更新棋盘，使计算机自动移动，并管理各种游戏状态。*

**注意:**这个存储库和代码代表了一个处于早期状态的项目。这样做是为了促进学术合作和社区参与。然而，这意味着该语言需要修订，存在缺陷和缺失的功能，并且性能有限。因此，我们**不**建议*在任何*制作工作中使用 Bosque 语言，而是鼓励在此时只对小型/实验性的副业项目进行实验。

**[也读作–EFI guard–启动时禁用 PatchGuard 和 DSE](https://kalilinuxtutorials.com/efiguard-disable-patchguard-and-dse-at-boot-time/)**

**代码片段**

添加 2 个数字:

**函数 add2(x: Int，y: Int): Int {
返回 x+y；
}
add2(2，3) //5**

使用 rest 参数和 lambda 进行所有奇数检查:

**function allOdd(…args: List[Int]): Bool {
return args- > all(fn(x) = > x % 2 == 1);
}
allOdd(1, 3, 4) //false**

批量更新记录上的属性

**函数更新(point: {x: Int，y: Int，z: Int}，value: Int): {x: Int，y: Int，z: Int} {
返回点< ~(y=value，x =-point . x)；
}
更新(@{x=1，y=2，z=3}，5) //@{x=-1，y=5，z = 3 }**

无法访问可选参数:

**函数 tryGetProperty(r？:{f: Int，k: Int}): Int？{
返回 r？。f；
}**

符号(带可选参数):

**函数符号(x？:Int): Int {
var！y；
if(x = = none | | x = = 0){
y = 0；
}
else {
y = (x > 0)？1 : -1;
}
返回 y；
}**

**使用博斯克语**

Bosque 项目目前的重点是核心语言设计。因此，对编译/开发的支持有限，对打包、部署、生命周期管理等的支持*没有*。

**要求**

**视窗**

为了构建 Windows 语言，需要以下内容:

*   用于 Windows (x64)的 LTS 版 [node.js](https://nodejs.org/en/download/)
*   Typescript(安装方式:`npm i typescript -g`)

**建造&测试**

`ref_impl`目录包含引用实现解析器、类型检查器、解释器和命令行运行程序。在此目录中，使用以下内容构建并测试 Bosque 参考实现:

**npm 安装&NPM 运行-脚本构建&NPM 测试**

**命令行执行**

`ref_impl`目录包含一个简单的命令行运行程序，用于独立的 Bosque ( `.bsq`)文件。这些文件必须有一个名为`main()`的`entrypoint`函数(参见[的一些例子](https://github.com/Microsoft/BosqueLanguage/blob/master/ref_impl/src/test/apps))。文件中的代码可以通过以下方式进行解析、类型检查和执行:

**节点 bin/test/app _ runner . js file . bsq**

**Visual Studio 代码集成**

这个库为 Bosque 语言提供了基本的 [Visual Studio 代码](https://code.visualstudio.com/) IDE 支持(目前仅限于语法和括号突出显示)。安装需要手动将完整的`bosque-language-tools/`文件夹复制到您的用户`.vscode/extensions/`目录中，并重新启动 VSCode。

[**Download**](https://github.com/Microsoft/BosqueLanguage)