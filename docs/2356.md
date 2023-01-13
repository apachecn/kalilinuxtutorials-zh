# Dontgo403:绕过 40X 响应代码的工具

> 原文：<https://kalilinuxtutorials.com/dontgo403/>

[![](img/f785e8ee7e81cbb450e575dfa26b9876.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjkftgIV9WfiGb_gR4NJG7MQZxnmdsesbPMD7CupwosvzI16zp4BAxQxxxQwSWwtC_sSkgocBB_pEbO-GHzUkDEovfPa3dAL_DGBlkGe_ThcE8JXCAfn20RhP2_MxsyCgyOi5rNmp56xNLtjbj1zrvlK9gEWqRgPUfwXQpAycdXxvOD9fuDSiVmyARE=s1623)

**Dontgo403** 是一个绕过 40X 误差的工具。

## 装置

**git 克隆 https://github.com/devploit/dontgo403; CD dontgo 403；去拿；去建造**

# 用户化

如果您想要编辑或添加新的旁路，您可以直接将其添加到有效负载文件夹中的特定文件，该工具将使用它。

# 选项

**。/dontgo403 -h
命令行应用程序，自动执行不同的方法来绕过 40X 代码。
用法:
dontgo 403【Flags】
Flags:
-b，–bypassIp string 用特定的 Ip 地址(或主机名)尝试旁路测试。即:' X-Forwarded-For: 192.168.0.1 '而不是' X-Forwarded-For:127 . 0 . 0 . 1 '
-H，–header string 向请求添加自定义头(可以多次指定)
-h，–help 帮助 dontgo403
-p，–Proxy string 代理 URL。例如:http://127.0.0.1:8080
-u，–uri 字符串目标 URL
-a，–User Agent 字符串设置用户代理字符串(默认为‘dontgo 403/0.3【T11’)**

[**Download**](https://github.com/devploit/dontgo403)