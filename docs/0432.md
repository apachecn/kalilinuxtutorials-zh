# Angr:一个强大且用户友好的二进制分析平台

> 原文：<https://kalilinuxtutorials.com/angr-user-friendly-binary-analysis/>

Angr 是一个平台无关的二进制分析框架。它是一套 Python 3 库，允许您加载二进制文件并对其做许多很酷的事情:

*   拆卸和中间表示提升
*   程序仪表化
*   符号执行
*   控制流分析
*   数据相关性分析
*   价值集分析(VSA)
*   反编译

最常见的 angr 操作是加载二进制文件:`**p = angr.Project('/bin/bash')**`如果你在 IPython 这样的增强 REPL 中这样做，你可以使用 tab 键自动完成来浏览[顶级可访问的方法](http://docs.angr.io/docs/toplevel.html)和它们的文档字符串。

“如何安装 angr”的简称是`**mkvirtualenv --python=$(which python3) angr && python -m pip install angr**`。

**又读——[用牛肉黑客——假冒 Flash 更新，安装插件，窃取脸书& Gmail 凭证](https://kalilinuxtutorials.com/hacking-with-beef/)**

**例子**

angr 做了很多二进制分析的东西。为了让您入门，这里有一个在 CTF 挑战中使用符号执行获取旗帜的简单示例。

**导入 angr
项目= angr。project(" angr-doc/examples/def camp _ r100/r100 "，auto _ load _ libs = False)
@ project . hook(0x 400844)
def print _ FLAG(state):
(FLAG 应为:"，state . POSIX . dumps(0))
project . termin ate _ execution()
project . execute()**

**安装**

麦克·OS X

应该可以，但是有一些注意事项。

angr 需要`**unicorn**`库，这个库(在撰写本文时)`pip`必须在 macOS 上从源代码构建，即使其他平台上存在二进制发行版(“wheels”)。

从源代码构建`**unicorn**`需要 Python 2，所以在`**python**`获得 Python 3 的 virtualenv 中会失败。如果你在使用`**pip install angr**`时遇到错误，你可能需要首先单独安装`**unicorn**`，将它指向你的 Python 2:

UNICORN _ QEMU _ FLAGS = "–Python =/path/to/Python 2 " pip 安装 unicorn # Python 2 在您的 macOS 系统上可能是/usr/bin/python

然后重试`**pip install angr**`。

如果这仍然不起作用，并且您遇到了带有 Clang 的不完整的构建脚本，请尝试使用 GCC。

**brew install gcc
CC =/usr/local/bin/gcc-8 UNICORN _ QEMU _ FLAGS = "–python =/path/to/python 2″pip install UNICORN #截至本文撰写之时，brew install gcc 为您提供 gcc-8
pip install angr**

安装 angr 后，您需要为 angr 本地库修复一些共享库路径。激活您的虚拟 env 并执行下面几行。在 angr-dev repo 中提供了一个脚本。

py vex =`python3 -c 'import pyvex; print(pyvex.__path__[0])'`UNICORN =`python3 -c 'import unicorn; print(unicorn.__path__[0])'`
ANGR =`python3 -c 'import angr; print(angr.__path__[0])'`
install _ name _ tool-change lib UNICORN . 1 . dylib " $ UNICORN "/lib/lib UNICORN . dylib " $ ANGR "/lib/angr _ native . dylib
install _ name _ tool-change libpyvex . dylib " $ py vex "/lib/libpyvex . dylib " $ ANGR "/lib/angr _ native . dylib

**窗户**

像往常一样，强烈推荐 virtualenv。为此你可以使用[虚拟赢](https://pypi.org/project/virtualenvwrapper-win/)或者[虚拟赢](https://pypi.python.org/pypi/virtualenv)软件包。

angr 可以从 Windows 上的 pip 安装，同上:`**pip install** **angr**`。使用这种设置，您不需要构建任何 C 代码，因为对于 angr 及其依赖项，轮子(二进制发行版)应该会被自动拉下来。

**开发安装**

有一个特殊的脚本库`**angr-dev**`,让 angr 开发者的生活更轻松。您可以通过运行以下命令在开发模式下设置 angr:

git 克隆 https://github.com/angr/angr-dev
CD angr-dev
/setup.sh -i -e angr

这将创建一个 virtualenv ( `**-e angr**`)，检查您可能需要的任何依赖项(`**-i**`)，克隆所有的存储库并以可编辑模式安装它们。`**setup.sh**`甚至可以为你创建一个 PyPy virtualenv(用`**-p**`代替`**-e**`，从而显著提高性能和降低内存使用。

您可以就地分支/编辑/重新编译各种模块，它将自动反映在您的虚拟环境中。

**windows 上的开发安装**

angr-dev 存储库有一个 setup.bat 脚本，它创建了与上面相同的设置，尽管它没有 setup.sh 那么神奇。

因为我们将构建 C 代码，所以您必须在 visual studio 开发人员命令提示符下。确保如果您使用的是 64 位 python 解释器，那么您也使用了 64 位构建工具(`**VsDevCmd.bat -arch=x64**`)

**pip 安装 virtualenv
git 克隆 https://github.com/angr/angr-dev
CD angr-dev
virtualenv-p " C:\ Path \ To \ python 3 \ python . exe " env
env \ Scripts \ activate
setup . bat**

你也可以用`**virtualenvwrapper-win**`包代替上面的`**virtualenv**`来获得更流畅的体验。

**Docker 安装**

为了方便起见，我们提供了一个 Docker 映像，保证 99%可以正常工作。您可以通过 docker 进行安装:

**安装坞站
【curl-SSL https://get . docker . com/| sudo sh

拉坞站形象
【sudo 坞站拉生气/愤怒】
运行它
【sudo 坞站运行-它生气/愤怒】**

docker 内外的文件同步留给用户来做练习(提示:查看`**docker -v**`)。

**修改 angr 容器**

你可能会发现自己需要通过 apt 安装额外的包。容器的普通版本没有安装 sudo 包，这意味着容器中的默认用户不能提升权限来安装其他包。

要克服这个障碍，请使用以下 docker 命令授予自己 root 访问权限:

**#假设 docker 容器运行的是
#名为“angr”，实例是
#在后台运行。
docker exec-ti-u root angr bash**

[**Download**](https://github.com/angr/angr)