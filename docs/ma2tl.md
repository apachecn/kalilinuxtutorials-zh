# Ma2Tl:使用 Mac_Apt 的分析结果 DBs 的 macOS 取证时间轴生成器

> 原文：<https://kalilinuxtutorials.com/ma2tl/>

[![](img/58a5eba6d7a59f309758bb60f99c8c82.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgR4oWpNpLzJRWbgjvwfx0Doy9Ql5Db-VtWGBSODMAmtyTkIxoZMgMmvzLcAFrPToiPU7fFBnociertohWu4nEAYgtgyPHnEeihSQCA4v4hwtJ4i8s6Fy5WFhbSWwCMpFF_opIRNbPnw12LWM6-z8ittj-QLUXokIVC-PWmv7SOYHfVwbLd5VKqirsX/s728/ma2tl_1_demo_scenario-709267%20(1).png)

**Ma2Tl** 是一个 DFIR 工具，用于从 mac_apt 的分析结果 DBs 生成 macOS 取证时间轴。

## 要求

*   Python 3.7.0 或更高版本
*   pytz
*   tzlocal
*   xls xwritter

## 安装

**% git 克隆 https://github . com/mnrkbys/ma 2tl . git**

## 使用

**% python。/ma2tl.py -h
用法:ma2tl . py[-h][-I INPUT][-o OUTPUT][-o OUTPUT _ TYPE][-s START][-e END][-t time zone][-l LOG _ LEVEL]plugin[plugin…]
使用 mac_apt 分析结果的取证时间轴生成器。仅支持 SQLite 数据库。
位置参数:
要运行的插件插件(空格分隔)。
可选参数:
-h，–help 显示此帮助消息并退出
-i INPUT，–INPUT INPUT
包含 mac_apt DBs 的文件夹路径。
-o OUTPUT，–OUTPUT 输出
保存 ma2tl 结果的文件夹路径。
-ot OUTPUT_TYPE，–OUTPUT _ TYPE OUTPUT _ TYPE
指定输出文件类型:SQLITE，XLSX，TSV(默认:SQLITE)
-s START，–START START
指定开始时间戳。(例如。2021-11-05 08:30:00)
-e END，–END END 指定结束时间戳。
-t 时区，–time zone 时区
指定时区:“UTC”、“亚洲/东京”、“美国/东部”等(默认:系统本地时区)
-l LOG_LEVEL，–LOG _ LEVEL LOG _ LEVEL
指定日志级别:INFO、DEBUG、WARNING、ERROR、CRITICAL(默认:INFO)
以下 4 个插件可用:
FILE_DOWNLOAD 提取文件下载活动。
暂留提取暂留设置。
PROG_EXEC 提取程序执行活动。
VOLUME_MOUNT 提取卷装载/卸载活动。
————————————————————————
全部运行所有插件**

## 生成的时间线示例

![](img/a2089e2dcc422e279fa223982c238d19.png)[**Download**](https://github.com/mnrkbys/ma2tl)