# PCI leech–直接内存访问(DMA)攻击软件

> 原文：<https://kalilinuxtutorials.com/pcileech-dma-attack-software/>

**PCILeech** 使用 PCIe 硬件设备读写目标系统内存。这是通过在 PCIe 上使用 DMA 来实现的。目标系统上不需要驱动程序。

**PCILeech** 支持多种内存采集设备。主要基于硬件，但也支持基于特定安全问题的转储文件和软件技术。基于 USB3380 的硬件本身只能读取 4GB 的内存，但是如果首先将内核模块(KMD)插入目标系统内核，则可以读取所有内存。基于 FPGA 的硬件能够读取所有内存。

**PCILeech** 能够将各种内核植入到目标内核中——允许通过“挂载的驱动器”轻松访问动态 ram 和文件系统。也有可能删除登录密码要求，加载未签名的驱动程序，执行代码和产生系统外壳。PCIleech 运行在 Windows/Linux/Android 上。目前支持的目标系统是:UEFI、Linux、FreeBSD、macOS 和 Windows 的 x64 版本。

PCILeech 还支持内存进程文件系统，可用于读写模式的 PCILeech FPGA 硬件设备或只读模式的内存转储文件。

开始克隆存储库并在 **pcileech_files** 文件夹中找到所需的二进制文件、模块和配置文件。

## **PCILeech 功能**

*   以大于 150MB/s 的速度从目标系统中检索内存
*   将数据写入目标系统内存。
*   4GB 内存可在本机 DMA 模式下访问(USB3380 硬件)。
*   所有存储器都可以在本机 DMA 模式下访问(FPGA 硬件)。
*   如果加载了内核模块(KMD ),就可以访问所有内存。
*   原始 PCIe TLP 访问(FPGA 硬件)。
*   挂载动态内存作为文件[Linux，Windows，macOS*]。
*   将文件系统挂载为驱动器[Linux、Windows、macOS*]。
*   将内存进程文件系统挂载为驱动程序[Windows]。
*   在目标系统上执行内核代码。
*   衍生系统外壳[Windows]。
*   衍生任何可执行文件[Windows]。
*   拉文件【Linux，FreeBSD，Windows，macOS*】。
*   推送文件【Linux，Windows，macOS*】。
*   修补/解锁(删除密码要求)[Windows、macOS*]。
*   易于创建自己的内核外壳代码和/或自定义签名。
*   此处未列出的更多功能…

**注意:**不支持 MacOS High Sierra。

## **硬件**

PCILeech 支持多种硬件设备。有关支持的基于 FPGA 的硬件的信息，请查看 PCILeech FPGA 项目。有关基于 USB3380 的硬件的信息，请查看 PCILeech USB3380。PCILeech 还支持有限功能的内存转储文件。

请在下面找到一个设备对照表。

| 设备 | 类型 | 连接 | 速度 | 64 位内存访问 | PCIe TLP 访问 |
| --- | --- | --- | --- | --- | --- |
| [AC701/FT601](https://github.com/ufrisk/pcileech-fpga/) | 现场可编程门阵列 （Field Programmable Gata Array 的缩写） | USB3 | 150 MB/秒 | 是 | 是 |
| [PCIeScreamer](https://github.com/ufrisk/pcileech-fpga/) | 现场可编程门阵列 （Field Programmable Gata Array 的缩写） | USB3 | 100 MB/秒 | 是 | 是 |
| [SP605/FT601](https://github.com/ufrisk/pcileech-fpga/) | 现场可编程门阵列 （Field Programmable Gata Array 的缩写） | USB3 | 75MB/秒 | 是 | 是 |
| [SP605/TCP](https://github.com/ufrisk/pcileech-fpga/) | 现场可编程门阵列 （Field Programmable Gata Array 的缩写） | 传输控制协议 | 100 千字节/秒 | 是 | 是 |
| [USB3380-EVB](https://github.com/ufrisk/pcileech/blob/master/usb3380.md) | USB3380 | USB3 | 150 MB/秒 | 否(仅经 KMD) | 不 |
| [PP3380](https://github.com/ufrisk/pcileech/blob/master/usb3380.md) | USB3380 | USB3 | 150 MB/秒 | 否(仅通过 KMD) | 不 |

**推荐的适配器**

*   **PE3B—**express card 到迷你 PCIe。
*   **PE3A—**PCIe 运通卡。
*   从 PCIe 到迷你 PCIe。
*   **P15S-P15F—**m . 2 钥匙 A+E 至迷你 PCIe。
*   **Sonnet Echo ExpressCard Pro—**迅雷到 express card。
*   **苹果雷电 3(USB-C)–**雷电 2 加密狗。

请注意，其他适配器也可以工作。

**也读作 [黄金眼——黄金眼 7 层 DoS 测试工具](https://kalilinuxtutorials.com/goldeneye-dos-test-tool/)**

## **安装 PCILeech**

请访问 PCILeech github [库](https://github.com/ufrisk/pcileech)，确保您拥有最新版本的 PCILeech。

克隆 PCILeech Github 存储库。二进制文件位于 pcileech_files 中，应该可以在 64 位 Windows 和 Linux 上运行。请从 pcileech_files 复制所有文件，因为有些文件包含附加模块和签名。

#### **窗户**

有关在 Windows 上运行 PCILeech 的信息，请参见 PCILeech-on-Windows [指南](https://github.com/ufrisk/pcileech/wiki/PCILeech-on-Windows)。

如果使用 USB3380 硬件，必须安装 Google Android USB 驱动程序。从[这里下载谷歌安卓 USB 驱动](http://developer.android.com/sdk/win-usb.html#download)解压驱动。
如果 FPGA 与 FT601 USB3 附加卡一起使用，必须安装 FTDI 驱动程序。从 FTDI 下载 64 位 [`FTD3XX.dll`](http://www.ftdichip.com/Drivers/D3XX/FTD3XXLibrary_v1.2.0.6.zip) 并放在`pcileech.exe`旁边。
要在 Windows 中挂载动态 ram 和目标文件系统作为驱动器，必须安装 Dokany 文件系统库。请下载并安装最新版本的 [Dokany](https://github.com/dokan-dev/dokany/releases/latest) 。

#### **Linux 和 Android**

关于在 Linux 上运行 PCILeech 的信息，请参见 [PCILeech-on-Linux](https://github.com/ufrisk/pcileech/wiki/PCILeech-on-Linux) 指南；关于 Android 的信息，请参见 [PCILeech-on-Android](https://github.com/ufrisk/pcileech/wiki/PCILeech-on-Android) 。

## **例子:**

更多示例请参见[项目维基页面](https://github.com/ufrisk/pcileech/wiki/)。维基正处于建立阶段，信息可能仍然缺失。

挂载目标系统动态 RAM 和文件系统，需要加载 KMD。本例中使用了 0x11abc000。

*   `**pcileech.exe mount -kmd 0x11abc000**`

显示特定内核植入的帮助，在本例中为 lx64_filepull 内核植入。

*   **`pcileech.exe lx64_filepull -help`**

显示转储命令的帮助。

*   **`pcileech.exe dump -help`**

假设在地址 0x7fffe000 加载了一个内核模块，则从目标系统转储所有内存。

*   `**pcileech.exe dump -kmd** **0x7fffe000**`

强制转储 4GB 以下的内存，包括使用更稳定的 USB2 方法的可访问内存映射设备。

*   `**pcileech.exe dump -force -usb2**`

接收 PCIe TLP(事务层数据包)并将其打印在屏幕上(需要正确配置的 FPGA 开发板)。

*   `**pcileech.exe tlp -vv -wait** 1000`

探测/枚举目标系统的内存以获取可读内存页面和最大内存。(仅限 FPGA 硬件)。

*   `**pcileech.exe probe**`

转储最小和最大地址之间的所有内存，不要在失败的页面上停止。只有 FPGA 硬件支持对 64 位内存的本机访问。

*   `**pcileech.exe dump -min 0x0** **-max 0x21e5fffff -force**`

强制使用特定设备(而不是默认自动检测它)。sp605_tcp 设备不会被自动检测到。

*   `**pcileech.exe pagedisplay -min 0x1000 -device** **sp605_tcp -device-addr 192.168.1.2**`

从 Windows 10 64 位内存映像挂载 PCILeech 内存进程文件系统。

*   `**pcileech.exe mount -device c:\temp\memdump_win10.raw**`

使用报告的“total meltdown”Windows 7/2008 R2 x64 PML 4 页表权限漏洞转储内存。

*   `**pcileech.exe dump -out memdump_win7.raw** **-device totalmeltdown -v -force**`

## **生成签名**

PCILeech 为 Windows、Linux、FreeBSD 和 macOS 提供了内置签名。对于 Windows 10，还可以使用 pcileech_gensig.exe 程序来生成替代签名。

## **限制/已知问题**

*   USB3380 在某些硬件上出现读写错误。尝试`pcileech.exe testmemreadwrite -min 0x1000`根据物理地址 0x1000(或任何其他地址)测试内存读取和写入，以便确认。如果存在问题，降级到 USB2 可能会有所帮助。
*   根据目标配置和使用的任何适配器，PCIeScreamer 设备当前可能会出现不稳定。
*   如果操作系统使用 IOMMU/VT-d，则不起作用。这是 macOS 上的默认设置(除非在恢复模式下禁用)。启用了基于虚拟化的安全功能的 Windows 10 不能完全工作，但这不是 Windows 10 或 Linux 中的默认设置。
*   一些 Linux 内核不工作。有时，内核中没有导出所需的符号，PCILeech 会失败。
*   基于 4.8 内核和更高版本的 Linux 可能无法与 USB3380 硬件一起工作。或者，如果目标根访问存在，编译并插入。ko (pcileech_kmd/linux)。如果系统是 EFI 引导的，则存在替代签名。
*   Windows 7:不发布签名。
*   文件系统挂载，包括内存进程文件系统，仅支持 Windows。

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ufrisk/pcileech)