# 破伤风:神话 C2 代理针对 Linux 和 Windows 主机写在 Rust

> 原文：<https://kalilinuxtutorials.com/tetanus/>

[![](img/108c307fd6619d7563db98be5a167e28.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYcyKeGijKexmOCqs-IlGtTw8qbvvRteXQIPVfE_zyvRxNpWn2Nk9s4RnAoqh8PACGPpQMC8E-DEohiYliFm1UWN6nvUnLoGIUWrWoZr8eyFdsZr2mwjV1Y-CZ9H9Yytty8UUEpJYObEvR66oAGip18GXKRvHkRMqqMGOrYT1S7BH0GEChmLN-OldY/s728/tetanus-svg.png)

**破伤风**是一个用 rust 编写的 Windows 和 Linux C2 代理。

# 安装

要安装破伤风，你需要在机器上安装 Mythic。

在 Mythic 根目录中，使用`**mythic-cli**`安装代理。

**须藤。/mythic-cli 安装 github https://github.com/MythicAgents/tetanus
sudo。/mythic-cli 有效载荷启动破伤风**

破伤风支持 http C2 配置文件:

**须藤。/mythic-cli 安装 github https://github.com/MythicC2Profiles/http
sudo。/mythic-cli c2 start http**

## 特征

*   后台作业管理
*   内置 ssh 客户端
    *   连接到一台机器，在那台机器和 Mythic 之间下载/上传文件
    *   使用 sftp 从机器获取目录列表
    *   使用 ssh 在机器上生成代理
    *   ssh-代理劫持
*   流式端口扫描
*   站立 TCP 重定向器

## 未来新增内容

*   v0.2.0
    *   袜子代理
    *   Windows 令牌操作
    *   更多浏览器脚本集成
    *   DNS C2 配置文件
    *   p2p 功能
    *   在内存中执行外壳代码`**execute-shellcode**`

## 通用命令

| 命令 | 句法 | 描述 |
| --- | --- | --- |
| 猫 | `**cat [file]**` | 输出文件的内容。 |
| 激光唱片 | `**cd [new directory]**` | 更改目录。 |
| 丙酸纤维素 | `**cp [source] [destination]**` | 将文件从[源]复制到[目的]。 |
| 下载 | `**download [path]**` | 从目标系统下载文件(支持相对路径)。 |
| 出口 | `**exit**` | 退出代理。 |
| getenv | `**getenv**` | 获取当前环境变量。 |
| getprivs | `**getprivs**` | 获取代理会话的权限。 |
| jobkill | `**jobkill [job id]**` | 关闭正在运行的后台作业。 |
| 工作 | `**jobs**` | 列出当前正在运行的后台作业。 |
| 限位开关（Limit Switch） | `**ls [directory]**` | 列出文件或目录(支持相对路径)。 |
| mkdir | `**mkdir [directory]**` | 创建一个新目录。 |
| 平均变化 | `**mv [source] [destination]**` | 将文件从[源]移动到[目的](支持相对路径)。 |
| 端口扫描 | `**portscan [popup]**` | 扫描 IP 列表中打开的端口。 |
| 著名图象处理软件 | `**ps**` | 获取当前正在运行的进程列表。 |
| 显示当前工作目录 | `**pwd**` | 打印工作目录。 |
| 再直接的 | `**redirect [<bindhost>:<bindport>:<connecthost>:<connectport>]**` | 在远程系统上设置 TCP 重定向器。 |
| 空间 | `**rm [path]**` | 删除文件或目录(支持相对路径)。 |
| setenv | `**setenv [name] [value]**` | 将环境变量[名称]设置为[值]。 |
| 壳 | `**shell [command]**` | 在一个新线程中使用 Linux 上的`**bash -c**`或 Windows 上的`**cmd.exe /c**`运行一个 shell 命令。 |
| 睡眠 | `**sleep [interval][units] [jitter]**` | 设置睡眠间隔和抖动(支持单位后缀)。 |
| 嘘 | `**ssh [popup]**` | 使用 ssh 来执行命令、下载/上传文件或获取目录列表。 |
| ssh 代理 | `**ssh-agent [-c <socket>] [-d] [-l]**` | 连接到主机上正在运行的 ssh 代理套接字或列出身份。 |
| ssh-spawn | `**ssh-spawn [popup]**` | 使用 ssh 在远程主机上生成一个神话代理。 |
| unsetenv | `**unsetenv [var]**` | 取消设置环境变量。 |
| 上传 | `**upload [popup]**` | 将文件上传到主机。 |

### Windows 特有的命令

| 命令 | 句法 | 描述 |
| --- | --- | --- |
| powershell | `**powershell [command]**` | 在新线程中使用`**powershell.exe /c**`运行命令。 |

[**Download**](https://github.com/MythicAgents/tetanus#future-additions)