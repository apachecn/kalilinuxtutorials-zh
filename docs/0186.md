# boot stomp——一个引导加载程序漏洞查找器

> 原文：<https://kalilinuxtutorials.com/bootstomp-vulnerability-bug-finder/>

BootStomp 是一个引导加载程序漏洞的工具。对于两类不同的错误，它看起来是不同的:内存损坏和状态存储漏洞。BootStomp 与为 ARM 架构(32 位和 64 位)编译的引导加载程序一起工作，结果可能会因 angr 和 Z3 的版本而略有不同。

## **要求**

*   安格尔

```
$ pip install angr
```

*   IDA PRO
*   IDA 反编译程序

## **手动运行 BootStomp】**

### **自动检测污染源和污染源**

1.  在 IDA 中加载 boot-loader 二进制文件(我们使用 6.95 版)。根据提取它的电话的 CPU 结构，需要 32 位或 64 位 IDA。
2.  从菜单栏中，运行 File => Script file => `**find_taint.py**`
3.  输出将出现在与引导加载程序相同目录下的文件`**taint_source_sink.txt**`中。

**亦读[Trape——学会追踪世界&避免被追踪](https://kalilinuxtutorials.com/trape-track-avoid-traced/)**

### **配置文件**

为引导加载程序二进制文件创建一个 JSON 配置文件(参见`config/`中的示例)，其中:

1.  **引导加载程序**:引导加载程序文件路径
2.  **info _ path**:boot-loader source/sink 信息文件路径(即 taint_source_sink.txt)
3.  **arch** :架构的位数(可选 32 和 64)
4.  **enable_thumb** :在分析期间考虑 thumb 模式(当需要时)
5.  **start_with_thumb** :启用 thumb 模式开始分析
6.  **exit_on_dec_error** :如果某些指令无法解码，则停止分析
7.  **unlock_addr** :解锁函数地址。只有在查找不安全状态存储漏洞时，此字段才是必需的。

### **寻找内存崩溃漏洞**

**运行**

```
python bootloadertaint.py config-file-path
```

结果将存储在`**/tmp/BootloaderTaint_[boot-loader].out**`中，其中`[boot-loader]`是被分析的引导加载程序的名称。请注意，包含循环的路径可能会出现多次。

### **发现不安全状态存储漏洞**

**运行**

```
python unlock_checker.py config-file-path
```

结果将存储在`**/tmp/UnlockChecker_[boot-loader].out**`中，其中`[boot-loader]`是被分析的引导加载程序的名称。请注意，包含循环的路径可能会出现多次。

### **检查结果**

要检查 BootStomp 结果，请使用脚本`result_pretty_print.py`，如下所示:

```
python result_pretty_print.py results_file
```

## **使用 docker 运行 BootStomp】**

使用 BootStomp 最简单的方法是在 docker 容器中运行它。文件夹`docker`包含一个合适的`**Dockerfile**`。这些是使用它的命令。

```
cd docker
# build the docker image
docker build -t bootstomp .
# run the docker image (if you need, use proper options to have persistent changes or shared files)
docker run -it bootstomp

# now you are inside a docker container
cd BootStomp
# run BootStomp's taint analysis on one of the examples
# this will take about 30 minutes
python taint_analysis/bootloadertaint.py config/config.huawei
# the last line of the output will be something like:
# INFO    | 2017-10-14 01:54:10,617 | _CoreTaint | Results in /tmp/BootloaderTaint_fastboot.img_.out

# you can then "pretty print" the results using:
python taint_analysis/result_pretty_print.py /tmp/BootloaderTaint_fastboot.img_.out
```

**输出应该如下所示:**

```
...
17)
===================== Start Info path =====================
Dereference address at: 0x5319cL
Reason: at location 0x5319cL a tainted variable is dereferenced and used as address.
...
Tainted Path 
----------------
0x52f3cL -> 0x52f78L -> 0x52f8cL -> 0x52fb8L -> 0x52fc8L -> 0x52fecL -> 0x53000L -> 0x53014L -> 0x5301cL -> 0x53030L -> 0x53044L -> 0x53050L -> 0x5305cL -> 0x53068L
===================== End Info path =====================
# Total sinks related alerts: 5
# Total loop related alerts: 8
# Total dereference related alerts: 4
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ucsb-seclab/BootStomp)