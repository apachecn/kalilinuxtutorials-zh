# 模糊 Chrome 和 Firefox 浏览器

> 原文：<https://kalilinuxtutorials.com/bfuzz-fuzzing-browsers/>

BFuzz 是一个基于输入的 fuzzer 工具，它以`**.html**`作为输入，用一个新的实例打开你的浏览器，并传递多个由 domato 生成的测试用例，这些测试用例存在于 BFuzz 的`**recurve**`文件夹中。

**也读作** [**Python-Nubia:一个命令行&交互外壳框架**](https://kalilinuxtutorials.com/python-nubia/)

## **运行 BFuzz**

```
warmachine@ftw:~/BFuzz$ ./generate.sh
warmachine@ftw:~/BFuzz$ python BFuzz.py 
Enter the browser type:
 1: Chrome 
 2: Firefox
>>
```

运行`**python BFuzz.py**`将询问选项天气以模糊 Chrome 或 Firefox，但是如果选择`2`这将打开 Firefox `**firefox --new-instance**`并随机打开来自`**recurve**`的任何测试用例在终端上创建日志等待`**3 seconds**`再次打开 Firefox，同样的过程继续下去。

BFuzz 是一个小的`**.py**`脚本，它能够打开 **`12 seconds`** 的浏览器运行测试用例，然后关闭等待`**3 seconds**`，并再次遵循相同的过程。

## 驯服

`**recurve**`中的测试用例由 domato generator.py 生成，py 包含主脚本。它使用 grammar.py 作为库，并包含额外的 DOM fuzzing 辅助代码。

grammar.py 包含的生成引擎大多与应用程序无关，因此可以用于其他(即非 DOM)基于生成的模糊器。因为它可以用作库，所以它的用法将在下面单独的一节中描述。

。txt 文件包含语法定义。有 3 个主要文件，html.txt、css.txt 和 js.txt，它们分别包含 html、css 和 JavaScript 语法。这些根语法文件可能包含来自其他文件的内容。

## **视频教程**

[https://www.youtube.com/embed/I59SkL0ReUM?feature=oembed](https://www.youtube.com/embed/I59SkL0ReUM?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/RootUp/BFuzz)