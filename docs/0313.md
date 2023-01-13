# BlobRunner–快速调试恶意软件分析期间提取的外壳代码

> 原文：<https://kalilinuxtutorials.com/blobrunner-shellcode-malware-analysis/>

BlobRunner 是一个简单的工具，可以快速调试恶意软件分析过程中提取的外壳代码。
BlobRunner 为目标文件分配内存，并跳转到所分配内存的基址(或偏移量)。这允许分析师以最小的开销和努力快速调试提取的工件。

## **布鲁纳大厦**

构建可执行文件非常简单，也相对容易。

##### **要求**

1.  下载并安装 Microsoft Visual C++构建工具或 Visual Studio

##### **构建步骤**

1.  打开 Visual Studio 命令提示符
2.  导航到签出 blogrunner 的目录
3.  通过运行以下命令构建可执行文件:

```
cl blobrunner.c
```

### **建筑 BlobRunner x64**

构建 x64 版本实际上与上面的相同，只是简单地使用了 x64 工具。

1.  打开 x64 Visual Studio 命令提示符
2.  导航到签出 blogrunner 的目录
3.  通过运行以下命令构建可执行文件:

```
 `cl /Feblobrunner64.exe /Foblobrunner64.out blobrunner.c
```

**也读作[BFuzz–Fuzzing Chrome&Firefox 浏览器](https://kalilinuxtutorials.com/bfuzz-fuzzing-browsers/)**

## **用途**

要调试:

1.  在您最喜欢的调试器中打开 BlobRunner。
2.  将外壳代码文件作为第一个参数传递。
3.  在跳转到外壳代码之前添加一个断点
4.  步入外壳代码

```
BlobRunner.exe shellcode.bin
```

在特定偏移量处调试到文件中。

```
BlobRunner.exe shellcode.bin --offset 0x0100
```

调试到文件中，不要在跳转之前暂停。

**警告:**确保在跳转之前设置了断点。

```
BlobRunner.exe shellcode.bin --nopause
```

##### **调试 x64 外壳代码**

x64 编译器不支持内联汇编，因此为了支持对 x64 外壳代码的调试，加载程序会创建一个挂起的线程，允许您在线程恢复之前在线程条目处放置一个断点。

##### **远程调试 Shell blob(IDA pro)**

该过程实际上与本地调试外壳代码相同，只是您需要将外壳代码文件复制到远程系统。如果文件被复制到你运行 *win32_remote.exe* 的同一个路径，你只需要使用文件名作为参数。否则，您需要指定远程系统上外壳代码文件的路径。

## **外壳代码样本**

您可以使用 Metasploit 工具 [msfvenom](https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom) 快速生成外壳代码示例。

生成简单的 Windows exec 负载。

```
msfvenom -a x86 --platform windows -p windows/exec cmd=calc.exe -o test2.bin
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/OALabs/BlobRunner) **信用:@seanmw 或@herrcore**