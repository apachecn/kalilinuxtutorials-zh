# Geowifi:在不同的公共数据库上通过 BSSID 和 SSID 搜索 wifi 地理位置数据

> 原文：<https://kalilinuxtutorials.com/geowifi/>

[![](img/3488b7ed5eabe618ef4d663995a4babf.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg0j8uW66TW1SzkJaxhCr0eHEvksYUFXnl0Dim36hZ9BV1k4ru8BZGineAiqbGa7Z28i8mT63iodNpNSJFQdEDQYd3zFnjSlVkJfqlPHcDuvxO1YRBq5gr6pVpNNx0XgVfURdgxF3RMDgHiKL1NjDOXpj6Y56sPLP_VPfcq9cFIB1gVfVa2-2kHEn7j/s728/FLLtmsPWQAswtMH.png)

**Geowifi** 是在不同的公共数据库上通过 BSSID 和 SSID 搜索 wifi 地理位置数据的工具。

**数据库**

*   扭动
*   苹果
*   OpenWifi
*   米尔尼科夫

## 先决条件

*   Python3。
*   为了在**窗口**上显示表情符号，建议安装新的 Windows 终端。
*   为了使用 Wigle 服务，有必要获取一个 API 并配置`**utils/API.yaml**`文件，以替换为使用 wigle 提供的数据而编码的"**的" **wigle_auth** "参数值。**这是通过 SSID** 进行搜索所必需的。**

## 装置

使用软件包管理器 pip 来安装需求。

**python3 -m pip 安装要求. txt**

**用途**

**用法:geo wifi . py[-h](-s SSID |-b BSSID)[-j][-m]
可选参数:
-h，–help 显示此帮助信息并退出
-s SSID，–SSID SSID 按 SSID 搜索
-b BSSID，–BSSID 按 BSSID 搜索 BSSID
-j，–Json Json 输出
-m，–Map 输出**

按 BSSID 搜索:

**python3 geowifi.py -b BSSID**

按 SSID 搜索:

**python3 geowifi.py -s SSID**

可以使用`**-j**`参数导出 json 格式的结果，并使用 **`-m`在 html 地图上显示位置。**

**Json 输出示例**

**{
" data ":{
" bssid ":" A0:XX:XX:XX:6F:90 ",
" vendor ":" TP-LINK TECHNOLOGIES co .，ltd ",
" MAC _ type ":" MA-L "，
" wig le ":{
" lat ":00.000908922099，
" lon ":00.00094522028
}。**

[**Download**](https://github.com/GONZOsint/geowifi)