# WSS at–Web 服务安全评估工具

> 原文：<https://kalilinuxtutorials.com/wssat/>

WSSAT 是一个开源的 web 服务安全扫描工具，它提供了一个动态环境，只需编辑配置文件就可以添加、更新或删除漏洞。该工具接受 WSDL 地址列表作为输入文件，并针对每个服务的安全漏洞执行静态和动态测试。它还制定了信息披露控制措施。有了这个工具，所有的网络服务都可以立刻被分析，组织可以看到整体的安全评估。

**WSS at 的目标**

1.  立即执行他们的 web 服务安全分析
2.  查看带报告的总体安全评估
3.  强化他们的 web 服务

**也读 [日志杀手:清除你在 Linux & Windows 服务器](https://kalilinuxtutorials.com/log-killer-linux-windows-servers/)中的所有日志**

## **WSSAT 安装**

### **开发环境**

```
C# 
Microsoft Visual Studio Community Edition 2017 (https://www.visualstudio.com/downloads/)
```

### **要求**

```
Windows OS (7 or later)
.Net Framework 4.7 (https://www.microsoft.com/en-us/download/details.aspx?id=55170)
```

### **安装**

```
**Step 1: Download the WSSAT folder and copy/extract it to your Windows computer**
**Step 2: Go to WSSAT WSSAT\WSSAT\bin\Debug folder (Read/Write permission is required to generate report, log etc.)**
**Step 3: Double click WSSAT.exe**
```

## **WSSAT 的主要功能包括**

### **动态测试:**

1.  不安全的通信–不使用 SSL
2.  未经认证的服务方法
3.  基于错误的 SQL 注入
4.  跨站点脚本
5.  XML 炸弹
6.  外部实体攻击–XXE
7.  XPATH 注入
8.  HTTP 选项方法
9.  跨站点跟踪(XST)
10.  缺少 X-XSS 保护标头
11.  详细的 SOAP 错误消息

### **静态分析:**

1.  弱 XML 模式:无限出现
2.  弱 XML 架构:未定义的名称空间
3.  弱 WS-SecurityPolicy:不安全的传输
4.  弱 WS-SecurityPolicy:支持令牌保护不足
5.  弱 WS-SecurityPolicy:令牌不受保护

### **信息泄露:**

1.  服务器或技术信息泄露

## **WSSAT 的主要模块**

1.  句法分析程序
2.  漏洞加载程序
3.  分析器/攻击者
4.  记录器
5.  报告程序编制器

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/YalcinYolalan/WSSAT)