# slither–固体静态分析仪

> 原文：<https://kalilinuxtutorials.com/slither-static-analyzer/>

**Slither** 是用 Python 3 编写的 Solidity 静态分析框架。它运行一套漏洞检测器，打印关于合同细节的可视信息，并提供一个 API 来轻松编写定制分析。Slither 使开发人员能够发现漏洞，增强他们的代码理解，并快速原型定制分析。

## **滑行特征**

*   以低误报率检测易受攻击的可靠性代码
*   标识源代码中错误条件出现的位置
*   轻松集成到持续集成和块菌构建中
*   内置“打印机”可快速报告重要的合同信息
*   用 Python 编写定制分析的检测器 API
*   能够分析坚实度> = 0.4 的合同
*   中间表示支持简单、高精度的分析

**也可阅读 [ct-exposer:一款通过搜索证书透明日志发现子域的 OSINT 工具](https://kalilinuxtutorials.com/ct-exposer-certificate-transparency-logs/)**

## **用途**

在 Truffle 应用程序上运行 Slither:

```
truffle compile
slither .
```

对单个文件运行 Slither:

```
$ slither tests/uninitialized.sol # argument can be file, folder or glob, be sure to quote the argument when using a glob
[..]
INFO:Detectors:Uninitialized state variables in tests/uninitialized.sol, Contract: Uninitialized, Vars: destination, Used in ['transfer']
[..]
```

如果 Slither 在一个目录上运行，它将在该目录中的每个`.sol`文件上运行。

### **配置**

*   `**--solc SOLC**`:路径到 **`solc`** (默认为‘solc’)
*   `**--solc-args SOLC_ARGS**`:添加自定义 solc 参数。`**SOLC_ARGS**`可以包含多个参数
*   `**--disable-solc-warnings**`:不要打印 solc 警告
*   `**--solc-ast**` **:使用** solc **AST 文件作为输入(** 【T1”)
*   `**--json FILE**`:将结果导出为 JSON

## **探测器**

默认情况下，所有检测器都在运行。

| 数字 | 探测器 | 它所探测到的 | 影响 | 信心 |
| --- | --- | --- | --- | --- |
| one | **`suicidal`** | 自杀功能 | 高的 | 高的 |
| Two | **`uninitialized-state`** | 未初始化的状态变量 | 高的 | 高的 |
| three | `**uninitialized-storage**` | 未初始化的存储变量 | 高的 | 高的 |
| four | `**arbitrary-send**` | 将以太传送到任意目的地的功能 | 高的 | 中等 |
| five | `reentrancy` | 重入漏洞 | 高的 | 中等 |
| six | `**locked-ether**` | 锁定以太的合同 | 中等 | 高的 |
| seven | `**tx-origin**` | `tx.origin`的危险用法 | 中等 | 中等 |
| eight | `**assembly**` | 程序集用法 | 报告的 | 高的 |
| nine | **`constable-states`** | 可以声明为常量的状态变量 | 报告的 | 高的 |
| Ten | **`external-function`** | 可以声明为外部的公共函数 | 报告的 | 高的 |
| Eleven | **`low-level-calls`** | 低级呼叫 | 报告的 | 高的 |
| Twelve | **`naming-convention`** | 符合可靠性命名惯例 | 报告的 | 高的 |
| Thirteen | **`pragma`** | 如果使用不同的 pragma 指令 | 报告的 | 高的 |
| Fourteen | `**solc-version**` | 旧版本的坚固性(< 0.4.23) | 报告的 | 高的 |
| Fifteen | **`unused-state`** | 未使用的状态变量 | 报告的 | 高的 |

### **打印机**

要运行打印机，使用`**--printers**`和逗号分隔的打印机列表。

| 数量 | 打印机 | 描述 |
| --- | --- | --- |
| one | `**call-graph**` | 将合约的调用图导出到点文件 |
| Two | `**contract-summary**` | 打印合同摘要 |
| three | `**function-summary**` | 打印功能摘要 |
| four | `**inheritance**` | 打印合同之间的继承关系 |
| five | `**inheritance-graph**` | 将每个契约的继承图导出到一个点文件 |
| six | `**slithir**` | 打印函数的滑动表示 |
| seven | **`vars-and-auth`** | 打印所写的状态变量和功能授权 |

## **安装**

Slither 需要 Python 3.6+和 solc，Solidity 编译器。

### **使用画中画**

```
$ pip install slither-analyzer
```

### **使用 Git**

```
$ git clone https://github.com/trailofbits/slither.git && cd slither
$ python setup.py install 
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/trailofbits/slither)