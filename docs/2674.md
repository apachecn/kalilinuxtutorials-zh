# 跟踪无线设备的接收信号强度

> 原文：<https://kalilinuxtutorials.com/dbmonster/>

[![](img/3d8581c73de9fdcf8e877124615fae9e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgV0WkPTBDtcNlWdMmtXnYx_Pucz_o61RcCAd5lpwFMBe-vvOkIUKzR8vINO-WqywQ2miBELjnMA4O1wjnSYrOROFuu4pCKDEoFNyu9rUUUbKm8epoC2C5CPbi3Vyyuii3adtsDaYcOlf9BcRPiDSSakCB7zIbS2i1Gc1HG6Rf387o2abUOWphEz6gQ/s728/db%20logo%20(1).png)

**dBmonster** 你可以扫描附近的 WiFi 设备，并通过它们发送的数据包的信号强度(dBm)来跟踪它们(用 TShark 嗅探)。这些 dBm 值将用 matplotlib 绘制成图形。它可以帮助您确定附近 WiFi 设备的确切位置(使用定向 WiFi 天线以获得最佳效果)或找出您自制的天线如何工作最佳(天线辐射模式)。

## Linux 和 MacOS 上的特性

| 特征 | Linux 操作系统 | 马科斯 |
| --- | --- | --- |
| 列出 WiFi 接口 | 981 号房 | 981 号房 |
| 2.4GHz 跟踪和扫描 | 981 号房 | 981 号房 |
| 5GHz 上的跟踪和扫描 | 981 号房 | 981 号房 |
| 正在扫描 AP | 981 号房 | 981 号房 |
| 扫描 STA | 981 号房 |  |
| 找到设备时发出哔哔声 | ❓ | 981 号房 |

## 安装

**git 克隆 https://github.com/90N45-d3v/dBmonster
CD db monster
安装所需工具(在没有 sudo 的 MacOS 上)
sudo python requirements . py
启动 db monster
sudo python db monster . py**

## 已在上成功测试

| 平台💻 | WiFi 适配器📡 |
| --- | --- |
| Kali Linux | 阿尔法 AWUS036NHA，DIY Bi-Quad WiFi 天线 |
| 马科斯·蒙特雷 | 内部卡 802.11 a/b/g/n/ac (MBP 2019) |

###### * *应该可以在任何基于 MacOS 或 Debian 的系统上工作，并且支持所有支持监控模式的 WiFi 卡*

[**Download**](https://github.com/90N45-d3v/dBmonster)