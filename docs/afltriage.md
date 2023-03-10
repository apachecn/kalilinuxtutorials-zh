# AFLTriage:使用调试器对崩溃的输入文件进行分类的工具

> 原文：<https://kalilinuxtutorials.com/afltriage/>

[![](img/7918dbb11cd82e4d12a07d0ddf8f02ef.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjAE8enug_AK9lRs3o82wjzR9ORhXauHfjz5zsuJlwcUi0rBX_8JRYjU256qdE1CeCdPjhJZi_CwkLhTk3gyB8ik2fHzEQ8NJmWcEDBt11wquLX9GdS8BzGyRXwkrjNZGF1My3pI7NFj0LyXdxJn1krRnrTnNa13nOWdjvno6JCmssnDSa49MZrpZRv=s728)

是一个使用调试器对崩溃的输入文件进行分类的工具。它被设计成可移植的，除了 libc 和外部调试器之外，不需要任何运行时依赖。它支持对任何程序产生的崩溃进行分类，不仅仅是 AFL，而是特别识别 AFL 目录，因此得名。

一些显著的特征包括:

*   多种报告格式:文本、JSON 和原始调试器 JSON
*   并行崩溃分类
*   崩溃重复数据删除
*   杀毒报告解析
*   支持带或不带符号/调试信息的二进制目标
*   源代码和变量将在报告中注明上下文

目前 AFLTriage 只支持 GDB，并且只在 Linux C/C++目标上测试过。请注意，AFLTriage 不会根据潜在的可利用性对崩溃进行分类。准确的可利用性分类是非常针对目标和场景的，最好留给专门的工具和专家分析师。

**用法**

AFLTriage 的用法非常简单。您需要您的输入进行筛选，需要报告的输出目录，需要筛选二进制文件及其参数。

示例:

$ AFL triage-I fuzzing _ directory-**o 报告。/target _ binary–option-one @ @
AFL triage v 1 . 0 . 0
[+]GDB 正在工作(GNU gdb(Ubuntu 8 . 1 . 1-0 Ubuntu 1)8 . 1 . 1–Python 3 . 6 . 9(默认，2021 年 1 月 26 日 15:33:00))
[+]图片 triage cmdline:“。/target _ binary–option-one @ @ "
[+]报告将输出到目录" Reports "
[+]Triaging AFL directory fuzzing _ directory/(41 个文件)
[+] Triaging 41 个测试用例
[+]使用 24 个线程进行 Triaging
[+]Triaging[41/41 00:00:02][# # # # # # # # # # # # # # # # # # # # # #]崩溃:ASAN 在一次读取导致 SIGABRT 后检测到 buggy_function 中的堆缓冲区溢出**

与 AFL 类似，`**@@**`被替换为要分类的文件的路径。a 伤检分类会处理剩下的。

**建筑** **和运行**

你将需要一个工作的 Rust 构建环境。一旦你有货物和铁锈安装，建设和运行是简单的:

**CD AFL triage-RS/
cargo run-help
<编译>
在 0.33 秒内完成 dev [unoptimized + debuginfo]目标
运行`target/debug/afltriage --help`
AFLTriage 用法>**

**扩展使用**

**afltriage 1.0.0
快速分类并总结崩溃的测试用例
用法:
afltriage -i … -o …
选项:
-i …
测试用例的路径列表，测试用例的目录，AFL 目录，和/或要
分类的 AFL 目录的目录。请注意，该参数在一行中接受多个输入(例如-i input1 input2…)，因此它不能是传递给 AFLTriage 的最后一个参数
——这是为命令保留的。
-o
分诊报告文件的输出目录。使用“-”将整个报告打印到控制台。
-t，–time out
每个测试用例进行分类的超时时间，以毫秒为单位。[默认值:60000]
-j，–jobs
在分类期间使用多少线程。
–报告格式…
分诊报告输出格式。允许多个值:例如，文本、json。[default:text][可能的
值:text，json，raw JSON]
–bucket-strategy
要使用的崩溃重复数据删除策略。[默认值:afltriage][可能值:无，AFL triage，
first_frame，first_frame_raw，first_5_frames，function_names，first _ function _ name]
–child-output
在 triage 报告中包含子输出。
–child-output-lines
在报告中包含多少行从目标输出的程序。使用 0 表示无限制线路(不建议使用
)。[default:25]
–stdin
通过 stdin 而不是文件向目标提供测试用例输入。
–仅分析
执行环境检查，描述要分类的输入，并分析目标二进制文件。
–跳过轮廓
在输入处理前跳过目标轮廓。
–debug
启用分流操作的低级调试输出。
-h，–help
打印帮助信息
-V，–version
打印版本信息
ARGS:
…
要执行的二进制可执行文件和参数。使用“@@”作为输入文件或
–stdin 路径的占位符。(可选)使用—分隔命令的开始。
……**