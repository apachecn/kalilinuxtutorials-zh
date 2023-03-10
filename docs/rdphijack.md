# RDPHijack:使用 WinStationConnect API 执行本地/远程 RDP 会话劫持

> 原文：<https://kalilinuxtutorials.com/rdphijack/>

[![](img/a8938e7b34325e619965baa15aa7bada.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJASPPHdANx8wLCEKHspTEBzxogyu8ia_Ofgcw0VkBFwU13AnnAUUVuXsRrmdzoowweEKaCu_tHAlRzHOpUDTEud-gtjkjtyKh-BjEWmjxDFEiwMCD4Ckk9P_gqY8x-1YQGO8_DRsuUVRFB-p-mJ2zhOt_gRGqP5bnd5xMn-S5T24p8QKPkNSefsvK/s728/q-C6XWFRNYwgwOlX5fNdDCth17Aejn9j5qBZZZ6-RII%20(3).png)

使用 WinStationConnect API 执行本地/远程 RDP 会话劫持的 Cobalt Strike Beacon 对象文件(BOF)。使用会话所有者的有效访问令牌/ kerberos 票证(例如黄金票证)，您将能够远程劫持会话，而不会在目标服务器上丢弃任何信标/工具。

要本地/远程枚举会话，您可以使用 Quser-BOF。

## 使用

**用法:BOF-rdphijack[您的控制台会话 id][要劫持的目标会话 id][密码|服务器][参数]
命令描述
密码指定拥有您要连接的会话的用户的密码。
server 指定您想要执行 RDP 劫持的远程服务器。
示例用法
将会话 2 重定向到会话 1(需要系统权限):
bof-rdphijack 1 2
使用拥有会话 2 的用户的密码将会话 2 重定向到会话 1(需要高完整性信标):
bof-rdphijack 1 2 密码 P@ssw0rd123
为远程服务器将会话 2 重定向到会话 1(需要拥有会话 2 的用户的令牌/票证):
bof-rdphijack 1 2 服务器 SQL01.lab.internal**

[**Download**](https://github.com/netero1010/RDPHijack-BOF)