# Stegify:用于 LSB 隐写术的 Go 工具，能够隐藏图像中的任何文件

> 原文：<https://kalilinuxtutorials.com/stegify-lsb-steganographycapable-hiding-file-within-image/>

[![Stegify : Go Tool For LSB Steganography,Capable Of Hiding Any File Within An Image](img/355121eeda8b88cdcde2c43eabc377c2.png "Stegify : Go Tool For LSB Steganography,Capable Of Hiding Any File Within An Image")](https://1.bp.blogspot.com/-Zv3Sb70o8Lo/XYL8EzsXv6I/AAAAAAAACho/xkd0Vz3_Oy4ar3Lr3qSCnoNOAt5L7Z2cQCLcBGAsYHQ/s1600/Carrier.png)

**Stegify** 是 LSB 隐写术的 Go 工具，能够隐藏图像中的任何文件。

这是一个简单的命令行工具，能够完全透明地隐藏图像中的任何文件。这种技术被称为 LSB(最低有效位)

**安装**

**$ go get-u github.com/DimitarPetrov/stegify**

**用途**

作为命令行工具

**$ stegify -op 编码-载波-数据-结果
$ stegify -op 解码-载波-结果**

编码时，名为标志***-数据*** 的文件隐藏在名为标志***-载体*** 的文件中，生成的文件以名为标志***-结果*** 保存在当前工作目录下的新文件中。

结果文件的文件扩展名继承自载体文件，不得在***-结果标志*** 中明确指定。

解码时，给定一个包含先前编码数据的载体文件的文件名，提取数据并保存在当前工作目录下的新文件中，文件名为标志***-结果*** 。

结果文件没有任何文件扩展名，因此应该在***-结果*** 标志中明确指定。

在这两种情况下，标志***-结果*** 都可以省略，它将被用作默认文件名:结果

**在你的代码中编程**

***stegify*** 也可以通过编程来使用，它提供了易于使用的函数来处理文件名或原始读取器和写入器。详情可以访问 steg 包下的 godoc。

**演示**

[![](img/58833e21ea61cccc7a13d01ca66a925b.png)](https://1.bp.blogspot.com/-7G-qxVcyHVY/XYL7HFoyEeI/AAAAAAAAChM/6PvQm6qvzhUw7Sutwx4hMglQaEhOJyH0wCLcBGAsYHQ/s1600/Carrier.jpeg)

**Carrier**

![](img/dbbdea613455d0d0ae78d7d5a25b0f49.png)

**Data**

![](img/a603195c170fa683e129ca8a12071b8f.png)

**Result**

`**Result**` 文件包含了隐藏在其中的`**Data**` 文件。如你所见，它是完全透明的。

**免责声明**

如果载体文件是 jpeg 或 jpg 格式，则编码后的结果文件图像将是 png 编码的(因此其大小可能更大),尽管文件扩展名是从原始载体文件继承而来的(即。jpeg 或者。jpg)。

[**Download**](https://github.com/DimitarPetrov/stegify)