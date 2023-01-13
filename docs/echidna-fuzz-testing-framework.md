# 鼹鼠:以太坊模糊测试框架

> 原文：<https://kalilinuxtutorials.com/echidna-fuzz-testing-framework/>

[![Echidna : Ethereum Fuzz Testing Framework](img/2ad86d5f0a05e77159337cd54b0963f7.png "Echidna : Ethereum Fuzz Testing Framework")](https://1.bp.blogspot.com/-ixGqaWSOP2o/XSd2y4AS2eI/AAAAAAAABUE/2b0EQqmfGJMJxqg9rDfngg0Bi7hrLf4CgCLcBGAs/s1600/Echidna%25281%2529.png)

鼹鼠是一种奇怪的生物，它吃虫子，对电流高度敏感(向雅各布·斯坦利道歉)

更严重的是，鼹鼠是一个 Haskell 库，设计用于 EVM 代码的模糊化/基于属性的测试。它支持相对复杂的基于语法的模糊化活动来伪造各种谓词。

**特色**

*   生成适合您实际代码的输入
*   可选的覆盖范围指南，用于发现更深层次的错误
*   用于快速分类的自动测试用例最小化
*   无缝集成到开发工作流程中
*   快的
*   用于高级用途的强大 API
*   漂亮的标志

**用法**

**执行测试运行器**

核心鼹鼠功能是一个名为`**echidna-test**` **的可执行文件。** `**echidna-test**`接受一个契约和一个不变量列表(应该始终保持为真的属性)作为输入。对于每个不变量，它生成对契约的随机调用序列，并检查不变量是否成立。如果它能找到伪造不变量的方法，它会打印出这样做的调用序列。如果它不能，你就可以保证合同是安全的。

**书写不变量**

不变量被表示为名字以`**echidna_**`开头的实性函数，没有参数，返回一个布尔值。例如，如果你有一些不应该低于`20`的`balance`变量，你可以在契约中写一个额外的函数，如下所示:

**也读作-[网络设置:操作安全实用程序&自动机](https://kalilinuxtutorials.com/netset-operational-security-utility-automator/)**

**函数 echidna _ check _ balance(){
return(balance>= 20)；
}**

要检查这些不变量，请运行:

**$ echidna-试验支原体. sol**

带有测试的示例契约可以在[examples/solidity/basic/flags . sol](https://github.com/crytic/echidna/blob/master/examples/solidity/basic/flags.sol)中找到。要运行它，您应该执行:

**$针鼹-测试示例/坚固性/基本/标志. sol**

鼹鼠应该找到一个伪造`**echidna_sometimesfalse**`的调用序列，并且应该找不到一个伪造的`**echidna_alwaystrue**`输入。

**配置选项**

鼹鼠的 CLI 可用于选择测试和加载配置文件的合同。

**$ echidna-TEST contract . sol TEST–config = " config . YAML "**

配置文件允许用户选择 EVM 和测试生成参数。带有默认选项的完整配置文件的示例可以在[examples/solidity/basic/default . YAML](https://github.com/crytic/echidna/blob/master/examples/solidity/basic/default.yaml)中找到。关于配置选项的更详细的文档可以在我们的 [wiki](https://github.com/trailofbits/echidna/wiki/Config) 中找到。

**高级用法**

鼹鼠出口一个 API 来构建强大的模糊系统，并有多种配置选项。不幸的是，代码库的这些部分变化很快，因此很少被记录。Bits 博客的[示例/api 目录](https://github.com/crytic/echidna/blob/master/examples/api)或[踪迹](https://blog.trailofbits.com/2018/05/03/state-machine-testing-with-echidna/)是很好的参考资料，或者使用下面的参考资料直接与我们联系。

**安装**

如果你想在 Linux 中快速测试鼹鼠，我们提供一个静态链接的二进制版本 v1.0.0.0，在这里下载。

否则，要安装鼹鼠的最新版本，我们建议使用 [docker](https://www.docker.com/) :

**$ docker build -t 针鼹。**

例如

**$ docker run-t-v ' pwd ':/src 针鼹针鼹-test/src/examples/solidity/basic/flags . sol**

如果你喜欢从源代码构建，使用[栈](https://docs.haskellstack.org/en/stable/README/)。`stack install`应该在`~/.local/bin`建立并编译`echidna-test`。您将需要链接 libreadline 和 libsecp256k1(构建时启用了恢复功能)，它们应该与您选择的软件包管理器一起安装。此外，您需要安装最新版本的 [libff](https://github.com/scipr-lab/libff) (您可以看看我们 CI 测试中使用的[这个脚本](https://github.com/crytic/echidna/blob/master/.travis/install-libff.sh))

如果您得到了与链接相关的错误构建，请尝试修改`**--extra-include-dirs**` **和** `**--extra-lib-dirs**` **。**

[**Download**](https://github.com/crytic/echidna)