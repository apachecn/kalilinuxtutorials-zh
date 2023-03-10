# 豆腐:Linux 的 Windows 离线文件系统黑客工具

> 原文：<https://kalilinuxtutorials.com/tofu/>

[![](img/dbe38541096bbd83a2da9ab0ad50ce2f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdFkY4OmAa1E62fRd18NpiQYzkZjRVSE1ZuT86lT8Phla4ETL3KwPeEcVHxSfObqapSaekzj0RRSFvV4rxNW9jPxdGnm7E7Bieg6nSv6-rlsrb2VGgUcRHwLLDFKtqSBd-pDUesZQDkh25gvjZlrzy77k41pOQaixaqwKpGiSg2YZQv-jejOqDWi6R/s728/tofu%20(1).png)

**豆腐**是一个模块化工具，用于入侵离线 Windows 文件系统，绕过登录屏幕。可以做哈希转储，OSK 后门，用户枚举等等。

# 它是如何工作的

当 Windows 计算机关闭时，除非它启用了 Bitlocker 或其他加密服务，否则它的存储设备包含设备上存储的所有内容，就像它已解锁一样。这意味着您可以从可引导 USB 上的操作系统进行引导，并访问其文件——或者甚至只是将文件系统连接到另一台计算机。这个工具有助于你从 Linux 访问 Windows 文件系统(使用上面提到的方法之一)；它有实用程序，可以转储 NTLM 密码哈希，列出用户，安装后门程序，以产生一个提升的命令提示符在登录屏幕上，等等。

# 模块

因为豆腐是在模块上工作的，所以可以针对不同的目的进行扩展。有关示例，请参见“模块”部分。
当前模块:
1。*hash dump . py*–从目标 Windows 文件系统
2 转储 NTLM 散列。*osk _ back door . py*–后门 osk.exe 绕过登录；还包括一个“解锁”模块
3。*List _ users . py*–列出在 Windows 文件系统上拥有配置文件的用户
4。*chrome . py*–转储 Windows 文件系统上所有用户的 chrome 历史和登录数据
5。*get _ dpapi _ master keys . py*–从 Windows 文件系统转储 DP API 主密钥
6。*enum _ unattend . py*–枚举无人参与文件
7。*memory _ strings . py*–在电脑的内存中搜索数据
8。*startup . py*–将程序注入用户的启动目录
9。*wifi . py*–使用 DPAPI 获取 Wi-Fi 密码

# 用法

' list ':以 MSDOS、NTFS 或-FVE-FS- (BITLOCKER)格式列出/dev/中的所有存储设备；这将把驱动器路径加载到内存
'usedrive ':设置要使用的驱动器；可以使用从“列表”命令分配的编号
“模块”:列表模块；这将把模块名加载到内存中，所以你需要在选择一个模块之前运行这个命令
‘使用’:使用选择的模块

# 设置

**(需要以 root 身份运行，因为 PyPyKatz 的导入路径目录依赖于当前用户，这需要以 root 身份运行)**
*sudo pip 3 install-r requirements . txt
sudo python 3 豆腐. py*

## 建有

pycrypt mode
pykatz

### **警告:如果你正在编写一个模块，在运行它之前确保它不会造成任何损害**

[**Download**](https://github.com/puckblush/tofu)