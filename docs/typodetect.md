# 类型检测:检测域的活跃突变

> 原文：<https://kalilinuxtutorials.com/typodetect/>

[![Typodetect : Detect The Active Mutations Of Domains](img/051fdb50db3db2556ab3432af2ea63b8.png "Typodetect : Detect The Active Mutations Of Domains")](https://1.bp.blogspot.com/-w7G-Hc-5wgg/YM36huj_m-I/AAAAAAAAJlE/RS_2DrZWDbIo-pTinWlhgo7gdIjGbSEugCLcBGAsYHQ/s728/Typodetect%25281%2529.png)

Typodetect 是一种工具，它使蓝色团队、SOC、研究人员和公司能够检测其域名的活跃突变，从而防止在欺诈活动中使用这些域名，如网络钓鱼和欺诈。

为此，Typodetect 允许使用 IANA 网站上发布的最新版本的顶级域名，验证区块链 DNS 中的分散域名和 DoH 服务中的恶意软件报告(HTTPS DNS)。

为了方便用户，Typodetect 默认以 JSON 格式或 TXT 格式提供报告，这取决于用户如何选择并在屏幕上显示所生成的突变摘要、活动域以及检测到的恶意软件或分散域的报告。

**安装**

使用以下内容克隆此存储库:

**git 克隆 https://github.com/Telefonica/typodetect**

运行安装程序进行安装:

**python3 pip 安装要求. txt**

**运行错字检测**

在 TypoDetect 目录中:

**python3 typodetect.py -h**

**用法:typodetect . py[-h][-u UPDATE][-t N _ THREADS][-d DOH _ SERVER][-o OUTPUT]domain
位置参数:
domain 指定要处理的域
可选参数:
-h，–help 显示此帮助消息并退出
-u UPDATE，–UPDATE UPDATE
(Y/N)用于更新 TLD 的数据库(默认值:N)
-t N_THREADS，–THREADS N _ THREADS
要处理的线程数**

简单分析一下:

**python3 typodetect.py**

更新 IANA 数据库和分析:

**python3 typodetect.py -u y**

更多线程分析:

**python 3 tycodetect . py-t<线程数> <域>**

对于不同的 DoH(目前只有 11 种云票价)

python3 typodetect.py -d 2<domain></domain>

用于创建文本报告

**python 3 tycodetect . py-o TXT<域>**

**报告**

在 reports 目录中，默认情况下，报告文件保存在 JSON 中，带有被分析域的名称和日期，例如:

**eleven paths . com 2021-01-26t 18:20:10.34568 . JSON**

对于检测到的每个活动突变，JSON 报告具有以下结构:

**【id:
【report _ DoH】:
【域】:
【A】:【ip1，ip2，…】
【MX】:【mx1，mx2，…】
}**

这些字段包含以下信息:

**id:突变的整数 id
“report _ DoH”:“”–去中心化 DNS 的域
“恶意软件”–对 DoH 报告为危险的域
“良好”–对 DoH 报告为良好的域
“域”:检测到活跃的突变。
“A”:变异的 DNS 中某个类型的 IP 地址。
“MX”:突变的 DNS 中 MX 类型的 IP 或 CNAME。**

[**Download**](https://github.com/telefonica/typodetect)