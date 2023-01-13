# Nginx 日志检查:Nginx 日志安全分析脚本

> 原文：<https://kalilinuxtutorials.com/nginx-log-check/>

[![Nginx Log Check : Nginx Log Security Analysis Script](img/a408ce192f5d4ed9cbb068bc9a705f7c.png "Nginx Log Check : Nginx Log Security Analysis Script")](https://1.bp.blogspot.com/-4zr7-7WogK4/XfdnbAchqYI/AAAAAAAAD-k/_UykUjioZFISGOpiTu5FgOwoOACrLoGEQCLcBGAsYHQ/s1600/Ngnix%25281%2529.png)

Nginx 日志检查是一个 Nginx 日志安全分析脚本。以下是 Nginx 日志安全检查脚本的一些功能；

*   统计前 20 个地址
*   SQL 注入分析
*   扫描仪警报分析
*   漏洞检测
*   敏感路径访问
*   文件包含攻击
*   Webshell
*   查找响应长度前 20 位的 URL
*   寻找罕见的脚本文件访问
*   查找 302 重定向的脚本文件

**也可理解为-[Exploitivator:自动化 Metasploit 扫描和利用](https://kalilinuxtutorials.com/exploitivator-metasploit-scanning-exploitation/)**

**engine log check 用法**

**设置报告保存地址 outfile
设置日志分析目录 access_dir
设置日志名称 access_log**

**。/nginx_check.sh**

[**Download**](https://github.com/al0ne/nginx_log_check)