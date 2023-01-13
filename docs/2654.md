# kage:Metasploit meter preter 和会话处理程序的图形用户界面

> 原文：<https://kalilinuxtutorials.com/kage/>

[![](img/2e741e03b8a3abf0867e743e86684670.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiHXRKvU75hJUcasYivln0lRytq2GS3gMAYZxOxZcrnkrIfnlyrcBBdpbtgZiiS7gyiZHL_TqwJ6xOn-IPMJr4srm4uM9OtU6gxS6wouBQNlfhqf0GWpMOZX1OBd7P1jN8YHDkRb6kWSv716Ms_SmJCBH_baEEAPy2bBXwVRjvI6HwYpp-ZUSVEGD-2/s728/kage-logo-svg%20(1).png)

**Kage** (ka-geh)是一个受 AhMyth 启发的工具，为 Metasploit RPC Server 设计，用于与 meterpreter 会话交互并生成有效负载。
目前只支持`**windows/meterpreter**` & **`android/meterpreter`。**

## 开始使用

请按照这些说明获得一个在本地机器上运行的 Kage 副本，没有任何问题。

### 先决条件

*   Metasploit-framework 必须安装在您的`**PATH**`中:
    *   Msfrpcd
    *   Msfvenom
    *   Msfdb

### 安装

您可以从这里安装 Kage 二进制文件。

#### 面向开发者

要从源代码运行应用程序:

**下载源代码
git 克隆 https://github.com/WayzDev/Kage.git
安装依赖项并运行 kage
cd Kage
yarn #或 npm 安装
yarn run dev #或 npm run dev
构建项目
yarn run build**

[**Download**](https://github.com/Zerx0r/Kage)