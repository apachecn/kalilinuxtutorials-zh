# knock——用于枚举子域的工具

> 原文：<https://kalilinuxtutorials.com/knock-enumerate-subdomains/>

**Knock** 是一个 python 工具，旨在通过单词表枚举目标域上的子域。

它被设计为扫描 **DNS 区域转移**，并尝试在启用的情况下自动绕过**通配符 DNS 记录**。

现在 knockpy 支持对 VirusTotal 子域的查询，您可以在 config.json 文件中设置 API_KEY。

**$淘气的 domain.com**

如果您想保存完整的日志[，就像这个](http://pastebin.com/d9nMiyP4)一样，只需键入:

**$诺克皮·domain.com–JSON**

**也可理解为:** [DjangoHunter:识别配置不正确的 Django 应用程序的工具](https://kalilinuxtutorials.com/djangohunter-django-applications/)

### **敲击安装**

*   Dnspython

**$ sudo apt-get 安装 python-dnspython**

*   安装

**$ git 克隆 https://github.com/guelfoweb/knock.git
$ CD 敲
$ nano knockpy/config . JSON<-设置你的 virus total API _ KEY
$ sudo python setup . py 安装**

**注:**建议使用谷歌 DNS:8.8.8.8 和 8.8.4.4

*   **令人震惊的争论**

$ knockpy -h
用法:knockpy[-h][-v][-w WORDLIST][-r][-c][-j]域
敲子域扫描
knockpy v.4.1
作者:Gianni ' guelfoweb ' Amato
Github:https://github.com/guelfoweb/knock
**位置参数:**
要扫描的域目标，如 domain.com
**可选参数:**
-h，–help 显示此帮助消息并退出 –resolve 解析 ip 或域名
-c、–csv 将输出保存在 csv
-f、–CSV fields 将字段名称添加到 CSV 输出文件的第一行
-j、–JSON 导出 JSON
**中的完整报告示例:**
knockpy domain.com
knockpy domain.com-w word list . txt
knockpy-r domain.com 或 IP
knockpy-c domain.com

**注意:**对于 virustotal 子域支持，您可以在 config.json 文件中设置 API_KEY。

[Download](https://github.com/guelfoweb/knock)

**鸣谢:** [**吉安尼‘古尔福韦布’阿马托**](http://guelfoweb.com/)