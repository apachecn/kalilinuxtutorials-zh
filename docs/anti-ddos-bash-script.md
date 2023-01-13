# 反 DDOS:防御 DDoS 攻击的反 DDOS Bash 脚本

> 原文：<https://kalilinuxtutorials.com/anti-ddos-bash-script/>

一个通过将 iptables 规则写入 Linux 操作系统来抵御 DOS 和 DDoS 攻击的开源项目被称为 Anti-DDoS 项目。

我们需要确保在实施或执行规则之前采取所有必要的防御配置。反 DDoS 项目将只在 Linux 操作系统上工作，它不会提供 100%的安全性，但它有助于您采取必要的措施。

## **什么是 DDoS 或 DoS 攻击？**

**DDoS** 或分布式拒绝服务(Distributed Denial of Service)是一种 DoS 攻击，其中多个通常感染了特洛伊木马的被入侵系统被用来针对单个系统，从而导致拒绝服务( **DoS** )攻击，换句话说，攻击意在关闭机器或网络，使其目标用户无法访问。 

为了使用这个应用程序，您需要根据您的系统架构设置配置文件。

**也读作[Root stealter——在根终端](https://kalilinuxtutorials.com/rootstealer-inject-root-terminal/)** 上注入命令的诡计

## **运行防 DDoS**

```
root@ismailtasdelen:~# bash ./anti-ddos.sh
```

### 克隆现有存储库(使用 HTTPS 克隆)

```
root@ismailtasdelen:~# git clone https://github.com/ismailtasdelen/Anti-DDOS.git
```

### 克隆现有存储库(使用 SSH 克隆)

```
root@ismailtasdelen:~# git** **clone git@github.com:ismailtasdelen/Anti-DDOS.git
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ismailtasdelen/Anti-DDOS)