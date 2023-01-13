# Slither:固体静态分析仪

> 原文：<https://kalilinuxtutorials.com/slither-static-analyzer-solidity/>

[![Slither : Static Analyzer for Solidity](img/0ebfb274f472836ebdf66bc97aa74b18.png "Slither : Static Analyzer for Solidity")](https://1.bp.blogspot.com/-w5GMADRXlX8/XbMwKQf3_DI/AAAAAAAADHU/LHFA0pehinAN1090Qom38xiq2KbaemO5wCLcBGAsYHQ/s1600/logo.png)

**Slither** 是用 Python 3 编写的 Solidity 静态分析框架。它运行一套漏洞检测器，打印关于合同细节的可视信息，并提供一个 API 来轻松编写定制分析。

它使开发人员能够发现漏洞，增强他们对代码的理解，并快速构建定制分析的原型。

**特性**

*   以低误报率检测易受攻击的可靠性代码
*   标识源代码中错误条件出现的位置
*   轻松集成到持续集成和块菌构建中
*   内置“打印机”可快速报告重要的合同信息
*   用 Python 编写定制分析的检测器 API
*   能够分析坚实度> = 0.4 的合同
*   中间表示( [SlithIR](https://github.com/trailofbits/slither/wiki/SlithIR) )支持简单、高精度的分析
*   正确解析 99.9%的公共安全代码
*   每个合同的平均执行时间不到 1 秒

**用法**

在 Truffle/Embark/Dapp/Etherlime 应用程序上运行 Slither:

滑行。

对单个文件运行 Slither:

**$ slither tests/initialized . sol**

有关其他配置，请参见[用法](https://github.com/trailofbits/slither/wiki/Usage)文档。

使用[solc-如果您的合同需要旧版本的 solc，请选择](https://github.com/crytic/solc-select)。

**探测器**

默认情况下，所有检测器都在运行。

| 数字 | 探测器 | 它所探测到的 | 影响 | 信心 |
| --- | --- | --- | --- | --- |
| one | `rtlo` | [使用了从右到左覆盖控制字符](https://github.com/crytic/slither/wiki/Detector-Documentation#right-to-left-override-character) | 高的 | 高的 |
| Two | `shadowing-state` | [状态变量遮蔽](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing) | 高的 | 高的 |
| three | `suicidal` | [允许任何人破坏合同的功能](https://github.com/crytic/slither/wiki/Detector-Documentation#suicidal) | 高的 | 高的 |
| four | `uninitialized-state` | [未初始化的状态变量](https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-state-variables) | 高的 | 高的 |
| five | `uninitialized-storage` | [未初始化的存储变量](https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-storage-variables) | 高的 | 高的 |
| six | `arbitrary-send` | [向任意目的地发送乙醚的功能](https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations) | 高的 | 中等 |
| seven | `controlled-delegatecall` | [受控委托目的地](https://github.com/crytic/slither/wiki/Detector-Documentation#controlled-delegatecall) | 高的 | 中等 |
| eight | `reentrancy-eth` | [重入漏洞(窃取醚)](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities) | 高的 | 中等 |
| nine | `erc20-interface` | [错误的 ERC20 接口](https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-erc20-interface) | 中等 | 高的 |
| Ten | `erc721-interface` | [错误的 ERC721 接口](https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-erc721-interface) | 中等 | 高的 |
| Eleven | `incorrect-equality` | [危险严格等式](https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-strict-equalities) | 中等 | 高的 |
| Twelve | `locked-ether` | [锁定以太的契约](https://github.com/crytic/slither/wiki/Detector-Documentation#contracts-that-lock-ether) | 中等 | 高的 |
| Thirteen | `shadowing-abstract` | [来自抽象契约的状态变量](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing-from-abstract-contracts) | 中等 | 高的 |
| Fourteen | `constant-function` | [常量功能改变状态](https://github.com/crytic/slither/wiki/Detector-Documentation#constant-functions-changing-the-state) | 中等 | 中等 |
| Fifteen | `reentrancy-no-eth` | [可重入漏洞(不窃取醚)](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1) | 中等 | 中等 |
| Sixteen | `tx-origin` | [`tx.origin`](https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-usage-of-txorigin)的危险用法 | 中等 | 中等 |
| Seventeen | `unchecked-lowlevel` | [未检查的低级调用](https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-low-level-calls) | 中等 | 中等 |
| Eighteen | `unchecked-send` | [未勾选发送](https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-send) | 中等 | 中等 |
| Nineteen | `uninitialized-local` | [未初始化的局部变量](https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables) | 中等 | 中等 |
| Twenty | `unused-return` | [未使用的返回值](https://github.com/crytic/slither/wiki/Detector-Documentation#unused-return) | 中等 | 中等 |
| Twenty-one | `shadowing-builtin` | [内置符号阴影](https://github.com/crytic/slither/wiki/Detector-Documentation#builtin-symbol-shadowing) | 低的 | 高的 |
| Twenty-two | `shadowing-local` | [局部变量隐藏](https://github.com/crytic/slither/wiki/Detector-Documentation#local-variable-shadowing) | 低的 | 高的 |
| Twenty-three | `void-cst` | [未实现调用的构造函数](https://github.com/crytic/slither/wiki/Detector-Documentation#void-constructor) | 低的 | 高的 |
| Twenty-four | `calls-loop` | [循环中的多个呼叫](https://github.com/crytic/slither/wiki/Detector-Documentation/_edit#calls-inside-a-loop) | 低的 | 中等 |
| Twenty-five | `reentrancy-benign` | [良性重入漏洞](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2) | 低的 | 中等 |
| Twenty-six | `timestamp` | [`block.timestamp`](https://github.com/crytic/slither/wiki/Detector-Documentation#block-timestamp)的危险用法 | 低的 | 中等 |
| Twenty-seven | `assembly` | [组装用途](https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage) | 报告的 | 高的 |
| Twenty-eight | `deprecated-standards` | [废弃的坚固性标准](https://github.com/crytic/slither/wiki/Detector-Documentation#deprecated-standards) | 报告的 | 高的 |
| Twenty-nine | `erc20-indexed` | [未索引的 ERC20 事件参数](https://github.com/crytic/slither/wiki/Detector-Documentation#unindexed-erc20-event-parameters) | 报告的 | 高的 |
| Thirty | `low-level-calls` | [低电平呼叫](https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls) | 报告的 | 高的 |
| Thirty-one | `naming-convention` | [符合可靠性命名惯例](https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions) | 报告的 | 高的 |
| Thirty-two | `pragma` | [如果使用不同的编译指示指令](https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used) | 报告的 | 高的 |
| Thirty-three | `solc-version` | [不正确的实度版本(< 0.4.24 或复杂杂注)](https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity) | 报告的 | 高的 |
| Thirty-four | `unused-state` | [未使用的状态变量](https://github.com/crytic/slither/wiki/Detector-Documentation#unused-state-variables) | 报告的 | 高的 |
| Thirty-five | `too-many-digits` | [符合数字符号最佳实践](https://github.com/crytic/slither/wiki/Detector-Documentation#too-many-digits) | 报告的 | 中等 |
| Thirty-six | `constable-states` | [可以声明为常数的状态变量](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variables-that-could-be-declared-constant) | 最佳化 | 高的 |
| Thirty-seven | `external-function` | [可以声明为外部的公共函数](https://github.com/crytic/slither/wiki/Detector-Documentation#public-function-that-could-be-declared-as-external) | 最佳化 | 高的 |

[联系我们](https://www.trailofbits.com/contact/)获取更多检测机。

**打印机**

要运行打印机，使用`--print`和逗号分隔的打印机列表。

| 数字 | 打印机 | 描述 |
| --- | --- | --- |
| one | `call-graph` | [将合约的调用图导出到一个点文件](https://github.com/trailofbits/slither/wiki/Printer-documentation#call-graph) |
| Two | `cfg` | [导出各功能的 CFG](https://github.com/trailofbits/slither/wiki/Printer-documentation#cfg) |
| three | `constructor-calls` | [打印执行的构造函数](https://github.com/crytic/slither/wiki/Printer-documentation#constructor-calls) |
| four | `contract-summary` | [打印合同摘要](https://github.com/trailofbits/slither/wiki/Printer-documentation#contract-summary) |
| five | `data-dependency` | [打印变量的数据相关性](https://github.com/trailofbits/slither/wiki/Printer-documentation#data-dependencies) |
| six | `echidna` | [导出鼹鼠引导信息](https://github.com/trailofbits/slither/wiki/Printer-documentation#echidna) |
| seven | `function-id` | [打印函数](https://github.com/trailofbits/slither/wiki/Printer-documentation#function-id)的 keccack256 签名 |
| eight | `function-summary` | [打印功能摘要](https://github.com/trailofbits/slither/wiki/Printer-documentation#function-summary) |
| nine | `human-summary` | [打印人类可读的合同摘要](https://github.com/trailofbits/slither/wiki/Printer-documentation#human-summary) |
| Ten | `inheritance` | [打印合同间的继承关系](https://github.com/trailofbits/slither/wiki/Printer-documentation#inheritance) |
| Eleven | `inheritance-graph` | [将每个合同的继承图导出到一个点文件](https://github.com/trailofbits/slither/wiki/Printer-documentation#inheritance-graph) |
| Twelve | `modifiers` | [打印每个函数调用的修饰符](https://github.com/trailofbits/slither/wiki/Printer-documentation#modifiers) |
| Thirteen | `require` | [打印每个函数的 require 和 assert 调用](https://github.com/trailofbits/slither/wiki/Printer-documentation#require) |
| Fourteen | `slithir` | [打印函数的第三种表示](https://github.com/trailofbits/slither/wiki/Printer-documentation#slithir) |
| Fifteen | `slithir-ssa` | [打印函数的第三种表示](https://github.com/trailofbits/slither/wiki/Printer-documentation#slithir-ssa) |
| Sixteen | `variable-order` | [打印状态变量的存储顺序](https://github.com/trailofbits/slither/wiki/Printer-documentation#variable-order) |
| Seventeen | `vars-and-auth` | [打印写入的状态变量和功能授权](https://github.com/trailofbits/slither/wiki/Printer-documentation#variables-written-and-authorization) |

**如何安装**？

Slither 需要 Python 3.6+和 [solc](https://github.com/ethereum/solidity/) ，Solidity 编译器。

**使用画中画**

$ pip 安装滑动分析器

**使用 Git**

$ git 克隆 https://github.com/crytic/slither.git & & CD slither
$ python setup . py 安装

如果你喜欢通过 git 安装 Slither，我们推荐使用 Python 虚拟环境，详见[开发者安装说明](https://github.com/trailofbits/slither/wiki/Developer-installation)。

**使用 Docker**

使用 [`**eth-security-toolbox**`](https://github.com/trailofbits/eth-security-toolbox/) docker 图像。它在一个映像中包含了我们所有的安全工具和 Solidity 的每个主要版本。`**/home/share**`将被安装到`**/share**`的集装箱中。使用 [`**solc-select**`](https://github.com/trailofbits/eth-security-toolbox/#usage) 切换实度版本。

docker pull trail ofbits/eth-安全-工具箱

要共享容器中的目录:

docker-run-it-v/home/share:/share trailofbits/eth-security-toolbox

[**Download**](https://github.com/crytic/slither/)