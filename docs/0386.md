# IP 混淆器–社交工程和绕过防火墙的简单工具

> 原文：<https://kalilinuxtutorials.com/ip-obfuscator-bypass-firewall/>

IP Obfuscator 是一个简单的 python 脚本，它将 IP 地址转换成不同的模糊形式，如整数、十六进制或八进制形式。

**什么是混淆？**

混淆是攻击者使用的一种技术，用于掩盖合法来源之间的恶意脚本，以绕过检测引擎，这使得分析更加困难。

**举个简单的例子:**
一个普通的 IP 地址“172.217.24.174”可以被混淆为 IPV6 地址“0000:0000:0000:0000:0000:ffff:172 . 217 . 24 . 174”
这种 IPV6 格式很难检查。

**安装:**T2


```
Download the python file:
git clone https://github.com/Sameera-Madhushan/IP-Obfuscator.py

```

```
After downloading the program,  navigate to the Digger directory and list the contents
cd IP-Obfuscator && ls

```

```
You are ready to run the script now!
python3 IP-Obfuscator.py
```

**用法:**

IP 地址> > 192.168.1.1 如何被混淆为不同形式的示例:

![alt img](img/6e23704c9f82f0c472fb36d5859e7af8.png)

另请参阅: [Kube-Hunter:寻找 Kubernetes 集群中的安全弱点](https://kalilinuxtutorials.com/kube-hunter-security-weaknesses/)