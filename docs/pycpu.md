# py CPU–中央处理器信息收集工具

> 原文：<https://kalilinuxtutorials.com/pycpu/>

**PyCPU** 工具您可以访问您的处理器信息的详细信息。还可以根据所用处理器的当前处理器信息来检查安全漏洞。

## **PyCPU 运行**

```
root@ismailtasdelen:~# git clone https://github.com/ismailtasdelen/PyCPU.git
root@ismailtasdelen:~# cd PyCPU
root@ismailtasdelen:~/PyCPU# python PyCPU.py
```

**也读作 [瘴气 Python 中的逆向工程框架](https://kalilinuxtutorials.com/miasm-reverse-engineering-framework/)**

## 工具菜单上有什么？

```
[1] CPU All Information Gathering
[2] Default Information Gathering
[3] CPU Vulnerability Check
[4] Exit
```

all _ CPU()–>调用函数。实际上这个函数是`cat /proc/cpuinfo`运行系统中的代码。我们可以获取所有信息。

```
processor	: 0
vendor_id	: GenuineIntel
cpu family	: 6
model		: 69
model name	: Intel(R) Core(TM) i5-4210U CPU @ 1.70GHz
stepping	: 1
microcode	: 0x1c
cpu MHz		: 1700.062
cache size	: 3072 KB
physical id	: 0
siblings	: 4
core id		: 0
cpu cores	: 2
apicid		: 0
initial apicid	: 0
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm epb tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid xsaveopt dtherm ida arat pln pts
bugs		:
bogomips	: 4788.92
clflush size	: 64
cache_alignment	: 64
address sizes	: 39 bits physical, 48 bits virtual
power management:
......
```

函数显示了一些简单的 cpu 信息。

```
vendor_id	: GenuineIntel
model name	: Intel(R) Core(TM) i5-4200U CPU @ 1.60GHz
microcode	: 0x24
cpu MHz		: 2446.218
cpu MHz		: 2574.107
cpu MHz		: 2294.998
cpu MHz		: 2295.091
cache size	: 3072 KB
```

函数在你运行的计算机上执行漏洞检查。

```
bugs : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf
```

#### **克隆现有存储库(使用 HTTPS 克隆)**

```
root@ismailtasdelen:~# git clone https://github.com/ismailtasdelen/PyCPU.git
```

#### **克隆现有存储库(使用 SSH 克隆)**

```
root@ismailtasdelen:~# git clone https://github.com/ismailtasdelen/PyCPU.git
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/ismailtasdelen/PyCPU) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***