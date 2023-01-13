# MongoBuster:搜索打开的 MongoDB 实例

> 原文：<https://kalilinuxtutorials.com/mongobuster/>

MongoBuster 是一个 hunt open mongoDB 实例。以下是与此相关的功能。

*   世界上最快、最高效的扫描仪(使用 Masscan)。
*   默认情况下，扫描整个互联网，所以火的工具和冷却。
*   超高效-使用比线程更轻的围棋程序。

**也可阅读-[用 Cocospy 键盘记录器](https://kalilinuxtutorials.com/monitor-smartphone-usage-with-cocospy-keylogger/)监控智能手机的使用情况**

**先决条件**

*   Go 语言(sudo apt 安装 golang)
*   Masscan(必须安装 masscan)
*   在 Ubuntu 和 Kali linux 上测试

**如何安装和运行**

git 克隆 https://github.com/yashpl/mongoBuster.git
CD mongoBuster
去构建 mongobuster.go utils.go
sudo。/蒙古克星

注意:使用 sudo 运行它，因为 Masscan 需要 sudo 访问。

**标志**

| 旗 | 描述 |
| --- | --- |
| –最大速率=(整数) | 定义数据包生成和发送的最大速率。默认值为 100。 |
| –out-file =(字符串) | 易受攻击的 IP 将导出到的文件的名称。 |
| -v | 显示来自不易受攻击的服务器的错误消息 |

**注**

使用像 10000+这样荒谬的值作为`**max-rate**`标志将*很可能*搞垮你自己的网络基础设施。

对于消费级千兆路由器，推荐值以`**--max-rate 500**`开头。

[Download](https://github.com/yashpl/mongoBuster)