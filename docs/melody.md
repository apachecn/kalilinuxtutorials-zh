# Melody:为威胁情报而构建的透明互联网传感器

> 原文：<https://kalilinuxtutorials.com/melody/>

[![](img/a474cad6ddfe22a22688db6c41d894fb.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjJ5Zux5wUPfI9byzdR0OuGtOneJFFeeC9NrMQRfh0A1bMOfSsCLqQJqJLb80Bxa84WciLsTYHoVmH4G7TlwqlIPJim6QL9xUQS6VbS9OdkFWzZ3pONp-tVmDkKFr8OjH4BQHEtMQnUKmDDc_gC4rMeZFCrNFeuStMhOiEF34vZYE73ZdTiOf7DBRda/s728/images.png)

**Melody** 是一款透明的互联网传感器，专为威胁情报而打造，并由检测规则框架提供支持，允许您标记感兴趣的数据包以进行进一步分析和威胁监控。

# 特征

以下是 Melody 的一些主要特征:

*   透明捕获
*   编写检测规则并标记特定数据包，以便对其进行大规模分析
*   使用内置 HTTP/S 服务器模拟易受攻击的网站
*   支持 IPv4 和 IPv6 上的主要互联网协议
*   为你处理日志旋转:Melody 被设计成永远运行在最小的 VPS 上
*   所需的最低配置
*   独立模式:仅使用 CLI 配置 Melody
*   易于扩展:
    *   静态编译二进制
    *   最新的 Docker 图像

# 愿望清单

由于我现在必须专注于其他项目，我不能在 Melody 的开发上投入太多时间。

不过，rom 还有很多需要改进的地方，所以这里有一些我希望有一天能实现的特性:

*   ~~创建、测试和管理规则的专用助手程序~~ - >检查`**cmd/meloctl**`中的 Meloctl
*   集中式规则管理
*   每端口模拟应用程序

# 使用案例

## 面向互联网的传感器

*   从互联网的噪音中提取趋势和模式
*   索引恶意活动、攻击企图和目标扫描器
*   监控新出现的威胁利用
*   关注特定的威胁

## 流分析

*   建立背景噪音档案，突出有针对性的攻击
*   重放捕获以标记可疑流中的恶意数据包

## 快速启动

## TL；速度三角形定位法(dead reckoning)

### 发布

在`**https://github.com/bonjourmalware/melody/releases**`获取最新版本。

**Make install # Set default outfacing interface
Make cap # Set network capabilities to start Melody with elevated privilege
Make certs # Make self signed certs for the HTTPS 文件服务器
Make Enable _ all _ rules # Enable the default rules
Make service #创建一个 systemd 服务以自动重启程序并在启动时启动它
sudo systemctl stop melody #在我们配置它时停止服务**

更新`**filter.bpf**`文件以过滤掉不需要的数据包

**sudo systemctl 开始旋律#开始旋律
sudo systemctl 状态旋律#检查旋律是否正在运行**

日志应该在`**/opt/melody/logs/melody.ndjson**`开始堆积。

**tail-f/opt/melody/logs/melody . nd JSON # | jq**

**来源于**

**git 克隆 https://github.com/bonjourmalware/melody/opt/melody
CD/opt/melody
make build**

然后继续从版本 t1 开始的步骤；博士

### 码头工人

**制作证书#为 HTTPS 文件服务器制作自签名证书
制作 enable_all_rules #启用默认规则
mkdir-p/opt/MELODY/logs
CD/opt/MELODY/
docker pull bonjourmalware/MELODY:latest
MELODY _ CLI = " " #将您的 CLI 选项放在这里。示例:export MELODY _ CLI = "-s-I ' lo '-F ' dst port 5555 '-o ' server . http . port:5555 ' "
docker run \
–net = host \
-e " MELODY _ CLI = $ MELODY _ CLI "
–mount type = bind，source="$(pwd)/filter.bpf "，target=/app/filter.bpf，readonly \
–mount type = bind，source = $(pwd)/config . ym**

## 规则

## 例子

**CVE-2020-14882 Oracle Weblogic Server RCE:
层:http
元:
id:3e1d 86 D8-FBA 6-4e 15-8 c74-941 c 3375 fd3e
版本:1.0
作者:BonjourMalware
状态:稳定
创建时间:2020/11/07
修改时间:2020/20/07
描述 test_handle="
标签:
cve: "cve-2020-14882"
厂商:" oracle"
产品:" weblogic"
影响:" rce"**

## 日志

## 例子

IPv4 上的 Netcat TCP 数据包:

**{
"tcp": {
"窗口":512，
"序列":1906765553，
"ack": 2514263732，
"data_offset": 8，
"flags": "PA "，
"加急":0，
"payload": {
"content ":"我今天有了一个发现。我找到了一台电脑。\n "，
" base64 ":" ssbtywrligegzglzy 292 zxj 5 ihrvzgf 5 lias ssbmb 3 vuzcbhingvbxb 1 dgvylgo = "，
" truncated ":false
}
}，
"ip": {
"version": 4，
"ihl": 5，
"tos": 0，
"length": 99，
"id**

[Download](https://github.com/bonjourmalware/melody)