# 自动模糊:自动模糊重复的任务

> 原文：<https://kalilinuxtutorials.com/autopwn-automate-fuzzing/>

[![AutoPwn : Automate Repetitive Tasks For Fuzzing](img/aeba314dc4b873f3b02e547b5451ac61.png "AutoPwn : Automate Repetitive Tasks For Fuzzing")](https://1.bp.blogspot.com/-VJEgsRCXB_0/XPd1esrXwAI/AAAAAAAAApU/7oceGnILRtUPDqG7MydY7sI33Sd8MNPRQCLcBGAs/s1600/fuzzing.png)

现在完全重写这个。对于初学者来说，重点将放在只从 stdin 获取输入的交互式 Linux 应用程序上。试图使用 Shellphish 的钻孔机和 Fuzzer 功能。目前状态下的自动驾驶将会以有限的形式做到这一点。只需运行`**autoPwn ./binary**`，然后选择启动选项。

**安装**

考虑到这里所有的依赖性问题，启动和运行自动生成的最简单方法是使用 Docker 构建。请注意，您可以删除–security-opt 和–cap-add 语句，但是一些模糊的方面可能不起作用。

**也可以理解为-[Kubolt:用于扫描公共 Kubernetes 集群的实用程序](https://kalilinuxtutorials.com/kubolt/)**

**$ sudo docker pull bann sec/autoPwn
$ sudo docker run-it-v $ PWD:/mount–security-opt = " apparmor = unconlined "-cap-add = SYS _ PTRACE bann sec/autoPwn**

在 Docker 构建中，一切都应该准备就绪。您可以简单地使用以下命令启动该工具:

**$自动生成。/文件**

**编译用于模糊化的源代码**

autoPwn 试图使模糊项目的编译源代码变得更容易。为了帮助解决这个问题，`**autoPwnCompile**`应运而生。只要把它指向你的源代码，给它一些选项，它就会输出一个可以模糊的可执行文件。

用法:autoPwncompile[-h][–FILE FILE][–ASAN |–MSAN][–乌巴桑]
[–FUZZER FUZZER]

将源代码编译成二进制文件，以便在 autopown 中使用。

可选参数:
-h，–help 显示此帮助信息并退出
–FILE 要编译的单个文件。
–ASAN 启用 ASAN(默认关闭)
–MSAN 启用 MSAN(默认关闭)
–UBSAN 启用 UBSAN(默认关闭)
–fuzzer FUZZER(可选)编译什么 FUZZER。选项有:
['AFL']。默认为 AFL。

下面是它的旧版本。

**概述**

自动生成是一个简单脚本的崇高名称。当使用 fuzzing 和 AFL-fuzzing 时，我注意到我会一遍又一遍地做同样的任务。考虑到这一点，我想创建一个脚本来完成以下任务:

1.  通过智能提示自动执行并简化启动模糊程序的任务
2.  通过配置文件自动化并简化重新启动 fuzzer 的任务
3.  完全自动化 afl 队列最小化流程
4.  完全自动化提取和最小化所有可能的可利用路径的过程
5.  完全自动化提取和最小化所有可能路径的过程。
6.  完全或部分自动生成初始路径值。

到目前为止，这个剧本能够排到第 5 位。第 6 部分是推测性的，目前正在尝试开发。它将利用 angr 符号执行引擎来创建可能的初始路径。在这一点上，脚本理论上可以完全自动化简单的模糊任务。

**例子**

我们来看看最近一个叫“WoO2”的 TUCTF 挑战赛。虽然它不一定能找到所需的漏洞，但它确实展示了如何使用 autoPwn 来简化路径发现。

下面是该程序的基本流程:

$ ./e 67 EB 287 f 23011 a 40 ef 5b D5 C2 ad 2 f 48 ca 97834 cf
欢迎光临！我想我们已经不在堪萨斯了。
我们即将开始一场冒险！
选择一些你想带去的动物。

菜单选项:
1:带狮子
2:带老虎
3:带熊
4:删除动物
5:退出

输入你的选择:
1
选择你想要的狮子类型:
1:刚果狮子
2:巴巴里狮子
1
输入狮子名称:
测试
菜单选项:
1:带一

让我们创建一个简单的输入测试用例:

**$ cat in/1
1
1
测试 5**

现在我们可以很容易地启动 fuzzer:

**$ autoPwn
设置模糊配置
目标二进制(完整或相对路径):e 67 EB 287 f 23011 a 40 e F5 BD 5 C2 ad 2f 48 ca 97834 cf
命令行参数:
内核数(默认:8):
测试用例目录(默认:' in/'):
测试用例目录(默认:' out/'):
最大内存(默认:200): 4096
启动模糊【T9 0 hrs) < < <
周期 1，生存期速度 1 execs/sec，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃
会话 000 (0 天，0 hrs) < < <
周期 1，生存期速度 1 execs/sec，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃
0 hrs) < < <
周期 1，生存期速度 1 执行/秒，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃
会话 004 (0 天，0 小时)< < <
周期 1，生存期速度 1 执行/秒，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃【T35 0 小时)< < <
周期 1，生存期速度 1 执行秒，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃
会话 003 (0 天，0 小时)< < <
周期 1，生存期速度 1 执行秒，路径 0/1 (0%)
待定 1/1，覆盖率 0.15%，尚未崩溃

汇总统计数据 0 小时
总执行数:000 万
累积速度:8 执行数/秒
挂起路径:8 个收藏夹，每个模糊器总共有 8 个

挂起:1 个收藏夹，总共(平均)发现 1 个
崩溃:0 个局部唯一的

自动生成> h
自动生成
s ==模糊器(s)状态
e ==收集(e)xploits
a ==收集**

这里发生的事情是，脚本创建了一些默认值(包括确定可用内核的数量)。我们更改了一个默认值，因为在 QEMU 中运行这个需要额外的内存。autoPwn 创建了一个配置文件，然后交给 AFL-utils([https://github.com/rc0r/afl-utils](https://github.com/rc0r/afl-utils))。在配置文件中，它还设置了 CPU 关联，因此模糊化将是默认的最佳选择。

在这一点上，你的电脑正在摆脱模糊。然而，模糊化的一个关键方面是最小化语料库。考虑到这一点，autoPwn 正在观察 afl-fuzz 实例，以监视一系列突变何时完成。当这种情况发生时，它将停止模糊化(非最优，但目前还好)，最小化语料库，然后重新开始模糊化。它不需要任何人工干预就能做到这一点，所以你可以发射并忘记。

在某种程度上，你可能想看看 afl 找到了什么路径。通过执行“a”命令，autoPwn 将复制所有已知的路径，最小化语料库，然后最小化案例本身，并在输出目录中提供它们。

[**Download**](https://github.com/bannsec/autoPwn)