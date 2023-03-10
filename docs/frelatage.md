# Frelatage:世界值得拥有的 Python Fuzzer

> 原文：<https://kalilinuxtutorials.com/frelatage/>

[![](img/bdab0b8cca14f648dfcd4131e169d608.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUA1nupVcazaSj7RB5c-EYWeh6ZGR91ASgB7huO14MdowuOvLCFs9Blwmdx3_eAktRzMjGeD_bcgF6AlzGY9DsBB7XJBH8I9_BA98vA2UXB3HAu_eoNZZWJOoDjUBjQ3n8WJHdy9uX8ZpY6zu9MBQDIUz9D3jIMUGJfDL_FOA5DuHh76tEGLkNYJz0/s728/frelatage_logo.png)

是一个基于覆盖率的 python 模糊库，可以用来模糊 Python 代码。Frelatage 的开发受到了其他各种 fuzzers 的启发，包括 AFL/AFL++、Atheris 和 PythonFuzz。该项目的主要目的是利用这些模糊器的最佳特性，并将它们收集到一个新工具中，以便有效地模糊 python 应用程序。

## 要求

python3

## 安装

#### 使用 pip 安装(推荐)

**pip3 安装频率**

#### 或者从源代码构建

推荐给开发者。它自动从 frelatage repo 克隆主分支，并从源代码安装。

**自动克隆 Frelatage 库并从源代码安装 Frelatage
bash<(wget-q https://raw . githubusercontent . com/rog 3 RSM 1 th/Frelatage/main/scripts/auto install . sh-O-)**

## 它是如何工作的

Frelatage 设计背后的想法是使用遗传算法来产生尽可能覆盖更多代码的突变。模糊化循环的功能可以用下图大致概括:

## 特征

#### 模糊不同的论证类型

*   线
*   （同 Internationalorganizations）国际组织
*   浮动
*   目录
*   元组
*   词典

#### 文件起毛

Frelatage 允许通过传递文件作为输入来模糊函数。

#### 起毛器效率

*   文集
*   字典(dictionary)

## 使用 Frelatage

#### 模糊一个经典参数

**import frelatage
import my _ vulnerable _ library
def my function fuzz(data):
my _ vulnerable _ library . parse(data)
input = frelatage。input(value = " initial _ value ")
f = frelatage。Fuzzer(MyFunctionFuzz，[[input]])
f.fuzz()**

#### 模糊文件参数

Frelatage 给你模糊文件类型输入参数的可能性。要初始化这些文件的值，必须在输入文件夹中创建文件(默认为`./in`)。

如果我们想初始化一个用来模糊的文件的值，我们可以这样做:

**呼应【初值】>。/in/input.txt**

然后运行 fuzzer:

**import frelatage
import my _ vulnerable _ library
def my function fuzz(data):
my _ vulnerable _ library . load _ file(data)
input = frelatage。Input(file=True，value = " input . txt ")
f = frelatage。Fuzzer(MyFunctionFuzz，[[input]])
f.fuzz()**

#### 一次加载几个文件到一个语料库

如果你需要一次加载几个文件到一个语料库中(如果你使用一个大的语料库是有用的)，你可以使用 Frelatage `**load_corpus**`的内置函数。这个函数返回一个输入列表。

`**load_corpus(directory: str, file_extensions: list) -> list[Input]**`

*   目录:输入目录的子目录(相对路径)，如 **`./`、`./images`**
*   file_extensions:包含在语料库条目中的文件扩展名列表，例如 **`["jpeg", "gif"]`、`["pdf"]`**

**import frelatage
import my _ vulnerable _ library
def my function fuzz(data):
my _ vulnerable _ library . Load _ file(data)
my _ vulnerable _ library . Load _ file(data 2)
加载。/in 目录
corpus _ 1 = frela tage . load _ corpus(directory = "。/)
加载每。gif/。中的 jpeg 文件。/in/images 子目录
corpus _ 2 = frela tage . load _ corpus(directory = "。/images "，file_extension=["gif "，" jpeg"])
f = frelatage。Fuzzer(MyFunctionFuzz，[语料库 _1，语料库 _2])
f.fuzz()**

#### 用字典弄模糊

您可以在词典专用目录中复制一个或多个词典(默认为`**./dict**`)。

#### 差分模糊化

差异模糊化是一种流行的软件测试技术，它试图通过向多个库/程序提供相同的输入并观察它们行为的差异来检测 bug。你会在这里找到一个使用`**json**`和`**ujson**`库的差分模糊化的例子。

#### 例子

您可以在示例目录中找到更多模糊器和语料库的示例。

*   用 Frelatage 对枕头进行模糊处理，以发现漏洞和缺陷

## 报告

每次崩溃都保存在输出文件夹中(默认为`**./out**`)，文件夹名为:`**id:<crash ID>,err:<error**` **`type>,err_pos:<error>,err_file:<error file>`。**

报告目录采用以下形式:

**输出
──id:，err:，err_file:，err_pos:
【输入】
【0】

】**

#### 阅读事故报告

传递给函数的输入在保存到`**<report_folder>/input file**`之前使用 pickle 模块进行序列化。因此，有必要对其进行反序列化，以便能够读取文件的内容。这个动作可以用这个脚本来执行。

**。/read_report.py 输入**

## 配置

有两种方法可以设置 Frelatage:

#### 使用环境变量

| 环境变量 | 描述 | 可能的值 | 缺省值 |
| --- | --- | --- | --- |
| **FRELATAGE _ DICTIONARY _ ENABLE** | 允许使用基于字典元素的突变 | `**1**`启用，`**0**`否则 | `**1**` |
| **频率 _ 超时 _ 延迟** | 函数返回 TimeoutError 之前的延迟时间(秒) | **`1`–`infinity`** | `**2**` |
| **文件输入文件目录** | 存储输入文件的临时文件夹 | 文件夹的绝对路径，例如`**/tmp/custom_dir**` | `**/tmp/frelatage**` |
| **频率输入最大长度** | 输入变量的最大字节数 | **`4`–**`**infinity**` | `**4094**` |
| **最大线程数** | 最大并发线程数 | `**8**`–`**infinity**` | `**8**` |
| **最大周期数无新路径数** | 没有找到新路径的循环数，在此之后我们进入下一阶段 | **`10`–`infinity`** | `**5000**` |
| **频率输入方向** | 包含初始输入文件的目录。它需要是一个相对路径(到模糊文件的路径) | 文件夹的相对路径，例如`**./in**` | `**./in**` |
| **频率 _ 字典 _ 目录** | 词典的默认目录。它需要是一个相对路径(到模糊文件的路径) | 文件夹的相对路径，例如`**./dict**` | `**./dict**` |
| **频率 _ 调试 _ 模式** | 启用调试模式(显示频率崩溃时的错误) | `**1**`启用，`**0**`否则 | `**1**` |

配置示例:

**export FRELATAGE _ DICTIONARY _ ENABLE = 1&&
export FRELATAGE _ time out _ DELAY = 2&&
export FRELATAGE _ INPUT _ FILE _ TMP _ DIR = "/TMP/FRELATAGE "&&
export FRELATAGE _ INPUT _ MAX _ LEN = 4096&&
export FRELATAGE _ MAX _ THREADS = 8&&
export FRELATAGE _ MAX _ CYCLES _ WITHOUT _ WITHOUT/in "&&
export frela tage _ DICTIONARY _ DIR = "。/dict "&&
python 3 fuzzer . py**

将参数传递给模糊化器

**def myfunction(input1_string，input 2 _ int):
pass
input 1 = frelatage。input(value = " initial _ value ")
input 2 = frelatage。输入(值=2)
f =频率。Fuzzer(
#您要模糊的方法
method=myfunction，
# Corpus
corpus=[[input1]，[input2]]，
#线程数
threads_count=8，
#将被考虑的异常
Exceptions _ whitelist =(OSError)，
#将不被考虑的异常
exceptions_blacklist=()，
#将存储错误报告的目录【T16/out "，
#启用或禁用静音模式
silent=False，
#启用或禁用无限模糊化
infinite _ fuzz = False
)
f . fuzz()**

[**Download**](https://github.com/Rog3rSm1th/Frelatage)