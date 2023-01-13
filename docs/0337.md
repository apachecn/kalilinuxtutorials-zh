# miasm——Python 中的逆向工程框架

> 原文：<https://kalilinuxtutorials.com/miasm-reverse-engineering-framework/>

Miasm 是一个免费的开源(GPLv2)逆向工程框架。Miasm 旨在分析/修改/生成二进制程序。以下是一个不完整的功能列表:

*   使用 Elfesteem 打开/修改/生成 PE / ELF 32 / 64 LE / BE
*   组装/拆卸 X86 / ARM / MIPS / SH4 / MSP430
*   用中间语言表示汇编语义
*   使用 JIT(动态代码分析、解包等)进行模拟
*   用于自动去混淆的表达式简化

**也可理解为[Ache——用于特定领域搜索的网络爬虫](https://kalilinuxtutorials.com/ache-web-crawler-domain/)**

## 瘴气是如何工作的？

Miasm 嵌入了自己的反汇编器、中间语言和指令语义。它是用 Python 写的。

为了模拟代码，它使用 LLVM、GCC、Clang 或 Python 来 JIT 中间表示。它可以模拟外壳代码和全部或部分二进制文件。可以执行 Python 回调来与执行交互，例如模拟库函数效果。

## **软件要求**

瘴气用途:

*   python-pyparsing
*   python 开发
*   精灵从[精灵从](https://github.com/serpilliere/elfesteem.git)
*   可选 python-pycparser(版本> = 2.17)

要启用代码 JIT，以下模块之一是必需的:

*   （同 groundcontrolcenter）地面控制中心
*   铿锵
*   带 Numba llvmlite 的 LLVM，见下文

可选的“瘴气”也可以使用:

*   Z3，[定理证明者](https://github.com/Z3Prover/z3)

## **配置**

*   安装精灵精灵

```
git clone https://github.com/serpilliere/elfesteem.git elfesteem
cd elfesteem
python setup.py build
sudo python setup.py install
```

要使用抖动，建议使用 GCC 或 LLVM

*   GCC(任何版本)
*   铿锵(任何版本)
*   LLVM
    *   Debian(测试/不稳定):未测试
    *   debian stable/Ubuntu/Kali/whatever:`pip install llvmlite`或者从 [llvmlite](https://github.com/numba/llvmlite) 安装
    *   Windows:未测试
*   构建并安装 Miasm:

```
$ cd miasm_directory
$ python setup.py build
$ sudo python setup.py install
```

如果在其中一个抖动模块编译期间出错，Miasm 将跳过错误并禁用相应的模块(参见编译输出)。

## **Windows & IDA**

大多数 Miasm 的 IDA 插件使用 Miasm 功能的子集。让它们工作的一个快速方法是添加:

*   **`elfesteem`** 目录和`**pyparsing.py**`到`**C:\...\IDA\python\**`或`**pip install pyparsing elfesteem**`
*   `**miasm2/miasm2**`目录到`**C:\...\IDA\python\**`

除抖动相关功能外，所有功能都将可用。有关更完整的安装，请参考以上段落。

## **测试**

瘴气带有一组回归测试。要运行所有这些程序:

```
cd miasm_directory/test
python test_all.py
```

可以指定一些选项:

*   单声道线程:`**-m**`
*   代码覆盖率检测:`**-c**`
*   仅快速测试:`**-t long**`(不包括长时间测试)

## **基本示例**

#### **组装/拆卸**

导入 Miasm x86 体系结构:

```
>>> from miasm2.arch.x86.arch import mn_x86
>>> from miasm2.core.locationdb import LocationDB
```

获取位置数据库:

```
>>> loc_db = LocationDB()
```

组装生产线:

```
>>> l = mn_x86.fromstring('XOR ECX, ECX', loc_db, 32)
>>> print l
XOR        ECX, ECX
>>> mn_x86.asm(l)
['1\xc9', '3\xc9', 'g1\xc9', 'g3\xc9']
```

修改操作数:

```
>>> l.args[0] = mn_x86.regs.EAX
>>> print l
XOR        EAX, ECX
>>> a = mn_x86.asm(l)
>>> print a
['1\xc8', '3\xc1', 'g1\xc8', 'g3\xc1']
```

拆解结果:

```
>>> print mn_x86.dis(a[0], 32)
XOR        EAX, ECX
```

使用`Machine`抽象:

```
>>> from miasm2.analysis.machine import Machine
>>> mn = Machine('x86_32').mn
>>> print mn.dis('\x33\x30', 32)
XOR        ESI, DWORD PTR [EAX]
```

对于 Mips:

```
>>> mn = Machine('mips32b').mn
>>> print  mn.dis('97A30020'.decode('hex'), "b")
LHU        V1, 0x20(SP)
```

## **中间表示法**

创建说明:

```
>>> machine = Machine('arml')
>>> instr = machine.mn.dis('002088e0'.decode('hex'), 'l')
>>> print instr
ADD        R2, R8, R0
```

创建中间表示对象:

```
>>> ira = machine.ira(loc_db)
```

创建一个空的 ircfg

```
>>> ircfg = ira.new_ircfg()
```

向池中添加指令:

```
>>> ira.add_instr_to_ircfg(instr, ircfg)
```

打印当前池:

```
>>> for lbl, irblock in ircfg.blocks.items():
...     print irblock.to_string(loc_db)
loc_0:
R2 = R8 + R0

IRDst = loc_4 
```

与 IR 一起工作，例如通过获得副作用:

```
>>> for lbl, irblock in ircfg.blocks.iteritems():
...     for assignblk in irblock:
...         rw = assignblk.get_rw()
...         for dst, reads in rw.iteritems():
...             print 'read:   ', [str(x) for x in reads]
...             print 'written:', dst
...             print
...
read:    ['R8', 'R0']
written: R2

read:    []
written: IRDst 
```

## **仿真**

给出外壳代码:

```
00000000 8d4904      lea    ecx, [ecx+0x4]
00000003 8d5b01      lea    ebx, [ebx+0x1]
00000006 80f901      cmp    cl, 0x1
00000009 7405        jz     0x10
0000000b 8d5bff      lea    ebx, [ebx-1]
0000000e eb03        jmp    0x13
00000010 8d5b01      lea    ebx, [ebx+0x1]
00000013 89d8        mov    eax, ebx
00000015 c3          ret
>>> s = '\x8dI\x04\x8d[\x01\x80\xf9\x01t\x05\x8d[\xff\xeb\x03\x8d[\x01\x89\xd8\xc3'
```

通过`Container`抽象导入外壳代码:

```
>>> from miasm2.analysis.binary import Container
>>> c = Container.from_string(s)
>>> c
<miasm2.analysis.binary.ContainerUnknown object at 0x7f34cefe6090>
```

在地址`0`拆卸外壳代码:

```
>>> from miasm2.analysis.machine import Machine
>>> machine = Machine('x86_32')
>>> mdis = machine.dis_engine(c.bin_stream)
>>> asmcfg = mdis.dis_multiblock(0)
>>> for block in asmcfg.blocks:
...  print block.to_string(asmcfg.loc_db)
...
loc_0
LEA        ECX, DWORD PTR [ECX + 0x4]
LEA        EBX, DWORD PTR [EBX + 0x1]
CMP        CL, 0x1
JZ         loc_10
->      c_next:loc_b    c_to:loc_10
loc_10
LEA        EBX, DWORD PTR [EBX + 0x1]
->      c_next:loc_13
loc_b
LEA        EBX, DWORD PTR [EBX + 0xFFFFFFFF]
JMP        loc_13
->      c_to:loc_13
loc_13
MOV        EAX, EBX
RET
```

使用堆栈初始化 Jit 引擎:

```
>>> jitter = machine.jitter(jit_type='python')
>>> jitter.init_stack()
```

在任意内存位置添加外壳代码:

```
>>> run_addr = 0x40000000
>>> from miasm2.jitter.csts import PAGE_READ, PAGE_WRITE
>>> jitter.vm.add_memory_page(run_addr, PAGE_READ | PAGE_WRITE, s)
```

创建一个 sentinelle 来捕获外壳代码的返回:

```
def code_sentinelle(jitter):
    jitter.run = False
    jitter.pc = 0
    return True

>>> jitter.add_breakpoint(0x1337beef, code_sentinelle)
>>> jitter.push_uint32_t(0x1337beef)
```

活动日志:

```
>>> jitter.set_trace_log()
```

在任意地址运行:

```
>>> jitter.init_run(run_addr)
>>> jitter.continue_run()
RAX 0000000000000000 RBX 0000000000000000 RCX 0000000000000000 RDX 0000000000000000
RSI 0000000000000000 RDI 0000000000000000 RSP 000000000123FFF8 RBP 0000000000000000
zf 0000000000000000 nf 0000000000000000 of 0000000000000000 cf 0000000000000000
RIP 0000000040000000
40000000 LEA        ECX, DWORD PTR [ECX+0x4]
RAX 0000000000000000 RBX 0000000000000000 RCX 0000000000000004 RDX 0000000000000000
RSI 0000000000000000 RDI 0000000000000000 RSP 000000000123FFF8 RBP 0000000000000000
zf 0000000000000000 nf 0000000000000000 of 0000000000000000 cf 0000000000000000
....
4000000e JMP        loc_0000000040000013:0x40000013
RAX 0000000000000000 RBX 0000000000000000 RCX 0000000000000004 RDX 0000000000000000
RSI 0000000000000000 RDI 0000000000000000 RSP 000000000123FFF8 RBP 0000000000000000
zf 0000000000000000 nf 0000000000000000 of 0000000000000000 cf 0000000000000000
RIP 0000000040000013
40000013 MOV        EAX, EBX
RAX 0000000000000000 RBX 0000000000000000 RCX 0000000000000004 RDX 0000000000000000
RSI 0000000000000000 RDI 0000000000000000 RSP 000000000123FFF8 RBP 0000000000000000
zf 0000000000000000 nf 0000000000000000 of 0000000000000000 cf 0000000000000000
RIP 0000000040000013
40000015 RET
>>> 
```

与抖动相互作用:

```
>>> jitter.vm
ad 1230000 size 10000 RW_ hpad 0x2854b40
ad 40000000 size 16 RW_ hpad 0x25e0ed0

>>> hex(jitter.cpu.EAX)
'0x0L'
>>> jitter.cpu.ESI = 12
```

## **符号执行**

正在初始化 IR 池:

```
>>> ira = machine.ira(loc_db)
>>> ircfg = ira.new_ircfg_from_asmcfg(asmcfg)
```

使用默认符号值初始化引擎:

```
>>> from miasm2.ir.symbexec import SymbolicExecutionEngine
>>> sb = SymbolicExecutionEngine(ira)
```

启动执行:

```
>>> symbolic_pc = sb.run_at(ircfg, 0)
>>> print symbolic_pc
((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
```

同样，对于步骤日志(仅显示更改):

```
>>> sb = SymbolicExecutionEngine(ira, machine.mn.regs.regs_init)
>>> symbolic_pc = sb.run_at(ircfg, 0, step=True)
Instr LEA        ECX, DWORD PTR [ECX + 0x4]
Assignblk:
ECX = ECX + 0x4
________________________________________________________________________________
ECX                = ECX + 0x4
________________________________________________________________________________
Instr LEA        EBX, DWORD PTR [EBX + 0x1]
Assignblk:
EBX = EBX + 0x1
________________________________________________________________________________
EBX                = EBX + 0x1
ECX                = ECX + 0x4
________________________________________________________________________________
Instr CMP        CL, 0x1
Assignblk:
zf = (ECX[0:8] + -0x1)?(0x0,0x1)
nf = (ECX[0:8] + -0x1)[7:8]
pf = parity((ECX[0:8] + -0x1) & 0xFF)
of = ((ECX[0:8] ^ (ECX[0:8] + -0x1)) & (ECX[0:8] ^ 0x1))[7:8]
cf = (((ECX[0:8] ^ 0x1) ^ (ECX[0:8] + -0x1)) ^ ((ECX[0:8] ^ (ECX[0:8] + -0x1)) & (ECX[0:8] ^ 0x1)))[7:8]
af = ((ECX[0:8] ^ 0x1) ^ (ECX[0:8] + -0x1))[4:5]
________________________________________________________________________________
af                 = (((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[4:5]
pf                 = parity((ECX + 0x4)[0:8] + 0xFF)
zf                 = ((ECX + 0x4)[0:8] + 0xFF)?(0x0,0x1)
ECX                = ECX + 0x4
of                 = ((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1))[7:8]
nf                 = ((ECX + 0x4)[0:8] + 0xFF)[7:8]
cf                 = (((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1)) ^ ((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[7:8]
EBX                = EBX + 0x1
________________________________________________________________________________
Instr JZ         loc_key_1
Assignblk:
IRDst = zf?(loc_key_1,loc_key_2)
EIP = zf?(loc_key_1,loc_key_2)
________________________________________________________________________________
af                 = (((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[4:5]
EIP                = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
pf                 = parity((ECX + 0x4)[0:8] + 0xFF)
IRDst              = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
zf                 = ((ECX + 0x4)[0:8] + 0xFF)?(0x0,0x1)
ECX                = ECX + 0x4
of                 = ((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1))[7:8]
nf                 = ((ECX + 0x4)[0:8] + 0xFF)[7:8]
cf                 = (((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1)) ^ ((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[7:8]
EBX                = EBX + 0x1
________________________________________________________________________________
>>>
```

使用具体的 ECX 重试执行。这里，符号/ concolic 执行到达外壳代码的结尾:

```
>>> from miasm2.expression.expression import ExprInt
>>> sb.symbols[machine.mn.regs.ECX] = ExprInt(-3, 32)
>>> symbolic_pc = sb.run_at(ircfg, 0, step=True)
Instr LEA        ECX, DWORD PTR [ECX + 0x4]
Assignblk:
ECX = ECX + 0x4
________________________________________________________________________________
af                 = (((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[4:5]
EIP                = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
pf                 = parity((ECX + 0x4)[0:8] + 0xFF)
IRDst              = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
zf                 = ((ECX + 0x4)[0:8] + 0xFF)?(0x0,0x1)
ECX                = 0x1
of                 = ((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1))[7:8]
nf                 = ((ECX + 0x4)[0:8] + 0xFF)[7:8]
cf                 = (((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1)) ^ ((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[7:8]
EBX                = EBX + 0x1
________________________________________________________________________________
Instr LEA        EBX, DWORD PTR [EBX + 0x1]
Assignblk:
EBX = EBX + 0x1
________________________________________________________________________________
af                 = (((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[4:5]
EIP                = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
pf                 = parity((ECX + 0x4)[0:8] + 0xFF)
IRDst              = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
zf                 = ((ECX + 0x4)[0:8] + 0xFF)?(0x0,0x1)
ECX                = 0x1
of                 = ((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1))[7:8]
nf                 = ((ECX + 0x4)[0:8] + 0xFF)[7:8]
cf                 = (((((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8]) & ((ECX + 0x4)[0:8] ^ 0x1)) ^ ((ECX + 0x4)[0:8] + 0xFF) ^ (ECX + 0x4)[0:8] ^ 0x1)[7:8]
EBX                = EBX + 0x2
________________________________________________________________________________
Instr CMP        CL, 0x1
Assignblk:
zf = (ECX[0:8] + -0x1)?(0x0,0x1)
nf = (ECX[0:8] + -0x1)[7:8]
pf = parity((ECX[0:8] + -0x1) & 0xFF)
of = ((ECX[0:8] ^ (ECX[0:8] + -0x1)) & (ECX[0:8] ^ 0x1))[7:8]
cf = (((ECX[0:8] ^ 0x1) ^ (ECX[0:8] + -0x1)) ^ ((ECX[0:8] ^ (ECX[0:8] + -0x1)) & (ECX[0:8] ^ 0x1)))[7:8]
af = ((ECX[0:8] ^ 0x1) ^ (ECX[0:8] + -0x1))[4:5]
________________________________________________________________________________
af                 = 0x0
EIP                = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
pf                 = 0x1
IRDst              = ((ECX + 0x4)[0:8] + 0xFF)?(0xB,0x10)
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x2
________________________________________________________________________________
Instr JZ         loc_key_1
Assignblk:
IRDst = zf?(loc_key_1,loc_key_2)
EIP = zf?(loc_key_1,loc_key_2)
________________________________________________________________________________
af                 = 0x0
EIP                = 0x10
pf                 = 0x1
IRDst              = 0x10
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x2
________________________________________________________________________________
Instr LEA        EBX, DWORD PTR [EBX + 0x1]
Assignblk:
EBX = EBX + 0x1
________________________________________________________________________________
af                 = 0x0
EIP                = 0x10
pf                 = 0x1
IRDst              = 0x10
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x3
________________________________________________________________________________
Instr LEA        EBX, DWORD PTR [EBX + 0x1]
Assignblk:
IRDst = loc_key_3
________________________________________________________________________________
af                 = 0x0
EIP                = 0x10
pf                 = 0x1
IRDst              = 0x13
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x3
________________________________________________________________________________
Instr MOV        EAX, EBX
Assignblk:
EAX = EBX
________________________________________________________________________________
af                 = 0x0
EIP                = 0x10
pf                 = 0x1
IRDst              = 0x13
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x3
EAX                = EBX + 0x3
________________________________________________________________________________
Instr RET
Assignblk:
IRDst = @32[ESP[0:32]]
ESP = {ESP[0:32] + 0x4 0 32}
EIP = @32[ESP[0:32]]
________________________________________________________________________________
af                 = 0x0
EIP                = @32[ESP]
pf                 = 0x1
IRDst              = @32[ESP]
zf                 = 0x1
ECX                = 0x1
of                 = 0x0
nf                 = 0x0
cf                 = 0x0
EBX                = EBX + 0x3
ESP                = ESP + 0x4
EAX                = EBX + 0x3
________________________________________________________________________________
>>>
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/cea-sec/miasm) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***