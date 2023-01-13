# PyShell:多平台 Python WebShell

> 原文：<https://kalilinuxtutorials.com/pyshell/>

[![](img/6d9eafaeee227d2c256ec70cb333b246.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmDMZf4hRiZGa-gSAnzfb5yxaGfkZpljCgGGCItBztheqINHxx85OgZxPN2UdZdPQnU_yFLvmPrPwR0XJiBVmrC_KRsohZvd0bVsjuwSqtxGWohUM4OXl-rgF3gsUSJzL69c80lJAy1QBzUU3gTLqXi2__cMfJTJ4nKryoE3Dl_rrQvpjHhj9Hsnm1/s728/PyShell%20logo%20(1).png)

PyShell 是多平台 Python WebShell。这个工具帮助您在 web 服务器上获得一个类似外壳的接口，以便进行远程访问。与其他 webshells 不同，该工具的主要目标是在服务器端使用尽可能少的代码，而不考虑使用的语言或服务器的操作系统。

得益于此，您可以在 Windows 和 Linux 中使用不同类型的 shell(aspx、php、jsp、sh、py……)，包括命令历史、上传和下载文件，甚至可以像使用标准 shell 一样在目录间移动。

# 要求

*   python3
*   安装要求. txt

# 下载

建议克隆完整的存储库或下载 zip 文件。您可以通过运行以下命令来实现这一点:

**git 克隆 https://github.com/JoelGMSec/PyShell**

**用途**

**。/py shell . py-h
██████▓██░██████████░██▓███████▓██▓
▓██░██▒██░██▒██▒▓████▒▓██▓██▒▓██▒
▓██░██▒████░░▓███▒██████░▒████▒██░▒██░
▒██████▒░████▓░▒██▒░██░██▒██▒██░▒██░
▒██▒░░░██▒▓░▒██████▒▒░██▒░██▓░█████▒░██████▒░██████▒
▒██░░░██▒▒▒▒▒▓▒▒░▒░░▒░▒░░▒░░░▒░▓░░▒░▓░
░▒░▓██░▒░░░▒░▒░░░░░░░░▒░░ ░▒░
░░░▒▒░░░░░░░░░░░░░
░░░░░░░
————by @ joelmsec&@ 3v4sion———
用法:py shell . py[-h][-a auth][-c cookies][-p param][-pi][-su][-PS]URL 方法
位置参数:
url Webshell URL
方法 HTTP 方法执行命令(GET 或 POST)
可选参数:
–在每个请求上使用的 auth AUTH 授权头
-c COOKIES，–COOKIES COOKIES
在每个请求上使用的 Cookie 头
-p PARAM，–PARAM PARAM
参数用于自定义 WebShell
-pi，–Pipe Pipe 参数后的所有命令
-su，–Sudo Sudo 命令执行(仅在 Linux 主机上)
-ps，–PowerShell PowerShell 命令执行(仅在 Windows 主机上)**

[**Download**](https://github.com/JoelGMSec/PyShellhttps://github.com/JoelGMSec/PyShell)