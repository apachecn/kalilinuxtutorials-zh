# 肢解:扫描内存中的秘密和更多

> 原文：<https://kalilinuxtutorials.com/dismember/>

[![](img/5b653196f287b5a2767a12e378937f7a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiIt3XUHmPvC1JI47DZz5Q-RZOlehIeLAFxptwg8kYelD1VNPT0cUC3Gf0s9yGzAyKdzdgh1EeDKiiWO-HM1LIOoIuEwcRSPeQoBEML7un4TKoT_JgFfDrxawJf52LVxw9Av-VwjueccZbXtfvRUbC5DHs-wPyaIuZK9yBtgi-8JkreAcq3XhZL76mQ/s1573/demo.gif)

**肢解**是一个用于 Linux 的命令行工具包，可以用来扫描所有进程(或特定进程)的内存，寻找公共秘密和自定义正则表达式，等等。

它最终将成为一个完整的工具包。

![](img/5b653196f287b5a2767a12e378937f7a.png)

使用`grep`命令，它可以在所有内存中为所有(可访问的)进程匹配一个正则表达式。这可以用来查找内存中的敏感数据，通过内存中包含的内容来识别进程，或者查询进程内存中感兴趣的信息。

通过`scan`命令包含了许多内置的模式，它有效地作为一个秘密扫描器扫描你机器上的内存。

肢解可以用来搜索它可以访问的所有进程的内存，因此以 root 用户身份运行它是最有效的方法。

命令还包括列出进程，探索进程状态和相关信息，绘制进程树，等等…

## 主要命令

| 命令 | 描述 |
| --- | --- |
| `grep` | 在进程内存中搜索给定的字符串或正则表达式 |
| `scan` | 在进程内存中搜索一组预定义的秘密模式 |

## 实用程序命令

| 命令 | 描述 |
| --- | --- |
| `files` | 显示进程正在访问的文件列表 |
| `find` | 给定一个进程名，查找一个 PID。如果多个进程匹配，则返回第一个进程。 |
| `info` | 显示关于进程的信息 |
| `kernel` | 显示关于内核的信息 |
| `kill` | 使用 SIGKILL 终止一个(或多个)进程 |
| `list` | 列出系统中当前可用的所有进程 |
| `resume` | 使用 SIGCONT 恢复挂起的进程 |
| `suspend` | 使用 SIGSTOP 暂停一个进程(使用'肢解恢复'退出暂停) |
| `tree` | 显示流程和所有子流程的树形图(默认为 PID 1)。 |

## 安装

从[最新版本](https://github.com/liamg/dismember/releases/latest)中抓取一个二进制文件，并将其添加到您的路径中。

## 用法举例

### 通过 PID 搜索流程中的模式

```
# search memory owned by process 1234
dismember grep -p 1234 'the password is .*'
```

### 按名称搜索流程中的模式

```
# search memory owned by processes named "nginx" for a login form submission
dismember grep -n nginx 'username=liamg&password=.*'
```

### 搜索所有流程的模式

```
# find a github api token across all processes
dismember grep 'gh[pousr]_[0-9a-zA-Z]{36}'
```

### 在所有进程中搜索内存中的秘密

```
# search all accessible memory for common secrets
dismember scan
```

[Click Here To Download](https://github.com/liamg/dismember)