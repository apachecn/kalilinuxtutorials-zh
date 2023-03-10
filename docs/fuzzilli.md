# Fuzzilli:一个 JavaScript 引擎 Fuzzer

> 原文：<https://kalilinuxtutorials.com/fuzzilli/>

[![Fuzzilli : A JavaScript Engine Fuzzer](img/a5027f987a10abc3d34863644a62cdcc.png "Fuzzilli : A JavaScript Engine Fuzzer")](https://1.bp.blogspot.com/-6dS48dq-YhY/X760DwQY8NI/AAAAAAAAIFI/Xri3BLYqBpYPAzCJc69OgpBXNkmYub9JgCLcBGAsYHQ/s728/Fuzzilli%25281%2529.png)

Fuzzilli 是一个(覆盖率)导向的模糊器，用于基于定制中间语言(“fuzzill”)的动态语言解释器，该语言可以变异并翻译成 JavaScript。

**用途**

使用这种模糊器的基本步骤是:

*   下载一个受支持的 JavaScript 引擎的源代码。有关支持的 JavaScript 引擎列表，请参见 [Targets/](https://github.com/googleprojectzero/fuzzilli/blob/master/Targets) 目录。
*   从目标目录中应用相应的补丁程序。另请参见该目录中的 README.md。
*   按照自述文件中的描述，使用覆盖率工具编译引擎(要求 clang >= 4.0)。
*   编译模糊器: **`swift build [-c release]`。**
*   运行 **`swift run [-c release] FuzzilliCli --profile=<profile> [other cli options] /path/to/jsshell`。另请参见`swift run FuzzilliCli --help`。**

在 Docker 内部和 Google Compute Engine 上构建和运行 Fuzzilli 和受支持的 JavaScript 引擎[也受支持](https://github.com/googleprojectzero/fuzzilli/blob/master/Cloud)。

**黑客攻击**

查看 [main.swift](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/FuzzilliCli/main.swift) 以查看 Fuzzilli 库的使用示例，并尝试各种配置选项。接下来，看看高级模糊逻辑的 [Fuzzer.swift](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Fuzzer.swift) 。从那里开始，深入到任何看起来有趣的部分。

补丁、添加、其他贡献等。对这个项目非常欢迎！但是，请务必快速查看[对贡献者](https://github.com/googleprojectzero/fuzzilli/blob/master/CONTRIBUTING.md)的注释。Fuzzilli 大致遵循[谷歌的 swift](https://google.github.io/swift/) 代码风格指南。

如果你能给[saelo@google.com](mailto:saelo@google.com)发一封短信(可能包括一个 CVE 号码),或者打开这个项目帮助下发现的任何漏洞的 pull 请求，以便它能被包括在 [bug 展示](https://github.com/googleprojectzero/fuzzilli#bug-showcase)部分，我将不胜感激。除此之外，你当然可以要求任何 bug 奖励，CVE 积分等等。针对漏洞🙂

**概念**

当对核心解释器错误进行模糊处理时，例如在 JIT 编译器中，生成的程序的语义正确性成为一个关注点。这与大多数其他场景相反，例如运行时 API 的模糊化，在这种情况下，可以通过将生成的代码包装在 try-catch 结构中来轻松解决语义正确性问题。有不同的可能性来实现语义正确样本的可接受比率，其中之一是突变方法，其中语料库中的所有样本也是语义有效的。在这种情况下，每个突变只有很小的机会将有效样本变成无效样本。

为了实现基于变异的 JavaScript fuzzer，必须定义 JavaScript 代码的变异。不是改变 AST 或程序的其他语法元素，而是定义定制中间语言(IL ),在该语言上可以更直接地执行对程序的控制和数据流的改变。这个 IL 随后被翻译成 JavaScript 来执行。中间语言大致如下:

v 0v4
V6<—二进制运算 v3，'+'，v4
重新分配 v3，V6
end for
v7<—LoadString ' Result:'
V8<—二进制运算 V7，'+'，v3
v9<—load global ' console '
v10<—调用方法 v9，' log '，[v8]

这可以例如被简单地翻译成下面的 JavaScript 代码:

const v0 = 0
const v1 = 10；
const v2 = 1；
设 v3 = 0；
for(设 v4 = v0v4<v1；v4 = v4+v2){
const V6 = v3+v4；
v3 = V6；
}
const V7 = " Result:"；
const V8 = V7+v3；
const v9 =控制台；
const v10 = v 9 . log(V8)；

或者通过内联中间表达式转换为以下 JavaScript 代码:

设 v3 = 0；
for(设 v4 = 0；v4<10；v4++){
v3 = v3+v4；
}
console.log("结果:"+v3)；

FuzzIL 有许多属性:

*   一个模糊的程序就是一系列指令。
*   FuzzIL 指令是一个操作以及输入和输出变量，可能还有一个或多个参数(在上面的符号中用单引号括起来)。
*   指令的输入总是变量，没有即时值。
*   一条指令的每个输出都是一个新变量，现有变量只能通过专用操作(如`Reassign`指令)重新分配。
*   每个变量在使用前都被定义了。

然后可以在这些程序上进行许多突变:

*   [InputMutator](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Mutators/InputMutator.swift) :用不同的变量替换指令的输入变量，使程序的数据流发生变异。
*   [CodeGenMutator](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Mutators/CodeGenMutator.swift) :生成代码并将其插入变异程序的某个地方。通过运行[代码生成器](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/CodeGenerators.swift)或者从语料库中的另一个程序复制一些指令(拼接)来生成代码。
*   [CombineMutator](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Mutators/CombineMutator.swift) :将语料库中的程序插入变异程序中的随机位置。
*   [OperationMutator](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Mutators/OperationMutator.swift) :对运算的参数进行变异，例如用不同的常数替换一个整数常数。
*   还有更多…

**实施**

fuzzer 在 [Swift](https://swift.org/) 中实现，有一些部分(例如覆盖测量、套接字交互等。)用 c 实现。

**架构**

fuzzer 实例(在 [Fuzzer.swift](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Fuzzer.swift) 中实现)由以下核心组件组成:

*   [突变模糊器](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/MutationFuzzer.swift):通过应用[突变](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Mutators)从现有程序产生新程序。然后执行生成的样本并对其进行评估。
*   [ScriptRunner](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Execution) :执行目标语言的程序。
*   [语料库](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/Corpus.swift):存储感兴趣的样本，并提供给核心模糊器。
*   [环境](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/JavaScriptEnvironment.swift):了解运行时环境，例如可用的内置、属性名和方法。
*   [最小化器](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Minimization/Minimizer.swift):最小化崩溃和有趣的程序。
*   [评估器](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Evaluation):根据某种度量标准，例如代码覆盖率，评估一个样本是否有趣。
*   [Lifter](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Lifting) :将一个 FuzzIL 程序翻译成目标语言(JavaScript)。

此外，还有许多模块可供选择:

*   [统计](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Modules/Statistics.swift):收集各种统计信息。
*   [network worker/network master](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Modules/NetworkSync.swift):通过网络同步多个实例。
*   [thread worker/thread master](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Modules/ThreadSync.swift):同步同一个进程内的多个实例。
*   [存储](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Modules/Storage.swift):将崩溃的程序存储到磁盘。

fuzzer 是事件驱动的，不同类之间的大多数交互都是通过事件发生的。例如，作为崩溃或发现感兴趣的程序、执行新程序、生成日志消息等的结果，事件被分派。请参见 [Events.swift](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/Events.swift) 了解完整的活动列表。事件机制有效地解耦了 fuzzer 的各种组件，并使实现附加模块变得容易。

使用 [ProgramBuilder](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Core/ProgramBuilder.swift) 实例可以构建一个 FuzzIL 程序。ProgramBuilder 提供了创建和追加新指令、追加来自另一个程序的指令、检索现有变量、查询当前位置的执行上下文(例如，它是否在循环内)等方法。

**执行**

Fuzzilli 使用了一种自定义的执行模式，称为 [REPRL(读取-评估-打印-重置-循环)](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Execution/REPRL.swift)。为此，修改目标引擎以接受通过管道和/或共享内存输入的脚本，执行它，然后重置其内部状态并等待下一个脚本。这消除了进程创建的开销，并在初始化时消除了引擎的大部分开销。

**可扩展性**

每个目标进程有一个 [Fuzzer](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Fuzzer.swift) 实例。这使得程序能够同步执行，从而简化了各种算法的实现，例如连续突变和最小化。此外，它避免了对内部状态(例如语料库)实现线程安全访问的需要。每个 fuzzer 实例都有自己的 [DispatchQueue](https://developer.apple.com/documentation/dispatch/dispatchqueue) ，在概念上对应于单个线程。根据经验，与 Fuzzer 实例的每次交互都必须发生在该实例的调度队列上。这保证了线程安全，因为队列是串行的。更多细节见[文档](https://github.com/googleprojectzero/fuzzilli/blob/master/Docs/ProcessingModel.md)。

为了扩大规模，fuzzer 实例可以成为工人，在这种情况下，它们向主实例报告新发现的有趣样本和崩溃。反过来，主实例也将它们的语料库与工作者同步。主设备和工作设备之间的通信可以以不同的方式进行，每种方式都作为一个模块实现:

*   [线程间通信](https://github.com/googleprojectzero/fuzzilli/blob/master/Sources/Fuzzilli/Modules/ThreadSync.swift):通过将任务排入另一个 fuzzer 的 DispatchQueue 来同步同一个进程中的实例。
*   进程间通信(TODO):通过 IPC 通道同步实例。
*   机器间通信:通过简单的基于 TCP 的协议同步实例。

这种设计允许 fuzzer 扩展到一台机器上的许多内核以及许多不同的机器。因为如果太多的工作器向一个主实例发送程序，该主实例会很快过载，所以也可以配置多个主实例层，例如一个主实例，16 个连接到主实例的中间主实例，以及 256 个连接到中间主实例的工作器。

**资源**

关于此 fuzzer 的更多资源:

*   关于 Fuzzilli 的一个[演示](https://saelo.github.io/presentations/offensivecon_19_fuzzilli.pdf)在进攻 Con 2019 上给出。
*   完成初始实现的[硕士论文](https://saelo.github.io/papers/thesis.pdf)。
*   Sensepost 发布了一篇关于使用 Fuzzilli 在 v8 中找到一个 bug 的博文
*   Doyensec 的一篇关于用 Fuzzilli 模糊化 JerryScript 引擎的博文

**Bug 展示区**

以下是在 Fuzzilli 的帮助下发现的一些 bug 的列表。列表中仅包含具有安全影响的错误。特别感谢所有举报过它发现的 bug 的 Fuzzilli 用户！

**WebKit/JavaScriptCore**

*   [问题 185328](https://bugs.webkit.org/show_bug.cgi?id=185328) : DFG 编译器在数字整数运算中使用了不正确的输出寄存器
*   [CVE-2018-4299](https://www.zerodayinitiative.com/advisories/ZDI-18-1081/):performProxyCall 向脚本泄漏内部对象
*   [CVE-2018-4359](https://bugs.webkit.org/show_bug.cgi?id=187451) :编译器产生不正确的机器代码
*   [CVE-2019-8518](https://bugs.chromium.org/p/project-zero/issues/detail?id=1775) :由于 LICM 在边界检查前移动数组访问，FTL JIT 中的 OOB 访问
*   [CVE-2019-8558](https://bugs.chromium.org/p/project-zero/issues/detail?id=1783) :由于悬空观察点导致代码块 UaF
*   [CVE-2019-8611](https://bugs.chromium.org/p/project-zero/issues/detail?id=1788):AIR optimization 错误地删除了注册分配
*   [CVE-2019-8623](https://bugs.chromium.org/p/project-zero/issues/detail?id=1789):DFG JIT 中的循环不变代码运动(LICM)使堆栈变量未初始化
*   [CVE-2019-8622](https://bugs.chromium.org/p/project-zero/issues/detail?id=1802) : DFG 的 doesGC()关于 HasIndexedProperty 操作在 StringObjects 上的行为是不正确的
*   [CVE-2019-8671](https://bugs.chromium.org/p/project-zero/issues/detail?id=1822) : DFG:循环不变代码运动(LICM)使得对象属性访问不受保护
*   [CVE-2019-8672](https://bugs.chromium.org/p/project-zero/issues/detail?id=1825) : JSValue 在 ValueProfiles 中使用后免费
*   [CVE-2019-8678](https://bugs.webkit.org/show_bug.cgi?id=198259) : JSC 在修改一些原型时无法运行 haveABadTime()，导致类型混淆
*   [CVE-2019-8685](https://bugs.webkit.org/show_bug.cgi?id=197691):JSPropertyNameEnumerator 使用了错误的结构 id
*   [CVE-2019-8765](https://bugs.chromium.org/p/project-zero/issues/detail?id=1915):DFG 编译期间 GetterSetter 类型混淆
*   [CVE-2019-8820](https://bugs.chromium.org/p/project-zero/issues/detail?id=1924) :重建参数对象时救助时类型混乱
*   CVE-2020-3901:FTL JIT 代码中的 GetterSetter 类型混乱(由于不总是安全的 LICM)

**壁虎/蜘蛛猴**

*   [CVE-2018-12386](https://ssd-disclosure.com/archives/3765/ssd-advisory-firefox-javascript-type-confusion-rce):ion monkey 寄存器分配 bug 导致类型混淆
*   [CVE-2019-9791](https://bugs.chromium.org/p/project-zero/issues/detail?id=1791) :对于通过 OSR 输入的构造函数，IonMonkey 的类型推断不正确
*   [CVE-2019-9792](https://bugs.chromium.org/p/project-zero/issues/detail?id=1794) : IonMonkey 泄露 JS_OPTIMIZED_OUT 魔值给脚本
*   [CVE-2019-9816](https://bugs.chromium.org/p/project-zero/issues/detail?id=1808):object group dispatch 操作中出现意外的对象组
*   [CVE-2019-9813](https://bugs.chromium.org/p/project-zero/issues/detail?id=1810) : IonMonkey 编译的代码无法更新推断的属性类型，导致类型混淆
*   [CVE-2019-11707](https://bugs.chromium.org/p/project-zero/issues/detail?id=1820):ion monkey 错误预测 Array.prototype.pop 的返回类型，导致类型混淆
*   [CVE-2020-15656](https://bugzilla.mozilla.org/show_bug.cgi?id=1647293):ion monkey 中特殊参数的类型混淆

**铬/v8**

*   [问题 939316](https://bugs.chromium.org/p/project-zero/issues/detail?id=1799) :优化 Reflect.construct 时，涡扇发动机可能会读取超出边界的地图指针
*   [问题 944062](https://bugs.chromium.org/p/project-zero/issues/detail?id=1809):JSCallReducer::reduce arrayindexofincludes 无法插入映射检查
*   [CVE-2019-5831](https://bugs.chromium.org/p/chromium/issues/detail?id=950328):V8 中地图处理错误
*   问题 944865:V8 中的值表示无效
*   [CVE-2019-5841](https://bugs.chromium.org/p/chromium/issues/detail?id=969588) :内联启发式的 Bug
*   [CVE-2019-5847](https://bugs.chromium.org/p/chromium/issues/detail?id=972921) : V8 密封/冻结元件导致崩溃
*   [CVE-2019-5853](https://bugs.chromium.org/p/chromium/issues/detail?id=976627) :正则表达式长度检查内存损坏
*   [问题 992914](https://bugs.chromium.org/p/project-zero/issues/detail?id=1923) :地图迁移不考虑元素种类，导致类型混乱
*   [CVE-2020-6512](https://bugs.chromium.org/p/chromium/issues/detail?id=1084820):V8 中的类型混淆

**Duktape**

*   [问题 2323](https://github.com/svaarala/duktape/pull/2323):putprop 中的 valstack 指针不稳定
*   [问题 2320](https://github.com/svaarala/duktape/pull/2320) :字符串内置内存 cmp 指针溢出

**杰瑞脚本**

*   [CVE-2020-13991](https://github.com/jerryscript-project/jerryscript/issues/3858) :传播论证的错误发布
*   [问题 3784](https://github.com/jerryscript-project/jerryscript/issues/3784) :由于不正确的属性枚举导致内存损坏
*   CVE-2020-13623 :通过代理对象的属性键堆栈溢出
*   [CVE-2020-13649 (1)](https://github.com/jerryscript-project/jerryscript/issues/3786) :由于 OOM 情况下的错误处理导致的内存损坏
*   [CVE-2020-13649 (2)](https://github.com/jerryscript-project/jerryscript/issues/3788) :由于 OOM 情况下的错误处理导致的内存损坏
*   [CVE-2020-13622](https://github.com/jerryscript-project/jerryscript/issues/3787) :由于代理对象的属性键处理不正确，导致内存损坏
*   [CVE-2020-14163](https://github.com/jerryscript-project/jerryscript/issues/3804) :添加键/值对时，垃圾收集触发的竞争条件导致内存损坏
*   [问题 3813](https://github.com/jerryscript-project/jerryscript/issues/3813):SerializeJSONProperty 函数中的错误处理不正确
*   [问题 3814](https://github.com/jerryscript-project/jerryscript/issues/3814):ECMA _ op _ function _ has _ instance 断言中出现意外的代理对象
*   [问题 3836](https://github.com/jerryscript-project/jerryscript/issues/3836) :由于不正确的 TypedArray 初始化导致内存损坏
*   [问题 3837](https://github.com/jerryscript-project/jerryscript/issues/3837):getOwnPropertyDescriptor 中不正确的内存处理导致内存损坏

**免责声明**

这不是官方支持的谷歌产品。