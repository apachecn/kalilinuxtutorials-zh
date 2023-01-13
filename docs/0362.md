# az tarna——机器人的足迹工具

> 原文：<https://kalilinuxtutorials.com/aztarna-footprinting-robots/>

这个库包含 Alias Robotic 的 aztarna，这是一个机器人足迹工具。

Alias Robotics 支持原始机器人制造商评估其安全性并提高其软件质量。

我们绝不鼓励或促进对运行中的机器人系统进行未经授权的篡改。这会造成严重的人身伤害和物质损失。

**又读:**[Tcpreplay–Pcap 编辑【UNIX 的重播工具& Windows 的](https://kalilinuxtutorials.com/tcpreplay-unix-windows/)

### **对于 ro**

*   系统中存在的 ROS 节点列表(发布者和订阅者)
*   对于每个节点，发布和订阅的主题包括主题类型
*   对于每个节点，每个节点提供的 ROS 服务
*   参数服务器中所有 ROS 参数的列表
*   系统中正在运行的活动通信的列表。单个通信包括涉及的发布者/订阅者节点和主题

### **对于 SROS**

*   确定系统是否是 SROS 主系统。
*   检测演示配置是否正在使用。
*   系统中找到的节点列表。(扩展模式)
*   每个节点的允许/拒绝策略列表。
    *   可发表的话题。
    *   可预订的主题。
    *   可执行服务。
    *   可读参数。

### **用于工业路由器**

*   检测 eWON、Moxa、Sierra Wireless 和 Westermo 工业路由器。
*   对找到的路由器进行默认凭据检查。

## **azar 的安装**

#### **用于生产**

直接来自 pypi

**pip3 安装偶合器**

或者从存储库中:

**pip3 安装。**

为了发展

**pip3 install -e .
或
python3 setup.py develop**

Python 3.7 和 setuptools 包是安装所必需的

#### **用对接器安装**

**docker build -t aztarna_docker。**

#### **代码用法:**

**用法:az tarna[-h]-t TYPE[-a ADDRESS][-p PORTS][-I INPUT _ FILE]
[-o OUT _ FILE][-e][-r RATE][–shod an][–API-KEY API _ KEY]
az tarn
可选参数:
-h，–help 显示此帮助消息并退出
-t TYPE，–TYPE 扫描 ROS、SROS
主机或工业路由器
-a ADDRESS，–ADDRESS ADDRESS
Single
-p 端口，–端口端口
要扫描的端口(格式:13311 或 11111-11155 或
1，2，3，4)
-i 输入文件，–输入文件输入文件
用于扫描的地址的输入文件
-o 输出文件，–输出文件输出文件
结果的输出文件
-e，–主机的扩展扩展扫描
-r
–API-KEY API _ KEY shod an API KEY**

#### **运行代码(示例输入文件):**

**azar-t ROS-p 11311 和 ros_scan_s20.csv**

#### **用 Docker 运行代码(示例输入文件):**

**对接器运行-v:/root-it aztar na _ docker-t ROS-p 11311-I**

#### **运行代码(示例单个 ip 地址):**

【t0-t 玫瑰-p 11311 -a 115.129.241.241

#### **运行代码(示例子网):**

【t0-t 玫瑰-p 11311 -a 115.129.241.0/24】

#### **运行代码(示例单个 ip 地址、端口范围):**

**阿兹海默症-p 11311-11500 -a 115.129.241】**

#### **运行代码(示例单个 ip 地址、端口列表):**

【t0-t 玫瑰-p 11311.11312.11313-a 115.129.241】

#### **运行代码(示例管道直接来自 zmap):**

**转储-p 11311 0.0.0/0-q \ n 转储-p 11311**

#### **运行代码(shodan 工业路由器示例搜索)**

**az tarna-t IROUTERS–shod an–API-key**

#### **运行代码(示例搜索 shodan 的工业路由器，管道到文件)**

**az tarna-t IROUTERS–shod an–API-key-o routers . CSV**

[**Download**](https://github.com/aliasrobotics/aztarna#for-production)