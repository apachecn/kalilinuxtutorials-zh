# ColdFire : Golang 恶意软件开发库

> 原文：<https://kalilinuxtutorials.com/coldfire/>

[![ColdFire : Golang Malware Development Library](img/a44f8fabe3e5f50cc168322a402785b2.png "ColdFire : Golang Malware Development Library")](https://1.bp.blogspot.com/-LSUlV2Elc2Q/YMmZJwhnPQI/AAAAAAAAJhM/NEMEmu9xo5Mgat8VedezieJwvYQe3vPzwCLcBGAsYHQ/s728/1%2B%25281%2529.png)

ColdFire 为 Golang 中的恶意软件开发提供了各种有用的方法。

大多数功能都兼容 Linux 和 Windows 操作系统。

**安装**

去找 github.com/redcode-labs/ColdFire

**包含的功能类型**

*   记录
*   辅助的
*   侦察
*   借口
*   管理
*   沙盒检测
*   破坏的

**文档**

**记录功能**

**func F(s string，arg…interface { })string
fmt 的别名。Sprintf
func PrintGood(消息字符串)
打印良好状态消息
func PrintInfo(消息字符串)
打印信息状态消息
func PrintError(消息字符串)
打印错误状态消息
func PrintWarning(消息字符串)
打印警告状态消息**

**辅助功能**

**func FileToSlice(file string)[]string
从文件中读取并返回切片，用换行符分隔行。
func 包含(s 接口{}，elem 接口{}) bool
检查接口类型是否包含另一个接口类型。
func str toInt(string _ integer string)int
将字符串转换为 int。
func IntToStr(i int) string
将 int 转换为 string。
func interval toseconds(interval string)int
将给定的时间间隔转换为秒。
func RandomInt(min Int，max int) int
从范围中返回一个随机 int。
func RandomSelectStr(list[]string)string
返回从字符串切片中随机选择的内容。
func RandomSelectInt(list[]Int)int
从 int 的切片中随机选择。
func RandomSelectStrNested(list[][]string)[]string
从嵌套的字符串切片中返回随机选择。
func remove newlines(s string)string
从字符串中删除“\n”和“\r”字符。
func FullRemove(str string，to_remove string) string
删除所有出现的子串。
func removeduplicatessstr(slice[]string)[]string
从字符串切片中删除重复项。
func RemoveDuplicatesInt(slice[]Int)[]int
从 int 切片中删除重复项。
func ContainsAny(str string，elements []string) bool
如果 slice 包含字符串，则返回 true。
func random string(n int)string
生成长度为[n]的随机字符串
func exit error(e error)
处理错误
func MD5 hash(str string)string
返回字符串的 MD5 校验和
func MakeZip(Zip_file string，files []string)错误
从文件列表中创建 zip 归档文件
func ReadFile(filename string)(string)(string，error)
读取
func WriteFile(文件名字符串)错误
将内容写入文件。
func B64d(str string)string
返回一个 base64 解码的字符串
func B64e(str string)string
返回一个 base64 编码的字符串
func file exists(file string)bool
检查文件是否存在。
func parse CIDR(CIDR string)([]string，error)
返回包含给定范围内所有可能 IP 地址的切片**。

**侦察功能**

**func GetLocalIp() string
返回机器的本地 Ip 地址。
func GetGlobalIp() string
返回机器的全局 Ip 地址。
func IsRoot() bool
检查用户是否有管理权限。
func Processes()(map[int]string，error)
返回所有进程的 PID 及其对应的名称。
func Iface() string，string
返回当前使用的无线接口的名称及其 MAC 地址。
func Ifaces() []string
返回包含所有本地接口名称的片。
func Disks() ([]string，error)
列出本地存储设备
func Users() []string，err
返回已知用户列表。
func Info()map[string]string
返回基本的系统信息。
可能的字段:用户名、主机名、go_os、os、
平台、cpu_num、内核、核心、本地 _ip、ap_ip、全局 _ip、mac。
如果该字段无法解析，则默认为“不适用”值。
func DnsLookup(主机名字符串)([]字符串，错误)
执行 DNS 查找
func RdnsLookup(ip 字符串)([]字符串，错误)
执行反向 DNS 查找
func HostsPassive(间隔字符串)[]字符串，错误
使用 ARP 监控被动发现网络上的活动主机。
可以使用参数更改发现时间。
func FilePermissions(文件名字符串)(bool，bool)
检查文件是否有读写权限。
func Portscan(target string，timeout，threads int) []int
返回目标上打开的端口列表。
func PortscanSingle(target string，port int) bool
如果所选端口打开，则返回 true。
func banner grab(target string，port int) (string，error)
从给定端口抓取服务横幅字符串。
func Networks() ([]string，error)
返回附近无线网络列表。**

**管理功能**

**func CmdOut(命令字符串)字符串，错误
执行命令并返回其输出。
func CmdOutPlatform(命令映射[字符串]字符串)(字符串，错误)
在平台感知模式下执行命令。
例如，传递{"windows":"dir "，" linux":"ls"}将执行不同的命令，
基于启动植入的平台。
func CmdRun(命令字符串)
与 cmd_out()不同，cmd_run 不返回任何东西，将输出和错误打印到 STDOUT。
func CmdDir(dirs _ cmd map[string]string)([]string，error)
在目录感知模式下执行命令。
比如传递{"/etc" : "ls"}会执行/etc 目录下的命令" ls "。
func CmdBlind(命令字符串)
在没有监督的情况下运行命令，不打印任何输出。
func CreateUser(用户名，密码字符串)错误
在系统上创建新用户。
func Bind(port int)
在给定的端口上运行绑定 shell。
func Reverse(host string，port int)
运行一个反向 shell。
func SendDataTcp(主机字符串，端口 int，数据字符串)错误
使用 Tcp 协议向远程主机发送字符串。
func senddataaudp(host string，port int，data string)错误
使用 Udp 协议向远程主机发送字符串。
func Download(url 字符串)错误
从 url 下载文件并以相同的名称保存。
func CopyFile(src string，dst string)错误
将文件从一个地方复制到另一个地方
func current dir files()[]string，错误
从当前目录返回文件列表**

**规避功能**

**func PkillPid(pid int)错误
通过 Pid 杀死进程。
func PkillName(名称字符串)error
杀死所有包含【名称】的进程。
func PkillAv() err
杀死最常见的 Av 进程。
func Wait(interval string)
在给定的时间间隔内不做任何事情。
func Remove()
从主机上删除二进制。
func settl(间隔字符串)
设置二进制文件的生存时间。
应作为 goroutine 启动。
func ClearLogs()错误
清除大部分系统日志。**

**沙盒检测功能**

**func sandbox file path()bool
通过寻找公共沙盒文件路径来检测沙盒。
仅与 windows 兼容。
func SandboxProc() bool
通过寻找通用沙盒进程来检测沙盒。
func SandboxSleep() bool
通过寻找 sleep-acceleration 机制来检测沙箱。
func sandbox disk(size int)bool
通过查找异常小的磁盘大小来检测沙箱。
func sandbox Cpu(cores int)bool
通过寻找数量异常少的 CPU 核心来检测沙盒。
func sandbox Ram(RAM _ MB int)bool
通过寻找异常少量的 RAM 来检测沙盒。
func SandboxMac() bool
通过查找本地主机的沙盒特定 Mac 地址来检测沙盒。
func SandboxUtc() bool
通过查找正确设置的 Utc 时区来检测沙箱。
func SandboxProcnum(proc _ num int)bool
检测沙盒是否有少量正在运行的进程
func SandboxTmp(entries int)bool
检测沙盒是否有少量临时目录下的条目
func sandbocal()bool
使用所有沙盒检测方法检测沙盒。如果任何沙盒检测方法返回 true，则返回 true。
func sandbox all _ n(num int)bool
使用所有沙盒检测方法检测沙盒。
如果至少检测方法返回 true，则返回 true。**

**破坏性功能**

**func WifiDisconnect()错误
从无线接入点断开
func Wipe()错误
清除整个文件系统。
func EraseMbr(device string，partition_table bool)错误
擦除设备的 Mbr 扇区。
如果为真，也删除分区表。
func Forkbomb()
运行 Forkbomb。
func Shutdown()错误
重启机器。**

**要求**

 **【github . com/Dustin/go-humanity】【中文不变】**

[**Download**](https://github.com/redcode-labs/Coldfire#disruptive-functions)