# Scannerl:模块化分布式指纹识别引擎

> 原文：<https://kalilinuxtutorials.com/scannerl-fingerprinting-engine/>

Scannerl 是由 Kudelski Security 实现的模块化分布式指纹识别引擎。它可以在一台主机上采集数千个目标的指纹，但也可以轻松地分布在多台主机上。它对于指纹识别就像 zmap 对于端口扫描一样。

Scannerl 可以在 Debian/Ubuntu/Arch 上运行(但也可能在其他发行版上运行)。它使用主/从架构，其中主节点将工作(主机进行指纹识别)分发到其从节点(本地或远程)。整个部署对用户来说是透明的。

## 为什么是 Scannerl？

当使用传统的指纹识别工具进行大规模分析时，安全研究人员通常会遇到两个限制:首先，这些工具通常是为一次扫描相对较少的主机而构建的，不适合大范围的 IP 地址。

其次，如果受 IPS 设备保护的大范围 IP 地址正在被采集指纹，则被列入黑名单的可能性更高，这可能导致信息集不完整。

它旨在规避这些限制，不仅提供了同时对多个主机进行指纹识别的能力，还将负载分布到任意数量的主机上。

它还使得这些任务的分配完全透明，这使得大规模指纹项目的设置和维护变得琐碎；这样就可以专注于分析，而不是手动管理和分发指纹识别流程的艰巨任务。

除了速度因素之外，它还被设计成允许在几行代码中轻松地建立特定的指纹分析。指纹聚类的创建不仅易于设置，而且可以通过在指纹活动中添加微调扫描来进行调整。

这是执行大规模指纹识别活动的最快工具。

**也读作[BlobRunner——快速调试恶意软件分析期间提取的外壳代码](https://kalilinuxtutorials.com/blobrunner-shellcode-malware-analysis/)**

## **安装**

要从源代码安装，首先要安装 Erlang(至少是 v.18 ),为您的平台选择合适的包: [Erlang 下载](https://www.erlang-solutions.com/resources/download.html)

安装所需的软件包:

```
# on debian
$ sudo apt install erlang erlang-src rebar

# on arch
$ sudo pacman -S erlang-nox rebar
```

然后构建 scannerl:

```
$ git clone https://github.com/kudelskisecurity/scannerl.git
$ cd scannerl
$ ./build.sh
```

通过运行以下命令获取用法

```
$ ./scannerl -h
```

aur 上为 arch linux 用户提供了扫描仪

*   [scannerl-aur](https://aur.archlinux.org/packages/scannerl/)
*   scannerl-git-aur

## **用途**

```
$ ./scannerl -h
   ____   ____    _    _   _ _   _ _____ ____  _
  / ___| / ___|  / \  | \ | | \ | | ____|  _ \| |
  \___ \| |     / _ \ |  \| |  \| |  _| | |_) | |
   ___) | |___ / ___ \| |\  | |\  | |___|  _ <| |___
  |____/ \____/_/   \_\_| \_|_| \_|_____|_| \_\_____|

USAGE
  scannerl MODULE TARGETS [NODES] [OPTIONS]

  MODULE:
    -m <mod> --module <mod>
      mod: the fingerprinting module to use.
           arguments are separated with a colon.

  TARGETS:
    -f <target> --target <target>
      target: a list of target separated by a comma.
    -F <path> --target-file <path>
      path: the path of the file containing one target per line.
    -d <domain> --domain <domain>
      domain: a list of domains separated by a comma.
    -D <path> --domain-file <path>
      path: the path of the file containing one domain per line.

  NODES:
    -s <node> --slave <node>
      node: a list of node (hostnames not IPs) separated by a comma.
    -S <path> --slave-file <path>
      path: the path of the file containing one node per line.
            a node can also be supplied with a multiplier (<node>*<nb>).

  OPTIONS:
    -o <mod> --output <mod>     comma separated list of output module(s) to use.
    -p <port> --port <port>     the port to fingerprint.
    -t <sec> --timeout <sec>    the fingerprinting process timeout.
    -T <sec> --stimeout <sec>   slave connection timeout (default: 10).
    -j <nb> --max-pkt <nb>      max pkt to receive (int or "infinity").
    -r <nb> --retry <nb>        retry counter (default: 0).
    -c <cidr> --prefix <cidr>   sub-divide range with prefix > cidr (default: 24).
    -M <port> --message <port>  port to listen for message (default: 57005).
    -P <nb> --process <nb>      max simultaneous process per node (default: 28232).
    -Q <nb> --queue <nb>        max nb unprocessed results in queue (default: infinity).
    -C <path> --config <path>   read arguments from file, one per line.
    -O <mode> --outmode <mode>  0: on Master, 1: on slave, >1: on broker (default: 0).
    -v <val> --verbose <val>    be verbose (0 <= int <= 255).
    -K <opt> --socket <opt>     comma separated socket option (key[:value]).
    -l --list-modules           list available fp/out modules.
    -V --list-debug             list available debug options.
    -A --print-args             Output the args record.
    -X --priv-ports             use only source port between 1 and 1024.
    -N --nosafe                 keep going even if some slaves fail to start.
    -w --www                    DNS will try for www.<domain>.
    -b --progress               show progress.
    -x --dryrun                 dry run.
```

### **独立使用**

它可以在没有任何其他主机的本地主机上使用。但是，它仍然会在运行它的主机上创建一个从属节点。因此，还必须满足设置中描述的要求。

一种快速的方法是确保您的主机能够用

```
grep -q "127.0.1.1\s*`hostname`" /etc/hosts || echo "127.0.1.1 `hostname`" | sudo tee -a /etc/hosts
```

创建一个 SSH 密钥(如果还没有的话)并将其添加到`authorized_keys`(您需要一个 SSH 服务器运行):

```
cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

以下示例从本地主机对 google.com 的*运行 HTTP 横幅抓取*

```
./scannerl -m httpbg -d google.com
```

### **分布式使用**

为了执行分布式扫描，需要预先设置 scannerl 将用来分发工作的主机。有关更多信息，请参见设置。

Scannerl 期望使用一个从机列表(由 **-s** 或 **-S** 开关提供)。

```
./scannerl -m httpbg -d google.com -s host1,host2,host3
```

### **列出可用模块**

Scannerl 将使用 **-l** 开关列出可用模块(输出模块和指纹模块):

```
$ ./scannerl -l

Fingerprinting modules available
================================

bacnet             UDP/47808: Bacnet identification
chargen            UDP/19: Chargen amplification factor identification
fox                TCP/1911: FOX identification
httpbg             TCP/80: HTTP Server header identification
                     - Arg1: [true|false] follow redirection [Default:false]
httpsbg            SSL/443: HTTPS Server header identification
https_certif       SSL/443: HTTPS certificate graber
imap_certif        TCP/143: IMAP STARTTLS certificate graber
modbus             TCP/502: Modbus identification
mqtt               TCP/1883: MQTT identification
mqtts              TCP/8883: MQTT over SSL identification
mysql_greeting     TCP/3306: Mysql version identification
pop3_certif        TCP/110: POP3 STARTTLS certificate graber
smtp_certif        TCP/25: SMTP STARTTLS certificate graber
ssh_host_key       TCP/22: SSH host key graber

Output modules available
========================

csv                output to csv
                     - Arg1: [true|false] save everything [Default:true]
csvfile            output to csv file
                     - Arg1: [true|false] save everything [Default:false]
                     - Arg2: File path
file               output to file
                     - Arg1: File path
file_ip            output to stdout (only ip)
                     - Arg1: File path
file_mini          output to file (only ip and result)
                     - Arg1: File path
file_resultonly    output to file (only result)
                     - Arg1: File path
stdout             output to stdout
stdout_ip          output to stdout (only IP)
stdout_mini        output to stdout (only ip and result)
```

### **模块参数**

参数可以用冒号提供给模块。例如对于*文件*输出模块:

```
./scannerl -m httpbg -d google.com -o file:/tmp/result
```

### **结果格式**

scannerl 返回给输出模块的结果具有以下形式:

```
{module, target, port, result}
```

在哪里

*   **`module`** :使用的模块(二郎原子)
*   `**target**` : IP 或主机名(字符串或 IPv4 地址)
*   **`port`** :港口(整数)
*   `**result**`:见下文

`result`部分的形式为:

```
{{status, type},Value}
```

其中`{status, type}`是以下元组之一:

*   `**{ok, result}**`:指纹识别目标成功
*   指纹识别没有成功，但是目标有反应
*   **`{error, unknown}`** :指纹识别失败

`Value`是返回值——它可以是一个原子，也可以是一列元素

## **扩展扫描器**

Scannerl 在设计和实现时考虑了模块化。添加新模块很容易:

*   **指纹模块**:查询特定的协议或服务。例如， *fp_httpbg.erl* 模块允许在 HTTP 响应中检索*服务器*条目。
*   **输出模块**:输出到特定的数据库/文件系统，或者以特定的格式输出结果。例如， *out_file.erl* 和 *out_stdout.erl* 模块分别允许输出到文件或 stdout(如果未指定，则为默认行为)。

要创建新的模块，只需遵循行为( *fp_module.erl* 用于指纹模块，而 *out_behavior.erl* 用于输出模块)并实现您的模块。

新模块既可以在编译时添加，也可以作为外部文件动态添加。

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/kudelskisecurity/scannerl#distributed-setup) **信用:库德尔斯基安全**