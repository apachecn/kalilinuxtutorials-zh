# ELFXtract:一个用于枚举 ELF 二进制文件的自动化分析工具

> 原文：<https://kalilinuxtutorials.com/elfxtract-2/>

[![](img/400edba9fefc2e1f9c841f8b176819b3.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjKfCgl49is06_5bkz3fgurFKH6WZOAI18UEtLyaIAnHTx85Ub_0jr2RkCgyDgIM76N39Az9Rh8VAZKH3v27RjsYEEfwUFAtj6X-3wJH0SmVjsKJQO9iqZ6O_u-x3D83NNLEJZIsvBHr_j1wh4vmOBGmJXYkShK4vkAbWeAmBdKdKO8pKKqnOPLGnei=s728)

ELFXtract 是一个自动分析工具，用于枚举 ELF 二进制文件

由 Radare2 和 r2ghidra 提供动力

这是专门为 PWN 挑战开发的，它有许多自动化功能

它几乎显示了 ELF 的每一个细节，还使用`**r2ghidra**`将它的 ASM 反编译成 C 代码

在 Ghidra 中反编译 elf 需要更多的时间，但是在**elf extract**中，它在几秒钟内反编译并显示

**elf xtract 中的特性**

*   文件信息
*   共享对象依赖关系详细信息
*   ELF 安全缓解详细信息/检查秒
*   字符串详细信息
*   标题存储器映射
*   ROP 小工具
*   PLT 表
*   有桌子吗
*   功能表
*   ASM 功能代码
*   反编译的函数代码
*   预测可能易受攻击的功能

**安装**

**git 克隆 https://github.com/AidenPearce369/elfxtract
CD elf xtract
chmod+x install . sh
。/install.sh
pip install -r 需求. txt**

**工作**

您可以对任何 ELF 运行 **elfxtract** 和`**-a**`来列出 ELF 的所有细节

**ra@ubuntu:~/elfxtract$ python3 main.py –file programvuln -a
*_* _ | *| | |* \ \ / / | | |
| | | | | |_ \ V /| |_ _ *_ _* _ *| |_ | || | | *| / |* | ‘/ ` |/ | | | |*| |*| | / /^\ \ || | | (| | (| |
_*/_____/_| \/ \/__|*| _*,*|__*|__|
@aidenpearce369 > FILE INFO :
ELF Name : programvuln
ELF Type : ELF 64-bit LSB shared object
ELF Arch : x86-64
ELF SHA1 Hash : BuildID[sha1]=cf149d97ad1e895561080b1f5c317bc5bc1e8652
This binary is dynamically linked & not stripped
SHARED OBJECT DEPENDENCY :
linux-vdso.so.1 (0x00007ffd525a4000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fd610d93000)
/lib64/ld-linux-x86-64.so.2 (0x00007fd610fa1000)
ELF SECURITY MITIGATIONS :
RELRO : Full RELRO
STACK CANARY : No Canary found
NX BIT : NX disabled
PIE : PIE enabled
RPATH : No RPATH
RUNPATH : No RUNPATH
POSSIBLE STRINGS :
nth paddr vaddr len size section type string
0 0x00002008 0x00002008 31 32 .rodata ascii You have bypassed this function
1 0x00002028 0x00002028 12 13 .rodata ascii cat flag.txt
2 0x00002035 0x00002035 15 16 .rodata ascii Enter your name
3 0x00002045 0x00002045 13 14 .rodata ascii Your name is
RODATA HEXDUMP :
0x00002000 01000200 00000000 596f7520 68617665 ……..You have
0x00002010 20627970 61737365 64207468 69732066 bypassed this f
0x00002020 756e6374 696f6e00 63617420 666c6167 unction.cat flag
0x00002030 2e747874 00456e74 65722079 6f757220 .txt.Enter your
0x00002040 6e616d65 00596f75 72206e61 6d652069 name.Your name i
0x00002050 732000 s .
ELF ENTRY POINT :
The entry point of the ELF is at 0x10c0
HEADER MEMORY MAP :
Type Offset VirtAddr PhysAddr
FileSiz MemSiz Flags Align
PHDR 0x0000000000000040 0x0000000000000040 0x0000000000000040
0x00000000000002d8 0x00000000000002d8 R 0x8
INTERP 0x0000000000000318 0x0000000000000318 0x0000000000000318
0x000000000000001c 0x000000000000001c R 0x1
[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
LOAD 0x0000000000000000 0x0000000000000000 0x0000000000000000
0x00000000000006a8 0x00000000000006a8 R 0x1000
LOAD 0x0000000000001000 0x0000000000001000 0x0000000000001000
0x00000000000002b5 0x00000000000002b5 R E 0x1000
LOAD 0x0000000000002000 0x0000000000002000 0x0000000000002000
0x00000000000001c8 0x00000000000001c8 R 0x1000
LOAD 0x0000000000002da0 0x0000000000003da0 0x0000000000003da0
0x0000000000000270 0x0000000000000278 RW 0x1000
DYNAMIC 0x0000000000002db0 0x0000000000003db0 0x0000000000003db0
0x00000000000001f0 0x00000000000001f0 RW 0x8
NOTE 0x0000000000000338 0x0000000000000338 0x0000000000000338
0x0000000000000020 0x0000000000000020 R 0x8
NOTE 0x0000000000000358 0x0000000000000358 0x0000000000000358
0x0000000000000044 0x0000000000000044 R 0x4
GNU_PROPERTY 0x0000000000000338 0x0000000000000338 0x0000000000000338
0x0000000000000020 0x0000000000000020 R 0x8
GNU_EH_FRAME 0x0000000000002054 0x0000000000002054 0x0000000000002054
0x000000000000004c 0x000000000000004c R 0x4
GNU_STACK 0x0000000000000000 0x0000000000000000 0x0000000000000000
0x0000000000000000 0x0000000000000000 RWE 0x10
GNU_RELRO 0x0000000000002da0 0x0000000000003da0 0x0000000000003da0
0x0000000000000260 0x0000000000000260 R 0x1
[*] Loaded 14 cached gadgets for ‘programvuln’ ROP GADGETS : 0x1017 : add esp, 8;ret 0x1016 : add rsp, 8;ret 0x1221 : leave;ret 0x128c : pop r12;pop r13;pop r14;pop r15;ret 0x128e : pop r13;pop r14;pop r15;ret 0x1290 : pop r14;pop r15;ret 0x1292 : pop r15;ret 0x128b : pop rbp;pop r12;pop r13;pop r14;pop r15;ret 0x128f : pop rbp;pop r14;pop r15;ret 0x1193 : pop rbp;ret 0x1293 : pop rdi;ret 0x1291 : pop rsi;pop r15;ret 0x128d : pop rsp;pop r13;pop r14;pop r15;ret 0x101a : ret PLT TABLE : cxa_finalize : 0x1074 puts : 0x1084 system : 0x1094 printf : 0x10a4 gets : 0x10b4 GOT TABLE : *ITM_deregisterTMCloneTable : 0x3fd8 __libc_start_main : 0x3fe0 __gmon_start* : 0x3fe8 _ITM_registerTMCloneTable : 0x3ff0 __cxa_finalize : 0x3ff8 puts : 0x3fb8 system : 0x3fc0 printf : 0x3fc8 gets : 0x3fd0 FUNCTION TABLE : __libc_csu_fini : 0x12a0 __libc_csu_init : 0x1230 win : 0x11a9 _start : 0x10c0 main : 0x11d POSSIBLE USER DEFINED FUNCTIONS : win : 0x11a9 main : 0x11d6 ASSEMBLY AND DECOMPILED CODE : [] ASM – win :
┌ 45: sym.win ();
│ 0x000011a9 f30f1efa endbr64
│ 0x000011ad 55 push rbp
│ 0x000011ae 4889e5 mov rbp, rsp
│ 0x000011b1 488d3d500e00\. lea rdi, str.You_have_bypassed_this_function ; 0x2008 ; “You have bypassed this function” ; const char *format
│ 0x000011b8 b800000000 mov eax, 0
│ 0x000011bd e8defeffff call sym.imp.printf ; int printf(const char *format)
│ 0x000011c2 488d3d5f0e00\. lea rdi, str.cat_flag.txt ; 0x2028 ; “cat flag.txt” ; const char *string
│ 0x000011c9 b800000000 mov eax, 0
│ 0x000011ce e8bdfeffff call sym.imp.system ; int system(const char *string)
│ 0x000011d3 90 nop
│ 0x000011d4 5d pop rbp
└ 0x000011d5 c3 ret
[] DECOMPILED CODE – win : void sym.win(void) { sym.imp.printf(“You have bypassed this function”); sym.imp.system(“cat flag.txt”); return; } [] ASM – main :
; DATA XREF from entry0 @ 0x10e1
┌ 77: int main (int argc, char **argv, char **envp);
│ ; var char *s @ rbp-0x40
│ 0x000011d6 f30f1efa endbr64
│ 0x000011da 55 push rbp
│ 0x000011db 4889e5 mov rbp, rsp
│ 0x000011de 4883ec40 sub rsp, 0x40
│ 0x000011e2 488d3d4c0e00\. lea rdi, str.Enter_your_name ; 0x2035 ; “Enter your name” ; const char *s
│ 0x000011e9 e892feffff call sym.imp.puts ; int puts(const char *s)
│ 0x000011ee 488d45c0 lea rax, [s]
│ 0x000011f2 4889c7 mov rdi, rax ; char *s
│ 0x000011f5 b800000000 mov eax, 0
│ 0x000011fa e8b1feffff call sym.imp.gets ; char *gets(char *s)
│ 0x000011ff 488d3d3f0e00\. lea rdi, str.Your_name_is* ; 0x2045 ; “Your name is ” ; const char *format
│ 0x00001206 b800000000 mov eax, 0
│ 0x0000120b e890feffff call sym.imp.printf ; int printf(const char *format)
│ 0x00001210 488d45c0 lea rax, [s]
│ 0x00001214 4889c7 mov rdi, rax ; const char *s
│ 0x00001217 e864feffff call sym.imp.puts ; int puts(const char *s) │ 0x0000121c b800000000 mov eax, 0 │ 0x00001221 c9 leave └ 0x00001222 c3 ret [*] DECOMPILED CODE – main :
WARNING: [r2ghidra] Failed to match type char * for variable s to Decompiler type:
undefined8 main(void)
{ undefined8 s;
sym.imp.puts(“Enter your name”);
sym.imp.gets(&s);
sym.imp.printf(“Your name is “);
sym.imp.puts(&s);
return 0;
}
VULNERABLE FUNCTIONS :
Possible vulnerability locations – Command Execution
0x000011ce e8bdfeffff call sym.imp.system ; int system(const char *string)
Possible vulnerability locations – Format String
0x000011bd e8defeffff call sym.imp.printf ; int printf(const char *format)
0x0000120b e890feffff call sym.imp.printf ; int printf(const char *format) Possible vulnerability locations – Buffer Overflow
0x000011fa e8b1feffff call sym.imp.gets ; char *gets(char *s)**

您还可以传递参数并根据需要获取信息，

**ra @ Ubuntu:~/elf xtract $ python 3 main . py-h
__ |*| |*\ \//| |
| | | | |*_ _*_*| _ | | | |*|/|*|/'/` |/|*|*| |【/^\ \ | | |(| |(| |
_*/_ _ _ _ _/_ | \/\/_ _ |*| _*，*| _ _*| _ _ | |
@ aiden peace 369
用法:main.py [-h] -f 文件[-a][-I][-g][–user-func][–GET-func GET _ FUNC][–ASM-only][–反编译 T22 –gadgets 显示 gadgets
–user-func 显示用户自定义函数的细节
–GET-func GET _ FUNC 显示给定函数
的 ASM &反编译代码–ASM-仅显示 ELF**
的 ASM—**-反编译-仅显示 ELF
-t 的反编译 C 代码，–tables 显示 PLT，GOT &函数表**

[**Download**](https://github.com/AidenPearce369/elfxtract)