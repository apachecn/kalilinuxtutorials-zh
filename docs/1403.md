# 先行者:快速和可扩展的网络扫描库

> 原文：<https://kalilinuxtutorials.com/forerunner/>

[![Forerunner : Fast & Extensible Network Scanning Library](img/2d94aaf19555105e57084d76f7980c72.png "Forerunner : Fast & Extensible Network Scanning Library")](https://1.bp.blogspot.com/-V4NvZiL91nI/XuBSjBPoEmI/AAAAAAAAGkM/JQlbx86R89o1H0x8nLquznSEFSEHEaJ-QCLcBGAsYHQ/s1600/Forerunner-svg.png)

**Forerunner 库**是一个快速、轻量级、可扩展的网络库，旨在帮助开发健壮的以网络为中心的应用程序，如:IP 扫描器、端口敲门程序、客户端、服务器等。

在其当前状态下，Forerunner 库能够同步和异步扫描和端口敲门 IP 地址，以便获得关于位于该端点的设备的信息，例如:IP 是否在线、物理 MAC 地址等。

该库是一个完全面向对象和基于事件的库，这意味着扫描数据包含在特制的“扫描”对象中，这些对象旨在处理从结果到异常的所有数据。

**要求**

*   。NET 框架 4.6.1

**也可阅读-[极简攻击性安全工具](https://kalilinuxtutorials.com/minimalistic/)**

**特性**

| 方法 | 描述 | 使用 |
| --- | --- | --- |
| 扫描 | 扫描单个 IP 以获取信息 | `Scan("192.168.1.1");` |
| 扫描范围 | 扫描一系列 IP 以获取信息 | `ScanRange("192.168.1.1", "192.168.1.255")` |
| 扫描列表 | 扫描 IP 列表以获取信息 | `ScanList("192.168.1.1, 192.168.1.2, 192.168.1.3")` |
| 敲门 | Ping 单个 IP 的每个端口 | `PortKnock("192.168.1.1");` |
| PortKnockRange | Ping 一系列 IP 中的每个端口 | `PortKnockRange("192.168.1.1", "192.168.1.255");` |
| PortKnockList | 使用 IP 列表 Ping 每个端口 | `PortKnockList("192.198.1.1, 192.168.1.2, 192.168.1.3");` |
| IsHostAlive | 在 X 毫秒内 Ping 主机 N 次 | `IsHostAlive("192.168.1.1", 5, 1000);` |
| GetAveragePingResponse | 获取主机的平均 ping 响应 | `GetAveragePingResponse("192.168.1.1", 5, 1000);` |
| IsPortOpen | 通过 TCP 和 Ping 单个端口 | `IsPortOpen("192.168.1.1", 45000, new TimeSpan(1000), false);` |

**例题**

**IP 扫描**

在这个数字时代，扫描网络是一项普通的任务，所以我冒昧地让这项工作尽可能简单，以方便未来的程序员。Forerunner 库是完全面向对象的，因此非常适合即插即用的情况；IP 扫描的对象称为 *IPScanObject* ，它实际上包含相当多的属性:

*   地址( ***字符串*** )
*   IP(***IP 地址*** )
*   平( ***长*** )
*   主机名( ***字符串***
*   MAC ( ***字符串*** )
*   isOnline ( ***Bool*** )
*   错误( ***异常*** )

记住这个对象，让我们试着创建一个新对象，并使用它执行扫描。有多种方法可以做到这一点，然而，最简单的开始方法是首先创建一个新的 *Scanner* 对象，这样我们就可以访问我们的扫描方法。接下来，创建一个 *IPScanObject* ，然后用您想要枚举的 IP 将其设置为 *Scan* 方法；例如:

*   **同步**

```
using System;
using Forerunner; // Remember to import our library.

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Our IP we would like to scan.
            string ip = "192.168.1.1";

            // Create a new scanner object.
            Scanner s = new Scanner();

            // Create a new scan object and perform a scan.
            IPScanObject result = s.Scan(ip);

            // Output that we have finished the scan.
            if (result.Errors != null)
                Console.WriteLine("[x] An error occurred during the scan.");
            else
                Console.WriteLine("[+] " + ip + " has been successfully scanned!")

            // Allow the user to exit at any time.
            Console.Read();
        }
    }
}
```

另一种方法，也是我更喜欢的操作方法，是创建一个 *Scanner* 对象，并订阅类似 *ScanAsyncProgressChanged* 或 *ScanAsyncComplete* 的*事件处理程序*，这样我就可以完全控制我的异步方法；我可以控制它们的进度状态如何影响我的应用程序等等；例如:

*   **异步**

```
using System;
using Forerunner; // Remember to import our library.

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Our IP we would like to scan.
            string ip = "192.168.1.1";

            // Create a new scanner object.
            Scanner s = new Scanner();

            // Create a new scan object and perform a scan.
            PKScanObject result = s.PortKnock(ip);

            // Output that we have finished the scan.
            if (result.Errors != null)
                Console.WriteLine("[x] An error occurred during the scan.");
            else
                Console.WriteLine("[+] " + ip + " has been successfully scanned!")

           // Display our results.
           foreach (PKServiceObject port in result.Services)
           {
                Console.WriteLine("[+] IP: " + port.IP + " | " +
                                  "Port: " + port.Port.ToString() + " | " +
                                  "Protocol: " + port.Protocol.ToString() + " | " +
                                  "Status: " + port.Status.ToString());
           }

           // Allow the user to exit at any time.
           Console.Read();
        }
    }
}
```

**端口敲击**

我知道你在想什么。敲左舷？是，也不是。这个术语不是指传统意义上的通过一组预定义的端口进行连接的端口敲门，而是指检查是否有任何端口实际上是打开的。它实际上是通过尝试连接到每个端口并发送数据来“敲打”一个端口。就像 IP 扫描一样，端口敲门使用一个自定义对象，简称为“*端口敲门扫描对象*或 *PKScanObject* 。 *PKScanObject* 实际上包含了一系列的 *PKServiceObject* ，它们依次保存我们的端口数据；服务对象包含以下属性:

*   IP ( ***字符串*** )
*   Port ( ***Int*** )
*   协议( ***端口类型*** )
*   状态( ***布尔*** )

端口敲门与 IP 扫描的方式相似。首先，创建一个*扫描仪*对象。接下来，用您选择的 IP 创建一个新的 *PKScanObject* 并将其设置为 *PortKnock* 方法，然后显示您的结果；例如:

*   **同步**

```
using System;
using Forerunner; // Remember to import our library.

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Our IP we would like to scan.
            string ip = "192.168.1.1";

            // Create a new scanner object.
            Scanner s = new Scanner();

            // Create a new scan object and perform a scan.
            PKScanObject result = s.PortKnock(ip);

            // Output that we have finished the scan.
            if (result.Errors != null)
                Console.WriteLine("[x] An error occurred during the scan.");
            else
                Console.WriteLine("[+] " + ip + " has been successfully scanned!")

           // Display our results.
           foreach (PKServiceObject port in result.Services)
           {
                Console.WriteLine("[+] IP: " + port.IP + " | " +
                                  "Port: " + port.Port.ToString() + " | " +
                                  "Protocol: " + port.Protocol.ToString() + " | " +
                                  "Status: " + port.Status.ToString());
           }

           // Allow the user to exit at any time.
           Console.Read();
        }
    }
}
```

最后，我将向您展示一个简单的异步端口敲门的例子。它本质上与端口同步敲门是一样的，除了你可以使用事件来为你服务。您可以获得进度更新，而不必担心用户界面崩溃或系统处于锁定状态；例如:

*   **异步**

```
using System;
using System.Threading.Tasks;
using Forerunner; // Remember to import our library.

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Our IP we would like to scan.
            string ip = "192.168.1.1";

            // Setup our scanner object.
            Scanner s = new Scanner();
            s.PortKnockAsyncProgressChanged += new PortKnockAsyncProgressChangedHandler(PortKnockAsyncProgressChanged);
            s.PortKnockAsyncComplete += new PortKnockAsyncCompleteHandler(PortKnockAsyncComplete);

            // Start a new scan task with our ip.
            TaskFactory task = new TaskFactory();
            task.StartNew(() => s.PortKnockAsync(ip));

            // Allow the user to exit at any time.
            Console.Read();
        }

        static void PortKnockAsyncProgressChanged(object sender, PortKnockAsyncProgressChangedEventArgs e)
        {
            // Display our progress so we know the ETA.
            if (e.Progress == 99)
            {
                Console.Write(e.Progress.ToString() + "%...");
                Console.WriteLine("100%!");
            }
            else
                Console.Write(e.Progress.ToString() + "%...");
        }

        static void PortKnockAsyncComplete(object sender, PortKnockAsyncCompleteEventArgs e)
        {
            // Tell the user that the port knock was complete.
            Console.WriteLine("[+] Port Knock Complete!");

            // Check if we resolved an error.
            if (e.Result == null)
                Console.WriteLine("[X] The port knock did not return any data!");
            else
            {
                // Check if we have any ports recorded.
                if (e.Result.Services.Count == 0)
                    Console.WriteLine("[!] No ports were open during the knock.");
                else
                {
                    // Display our ports and their details.
                    foreach (PKServiceObject port in e.Result.Services)
                    {
                        Console.WriteLine("[+] IP: " + port.IP + " | " +
                                          "Port: " + port.Port.ToString() + " | " +
                                          "Protocol: " + port.Protocol.ToString() + " | " +
                                          "Status: " + port.Status.ToString());
                    }
                }
            }
        }
    }
}
```

[**Download**](https://github.com/jasondrawdy/Forerunner)