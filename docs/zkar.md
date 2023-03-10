# Zkar:一个在 Go 中实现 Java 序列化协议分析工具

> 原文：<https://kalilinuxtutorials.com/zkar/>

[![](img/b73ca7bae385be116e5e7d809a7aebd2.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhmuaXwdvC5bcd779Z3-7XqnBqNf-hlPdFhA4oSsAMLpvV9qMWuAF1vISMGdGtiP0cRM0-dPvM-NUhLKxjJxSADud0OkjD3Q1uGVXqgsbUSl0GApLQ8YTSq5JWYVjM250GK8xaaMQdiTRdACFTWe6L7_YLdKfA170ZTgyLJB11g2FrbaF1WVZs1t7hy/s728/JavaSerialization%20(1).png)

ZKar 是一个在 Go 中实现的 Java 序列化协议分析工具。该工具仍在**进行中**，因此没有完整的 API 文档和贡献指南。

ZKar 提供:

*   纯 Go 中的 Java 序列化有效负载解析器和查看器，不需要 CGO 或 JDK
*   从 Java 序列化协议到 Go 结构
*   一个可以操作 Java 序列化数据的 Go 库
*   WIP:在 Go 中实施的 ysoserial
*   WIP: Java 类字节码解析器、查看器和操作
*   WIP:RMI/LDAP 在 Go 中的实现

## 安装

使用 ZKar 很容易。使用`**go get**`安装 ZKar 以及库和它的依赖项:

**去 github.com/phith0n/zkar 吧**

接下来，在您的应用程序中使用 **`github.com/phith0n/zkar/*`** :

**包主
导入(
【fmt】
【github . com/phi th0n/zkar/serz】
【io/iou til】
【log】
)
func main(){
数据，_ := ioutil。ReadFile("。/test cases/yso serial/commons collections 6 . ser ")
序列化，err := serz。FromBytes(data)
if err！= nil {
log。致命("解析错误")
}
fmt。Println(连载。ToString())
}**

## 命令行实用工具

ZKar 还提供了一个可以直接使用的命令行实用工具:

**$ go run main . go
NAME:
zkar–一个 Java serz 工具
用法:
main【全局选项】command【命令选项】【参数…】
COMMANDS:
generate 生成 Java serz 攻击有效载荷
dump 解析 Java serz 流并转储 struct
help，h 显示命令列表或一个命令的帮助
全局选项:
–help，-h 显示帮助(默认:false)**

例如，您可以从 ysoserial 转储有效负载 CommonsBeanutils3，如下所示:

**$ go run main . go dump-f " $(pwd)/test cases/yso serial/commonsbeautils 3 . ser "**

## 试验

ZKar 是一个经过充分测试的工具，它通过了所有 ysoserial 生成的小工具解析和重建测试。这意味着由 ysoserial 生成的 gadget 可以被 ZKar 解析，并且解析后的 struts 可以被转换回与原字符串相等的 bytes 字符串。

| 小玩意 | 包裹 | 从语法上分析 | 重建 | 消遣时间 |
| --- | --- | --- | --- | --- |
| AspectJWeaver | ysoserial | 981 号房 | 981 号房 | 80.334 s |
| 豆壳 1 | ysoserial | 981 号房 | 981 号房 | 782.613 南纬 |
| C3P0 | ysoserial | 981 号房 | 981 号房 | 98.321 南纬 |
| 点击 1 | ysoserial | 981 号房 | 981 号房 | 573.298 南纬 |
| Clojure | ysoserial | 981 号房 | 981 号房 | 72.415 南纬 |
| 普通手册 1 | ysoserial | 981 号房 | 981 号房 | 461.15 南纬 |
| 常见收藏 1 | ysoserial | 981 号房 | 981 号房 | 64.484 s |
| 常见收藏 2 | ysoserial | 981 号房 | 981 号房 | 508.918 南 |
| 常见收藏 3 | ysoserial | 981 号房 | 981 号房 | 564.071 南 |
| 常见收藏 4 | ysoserial | 981 号房 | 981 号房 | 535.449 南纬 |
| 常见收藏 5 | ysoserial | 981 号房 | 981 号房 | 137.609 南纬 |
| 常见收藏 6 | ysoserial | 981 号房 | 981 号房 | 68.753 南纬 |
| 常见收藏 7 | ysoserial | 981 号房 | 981 号房 | 178.549 南纬 |
| FileUpload1(文件上载 1) | ysoserial | 981 号房 | 981 号房 | 35.39 秒 |
| Groovy1 | ysoserial | 981 号房 | 981 号房 | 150.991 南纬 |
| 休眠 1 | ysoserial | 981 号房 | 981 号房 | 789.674 南 |
| 冬眠 2 | ysoserial | 981 号房 | 981 号房 | 168.624 南纬 |
| JBossInterceptors1 | ysoserial | 981 号房 | 981 号房 | 632.581 南 |
| JRMPClient | ysoserial | 981 号房 | 981 号房 | 32.967 南纬 |
| JRMPListener | ysoserial | 981 号房 | 981 号房 | 38.263 南纬 |
| JSON1 | ysoserial | 981 号房 | 981 号房 | 2.157225 毫秒 |
| javassistsweld 1 | ysoserial | 981 号房 | 981 号房 | 468.596 南 |
| Jdk7u21 | ysoserial | 981 号房 | 981 号房 | 355.01 南纬 |
| Jython1 | ysoserial | 981 号房 | 981 号房 | 216.862 南纬 |
| MozillaRhino1 | ysoserial | 981 号房 | 981 号房 | 1.775193 毫秒 |
| MozillaRhino2 | ysoserial | 981 号房 | 981 号房 | 409.124 s |
| 我的面孔 1 | ysoserial | 981 号房 | 981 号房 | 22.997 先令 |
| Myfaces2 | ysoserial | 981 号房 | 981 号房 | 38.131 s |
| 罗马 | ysoserial | 981 号房 | 981 号房 | 485.804 南 |
| 春天 1 | ysoserial | 981 号房 | 981 号房 | 797.469 南纬 |
| 春天 2 | ysoserial | 981 号房 | 981 号房 | 358.041 南纬 |
| 厄伦斯 | ysoserial | 981 号房 | 981 号房 | 21.502 s |
| 要求 1 | ysoserial | 981 号房 | 981 号房 | 438.729 南纬 |
| wicked1 | ysoserial | 981 号房 | 981 号房 | 23.509 南 |
| JDK8u20* | 品特斯特 | 981 号房 | 981 号房 | 529.3 南纬 |

注意:为了解析 JDK8u20 有效载荷，您应该在`**dump**`命令中添加`**--jdk8u20**`标志。因为有效负载不是有效的序列化数据流，所以有必要通过这个标志告诉 ZKar patches 数据。

[**Download**](https://github.com/phith0n/zkar)