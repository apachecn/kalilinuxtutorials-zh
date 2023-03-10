# HttpLab:交互式网络服务器

> 原文：<https://kalilinuxtutorials.com/httplab-interactive-web-server/>

HttpLab 是交互式网络服务器。HTTPLabs 允许您检查 HTTP 请求并伪造响应。

![HttpLab](img/9b13d684c667955c6edeff96aac494a5.png)

## **HttpLab 安装**

### **Golang**

```
go get github.com/gchaincl/httplab
go install github.com/gchaincl/httplab/cmd/httplab
```

### **Archlinux**

```
yaourt httplab
```

### **固定我**

在支持快照的[系统](https://snapcraft.io/docs/core/install)上:

```
snap install httplab
```

**也可理解为[Winspy–Windows Reverse Shell 带有自动 IP 平衡程序的后门创建者](https://kalilinuxtutorials.com/winspy-windows-reverse-shell-backdoor/)**

## **帮助**

```
Usage of httplab:
  -a, --auto-update       Auto-updates response when fields change. (default true)
  -b, --body string       Specifies the inital response body. (default "Hello, World")
  -c, --config string     Specifies custom config path.
      --cors              Enable CORS.
      --cors-display      Display CORS requests. (default true)
  -d, --delay int         Specifies the initial response delay in ms.
  -H, --headers strings   Specifies the initial response headers. (default [X-Server:HTTPLab])
  -p, --port int          Specifies the port where HTTPLab will bind to. (default 10080)
  -s, --status string     Specifies the initial response status. (default "200")
  -v, --version           Prints current version.
```

## **按键绑定**

| 钥匙 | 描述 |
| --- | --- |
| `Tab` | 下一次输入 |
| `Shift+Tab` | 先前输入 |
| `Ctrl+a` | 应用响应更改 |
| `Ctrl+r` | 重置请求历史记录 |
| `Ctrl+s` | 将响应另存为 |
| `Ctrl+f` | 将请求另存为 |
| `Ctrl+l` | 切换响应列表 |
| `Ctrl+t` | 切换响应生成器 |
| `Ctrl+o` | 打开正文文件 |
| `Ctrl+b` | 切换身体模式 |
| `Ctrl+h` | 切换帮助 |
| `Ctrl+w` | 切换换行 |
| `q` | 关闭弹出窗口 |
| `PgUp` | 以前的请求 |
| `PgDown` | 下一个请求 |
| `Ctrl+c` | 放弃 |

HTTPLab 使用 file 来存储预先构建的响应，它将在当前目录中查找名为`.httplab`的文件，如果没有找到，它将退回到`$HOME`。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/gchaincl/httplab)