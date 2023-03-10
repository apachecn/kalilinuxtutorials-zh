# Bluewall:为攻防网络专业人士设计的防火墙框架

> 原文：<https://kalilinuxtutorials.com/bluewall/>

[![Bluewall : Firewall Framework Designed For Offensive & Defensive Cyber Professionals](img/7f593a31991650b39e5560c7ec2a5b7f.png "Bluewall : Firewall Framework Designed For Offensive & Defensive Cyber Professionals")](https://1.bp.blogspot.com/-3Ss9MxGXgTk/XidJaQJZaMI/AAAAAAAAEgo/glcciHCW1aAUET2Zd4NblBEd-5k8N5gnACLcBGAsYHQ/s1600/Bluewall%25281%2529.png)

**Bluewall** 是一款专为攻击性和防御性网络专业人士设计的防火墙框架。该框架允许网络安全专业人员快速设置他们的环境，同时保持在他们的范围内。

**特性**

*配置防火墙
*配置主机名
*配置接口

**也读作-[lol BITS:C #反向 Shell 使用 BITS 作为通信协议](https://kalilinuxtutorials.com/lolbits-reverse-shell-using-bits-communication-protocol/)**

**支持的操作系统**

*** Redhat/CentOS
*可以生成但不能执行 Windows 配置。**

**命令行**

* blue wall-c config/example . ini
* *参见配置示例

**Utils**

*列举–识别网络中的活动主机(即将推出)

**征兆**

***目标主机–出站通信
*可信主机–双向通信
*无攻击–您的计算机不应与之通信的设备**

**设置**

# **专为 PYTHON 2 . x**
sudo PYTHON setup . py install
sudo blue wall-h(求助)

**入门**

**#设置初始环境使用配置**
sudo blue wall-c config/host config . ini

**#导出可选 windows 配置**
sudo blue wall-c config/host config . ini-w auto config . PS1

**#添加额外的入站主机或范围**
sudo blue wall-ih 192 . 168 . 0 . 3、192.168.1.0/24

[**Download**](https://github.com/austin-taylor/bluewall)