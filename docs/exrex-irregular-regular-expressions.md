# Exrex:正则表达式上的不规则方法

> 原文：<https://kalilinuxtutorials.com/exrex-irregular-regular-expressions/>

Exrex 是一个命令行工具和 python 模块，它可以为给定的正则表达式生成所有或者随机匹配的字符串。它是纯 python，没有外部依赖。

存在具有无限匹配字符串的正则表达式(例如:`[a-z]+`)，在这些情况下，它限制了无限部分的最大长度。

它使用生成器，所以内存的使用不依赖于匹配字符串的数量。

又念: [Sh00t:人工安全测试人员的测试环境](https://kalilinuxtutorials.com/sh00t-manual-security-testers/)

**特性**

*   帮助生成所有匹配的字符串。
*   帮助生成随机匹配字符串。
*   帮助计算匹配字符串的数量。
*   帮助简化正则表达式。

如何完成安装？

要安装它，只需运行以下命令:

**$ pip install exrex**

或者你可以尝试下面的步骤来安装它

**$ easy_install exrex**

**怎么用？**

如果是 python 模块

**导入 ex rex

ex rex . getone('(ex)r \ 1 ')
' ex rex '

list(ex rex . generate(((海){2}|world！)'))
['海海'，'世界！]]

ex rex . getone(' \ d { 4 }-\ d { 4 }-\ d { 4 }-[0-9]{ 4 } ')
' 3096-7886-2834-5671 '

ex rex . getone('(1[0-2]| 0[1-9])(:[0-5]\ d){ 2 }(A | P)M ')
' 09:31:40join(exrex . generate(' This is(a(code | cake | test)| an(apple | elf | output))。'))

这是一个代码。这是一块蛋糕。
这是一个测试。这是一个苹果。这是一个精灵。这是一个输出。
print ex rex . simplify('(ab | AC | ad)')
(a[BCD])**

**命令行用法？**

**exrex–help
用法:exrex . py[-h][-o FILE][-l][-d DELIMITER][-v]REGEX

exrex–正则表达式字符串生成器

位置参数:
REGEX REGEX 字符串

可选参数:
-h，–help 显示此帮助消息并退出
-o FILE，–输出文件
输出文件–默认为 STDOUT
-l N，–limit N Max –Max-number N 最大字符串数–默认值为-1
-r，–random 返回与 regex
-s 匹配的随机字符串，–simplify 简化正则表达式
-d 分隔符，–分隔符
分隔符–默认值为\n
-v，–详细模式**

**例子:**

**$ ex rex '[asdfg]'
a
s
d
f
g

$ ex rex-r '(0[1-9]| 1[012])-\ d { 2 } '
09-85

$ ex rex '[01]{ 10 } '-c
1024**

[**Download**](https://github.com/asciimoo/exrex)