# Libinjection : SQL / SQLI 记号赋予器解析器分析器

> 原文：<https://kalilinuxtutorials.com/libinjection/>

[![Libinjection : SQL / SQLI Tokenizer Parser Analyzer](img/9d7a11f0e8c486af278bc576b7772a18.png "Libinjection : SQL / SQLI Tokenizer Parser Analyzer")](https://1.bp.blogspot.com/-Zaz9la0wc9c/YM4DFA7Op1I/AAAAAAAAJnU/PQmgRjxIt5M85EwZFmPYzV-iJN8-2-GuQCLcBGAsYHQ/s728/Libinjection%25281%2529.png)

Libinjection 是一个 SQL / SQLI 记号赋予器解析器分析器。为

*   C 和 C++
*   [PHP](https://libinjection.client9.com/doc-sqli-php)
*   [Python](https://libinjection.client9.com/doc-sqli-python)
*   月球
*   [Java](https://github.com/jeonglee/Libinjection) (外部端口)
*   [Lua JIT/FFI]([https://github.com/p0pr0ck5/lua-ffi-libinjection](https://github.com/p0pr0ck5/lua-ffi-libinjection))(外部端口)

简单的例子

#**include
# include
# include
# include " libinject . h "
# include " libinject _ sqli . h "
int main(int argc，const char * argv[])
{
struct libinject _ sqli _ state；
int is sqli；
const char * input = argv[1]；
size_t slen = strlen(输入)；
/*在现实世界中，你会对输入进行 url 解码，etc */
libinject _ sqli _ init(&state，input，slen，FLAG _ NONE)；
is sqli = lib inject _ is _ sqli(&州)；
if(is sqli){
fprintf(stderr，"检测到指纹为“%s”的 sqli \ n "，state . fingerprint)；
}
返回 issqli
}**

**$ gcc-Wall-we xtra examples . c lib injection _ sqli . c
$。/a . out "-1 ' and 1 = 1 union/* foo */select load _ file('/etc/passwd ')–"
用的& 1UE'** 的指纹检测到 sqli

更多高级样本:

*   [sqli_cli.c](https://github.com/client9/libinjection/blob/master/src/sqli_cli.c)
*   [reader.c](https://github.com/client9/libinjection/blob/master/src/reader.c)
*   [fptool](https://github.com/client9/libinjection/blob/master/src/fptool.c)

**版本信息**

版本被列为“major.minor.point”

主要是对 API 和/或指纹格式的重大更改。应用程序将需要重新编译和/或重构。

轻微的 C 代码更改。这些可能包括

*   要检测或抑制的逻辑变化
*   优化变化
*   代码重构

点发布纯粹是数据变更。这些可以安全地应用。

**质量和诊断**

在[https://travis-ci.org/client9/libinjection](https://travis-ci.org/client9/libinjection)的连续积分结果测试如下:

*   GCC 下的构建和单元测试
*   Clang 下的构建和单元测试
*   使用 [clang 静态分析仪](http://clang-analyzer.llvm.org/)进行静态分析
*   使用 [cppcheck](https://github.com/danmar/cppcheck) 进行静态分析
*   使用 [valgrind](http://valgrind.org/) 检查内存错误
*   使用[工作服在线编写代码覆盖率。io](https://coveralls.io/github/client9/libinjection)

[**Download**](https://github.com/client9/libinjection)