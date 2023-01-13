# recovery:从您的终端交互式查找和恢复删除或覆盖的文件

> 原文：<https://kalilinuxtutorials.com/recoverpy/>

[![](img/a3c07c3369dde5ca2a8a8489ced14e4b.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhE0ZCspu8C_xNIF-o1qK-n7iVbzT-FVK2MV5dI8WZFGkIabL75oafeZ6wUJ8LcC09DiqYluE--dsWRXMoP_v2GRuU6XVFZfFut21Ns4_OIvbvF4YGddUIch7kR2E0Lzz0gCrmBRiKZnt75wjVJIQ5OkHboXngC7iBrw9OneMfXaTVMcVJB0M7Y2U-P=s1192)

**RecoverPy** 搜索分区的每个块以找到您的请求。你已经可以找到很多恢复被删除文件的解决方案，但是恢复被覆盖的文件可能会很麻烦。

# 装置

RecoverPy 目前仅在 Linux 系统上可用。

#### 属国

**强制:**为了列出和搜索分区，recoverpy 使用`**grep**`、`d**d**`和`**lsblk**`命令。

**可选:**要显示实时 grep 进度，可以安装`**progress**`。

要安装所有依赖项:

*   类 debian:`**apt install grep coreutils util-linux progress**`
*   拱门:`**pacman -S grep coreutils util-linux progress**`
*   Fedora: `**dnf install grep coreutils util-linux progress**`

#### 从 pip 安装

`**python3 -m pip install recoverpy**`

## 用法

**python 3-m recovery**

*如果你没有以根用户身份登录，在执行前使用`**sudo recoverpy**`或使用`**su -**`登录。*

* * *

**选择文件所在的系统分区**。如果你运气不好，你可以在你的主分区中搜索，也许是你的 IDE，文本编辑器等等。在某个时候做了备份。

**输入文本字符串以搜索**。请参阅下面的提示以获得更好的效果。

注意，在整个分区中搜索一个字符串可能需要*一段时间*。(见委婉语)

默认保存路径为`**/tmp/**`，点击设置编辑配置。

**开始搜索**，结果会出现在左边的框中。

**选择一个结果**在右边的框中显示相应的分区块内容。

一旦你找到了你的宝贝，**选择`Save`** 。

现在，您可以单独保存该块，也可以浏览文件剩余部分的相邻块。然后，您可以将其全部保存在一个文件中。

[Download](https://github.com/PabloLec/RecoverPy)