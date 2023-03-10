# Assless-Chaps:使用 NT 哈希数据库快速破解 MSCHAPv2 挑战/响应

> 原文：<https://kalilinuxtutorials.com/assless-chaps/>

[![](img/73c92d84eaa1d1b36904d1d28b1c97d2.png)](https://1.bp.blogspot.com/-6VNnN-qUThw/YTG8m_2Cr_I/AAAAAAAAKqQ/NfSVXHpzd-guGqgypqXYPaeHKnAJLRWOACLcBGAsYHQ/s728/hash.png)

**Assless-CHAPs** 是恢复 MSCHAPv2/ntLMv1 交换中使用的 NT 哈希的有效方法，如果您有挑战和响应(例如来自 WiFi EAP WPE 攻击)。

它需要一个 NT 哈希表的数据库，关于如何从现有列表或使用 hashcat 的单词列表和规则来制作这些的说明如下。我包含了一个来自 SecLists 的示例数据库。你需要解开它。

**手法**

MSCHAPv2 交换不需要“破解”明文密码，我们只需要使用 NThash。

MSCHAPv2 将 NThash 分成三个部分，并使用每个部分作为不同的密钥来 DES 加密相同的质询(从对等方和验证方质询中派生)。NTHash 被分成两个 7 字节的密钥和一个 2 字节的密钥。这意味着最后一个密钥用空值填充，以形成所需长度的密钥。由于 DES 操作的效率和 65 535 的密钥空间，这可以被快速暴力破解。一旦我们有了这两个字节，我们就可以在数据库中查找所有 n 个以这两个字节结尾的灰。这提供了一个小得多的可能要检查的散列集。

这是一种空间与时间的权衡，类似于彩虹表。这也是一种哈希剥壳的形式。

**演讲**

这是第一次在 Defcon 29 的射频黑客村。幻灯片包含在该存储库中。

**速度**

下面是三个样本挑战/回答和三个不同单词列表的比较，一个小的私人列表，rockyou，和“我被 pwd 了吗”。这些都是在我的 Macbook Pro 2016 上完成的。Hashcat 使用这个 hash schucking 内核和两个内置的 GPU 以及一个纯的而不是优化的内核(因为后者还不存在)。Hash3 不在模拟最差情况性能的列表中。我没有包括 hashcat 在第一次运行时构建字典缓存所花费的时间。

*Hash1*

小型哈希表:

**hashcat 0.50s 用户 0.27s 系统 55% cpu 1.405 合计(8597.8 khz/s)
assless 0.05s 用户 0.00s 系统 294% cpu 0.018 合计**

Rockyou 哈希表:

**哈希卡特 2.67s 用户 0.51s 系统 93% cpu 3.413 合计
无哈希 0.05s 用户 0.01s 系统 281% cpu 0.021 合计**

HIBP 哈希表:

**hashcat 59.97s 用户 11.72s 系统 136% cpu 52.603 合计(5620.6 khz/s)
assless 0.05s 用户 0.00s 系统 292% cpu 0.018 合计**

*哈希 2*

小型哈希表:

**hashcat 0.51s 用户 0.27s 系统 55% cpu 1.409 合计(8704.7 khz/s)
assless 0.03s 用户 0.00s 系统 248% cpu 0.012 合计**

Rockyou 哈希表:

h **ashcat 2.20s 用户 0.46s 系统 110% cpu 2.409 合计(5798.4 khz/s)
无 ass 0.03s 用户 0.00s 系统 231% cpu 0.015 合计**

HIBP 哈希表:

**hashcat 65.37s 用户 12.74s 系统 135% cpu 57.712 合计(5768.7 khz/s)
assless 0.03s 用户 0.00s 系统 249% cpu 0.013 合计**

*哈希 3*

Hash 3 不存在于任何一个 hashlists 中来模拟最坏情况下的查找性能。

小型哈希表:

**hashcat 0.67s 用户 0.34s 系统 66% cpu 1.526 合计(7550.1 khz/s)
assless 0.02s 用户 0.00s 系统 211% cpu 0.012 合计**

Rockyou 哈希表:

**hashcat 2.71s 用户 0.52s 系统 94% cpu 3.415 合计(5685.4 khz/s)
无 ass 0.02s 用户 0.01s 系统 181% cpu 0.014 合计**

HIBP 哈希表:

**hashcat 125.19s 用户 27.62s 系统 139% cpu 1:49.75 合计(5634.9 khz/s)
assless 0.06s 用户 0.03s 系统 115% cpu 0.075 合计**

**安装**

rust 版本需要 SQLite 3.6.8 或更高版本。

python 版本需要`**python3**`、`**sqlite3**`和`**pycryptodome**`。

数据库创建实用程序需要 python3 和 sqlite3 CLI。

**编译**

这只适用于铁锈版本。你需要货物。

安装货物后，只需切换到 assless-chaps-rs 目录，并使用:`**cargo build --release**`构建它

生成的二进制文件将放在`**target/release**/`目录中。

**用法**

Assless 需要挑战、响应和 NThashes 数据库。或者，python 版本可以使用捆绑的优化的双字节查找文件。最简单的用法如下:

`**./assless-chaps <Challenge> <Response> <hashes.db>**`

或者

`python3 assless-chaps.py <**Challenge> <Response> <hashes.db>**`

例如:

**`./assless-chaps 5d79b2a85966d347 556fdda5f67d2b746ca3315fd8b93adcab5c792790a92e87 rockyou.db`或`python3 assless-chaps.py 5d79b2a85966d347 556fdda5f67d2b746ca3315fd8b93adcab5c792790a92e87 rockyou.db`**

输出应该类似于:

**[-]未提供两个字节的查找文件，将用暴力代替。**
**[+]在 22636 次尝试中找到:586c
[-]找到以 586c 结尾的 222 个哈希
[+]找到哈希:8846f7eaee8fb1**
[ **-]找到 186 个哈希后。
[+]找到哈希:17ad06bdd830b7
[+]全哈希:8846 f 7 eaee 8 FB 117 ad 06 BDD 830 b 7586 c**

最后的完整散列`**8846f7eaee8fb117ad06bdd830b7586c**`是`**password**`的 NT 散列。

**双字节查找——目前仅 Python**

我花了一些时间构建了一个包含所有 65 535 个可能的双字节值的列表，这些值按照大型密码语料库中最常见的值进行排序。该文件包含在`**twobytes**`中。你可以把它作为第四个参数传递给 assless。

这通常会节省几轮 DES，但不会产生很大的速度差异。如果你做很多杂凑的话可能会。

`**python3 assless-chaps.py 5d79b2a85966d347 556fdda5f67d2b746ca3315fd8b93adcab5c792790a92e87 rockyou.db twobytes**`

**[+]在 65533 次尝试中找到:586c
[-]找到 222 个以 586c 结尾的哈希
[+]找到哈希:8846f7eaee8fb1
[-]找到 186 个哈希后。
[+]找到哈希:17ad06bdd830b7
[+]全哈希:8846 f 7 eaee 8 FB 117 ad 06 BDD 830 b 7586 c**

**创建自己的哈希字典**

`**mksqlitedb.py**`文件将帮助把一个 CSV 散列文件转换成数据库。

`**python3 mksqlitedb.py <database name> <csv file>**`

CSV 文件需要三列:

*   哈希的最后两个字节(最后四个 ASCII 字符)
*   前 7 个字节(前 14 个 ASCII 字符)
*   第二个 7 字节(第 15-29 个 ASCII 字符

例如，散列值`**8846f7eaee8fb117ad06bdd830b7586c**`将变成:

`**586c,8846f7eaee8fb1,17ad06bdd830b7**`

这种正则表达式转换的一个例子是:`**echo 8846f7eaee8fb117ad06bdd830b7586c | sed "s/^\(.**\{14\}\)\(.\{14\}\)\(.\**{4\}\)$/\3,\1,\2/"**`

你可以选择一个现有的哈希表(比如我被 Pwned 了吗)或者从 hashcat 和你喜欢的单词表/规则组合中生成你自己的。

**利用我被 pwn 了**

HIBP 密码列表已经可以作为 NT 哈希下载，只需要从文件中删除计数，并将其转换为 CSV 格式导入到数据库中。

这可以使用标准的 Unix 实用程序`**sed**`来完成，如下所示:

`**sed "s/^\(.\{14\}\)\(.\{14\}\)\(.\{4\}\):.*/\3,\1,\2/ pwned-passwords-ntlm-ordered-by-hash.txt" > hibp.csv**`

之后可以使用 **`mksqlitedb.py hibp.db hibp.xsc`将其导入。**

**使用 Hashcat 从单词列表和规则中创建一个哈希 csv 文件**

您需要对 1000 模式的 OpenCL 模块做一个小的代码更改，使它能够输出每个散列，而不仅仅是那些匹配您的破解候选的散列。默认情况下，它会以所需的正确 CSV 格式生成哈希。

*   切换到您的 hashcat `**OpenCL**`目录:`**cd hashcat/OpenCL**`
*   应用补丁:`**patch < m01000_a0-pure.cl.patch**`
*   准备一个不可能破解 NT 哈希的文件，比如`**echo 11111111111111111111111111111111 > impossible_hash**`
*   像平常一样破解，但是禁用 potfile 并将输出重定向到一个文件:`**hashcat -m1000 impossible_hash rockyou.txt -r best64.rule --potfile-disable --quiet > rockyou.csv**`
*   创建您的哈希数据库:`**python3 mksqlitedb.py rockyou.db rockyou.csv**`

**关于磁盘空间和文件大小的说明**

SQLite 数据库通常比用于创建它的 CSV 文件大 61%。根据文件的大小，创建数据库也需要一些时间。相应地准备您的文件系统需求。

下面是一个使用 rockyou 字典的示例:

*   Base rockyou 字典 129M
*   hashcat 生成的 rockyou.csv 462M
*   生成的 SQLite 数据库 rockyou.db 746M
*   BZip2 最大压缩 rockyou.db.bz2 339M

您可以通过动态转换和插入每个散列来节省空间，并且跳过对中间 CSV 文件的需要。

**NTLMv1 SSP**

NTLMv1 将以完全相同的方式工作，除非它使用 SSP。如果您得到一个以一串零结尾的 LM 响应，您就会知道 SSP 是否在使用中。你可以使用附带的`**ntlm-ssp.py**`来制作 assless 需要的服务器挑战。

像这样运行:`**python3 ntlm-ssp.py <lm response> <challenge>**`

例如，如果我们使用来自 hashcat 示例哈希的示例 NTLMv1-SSP 质询响应:`**u4-netntlm::kNS:338d08f8e26de93300000000000000000000000000000000:9526fb8c23a90751cdd619b6cea564742e1e4bf33006ba41:cb8086049ec4736c**`

你会通过 LM，然后像这样挑战:

`**python3 ntlm-ssp.py 338d08f8e26de93300000000000000000000000000000000 cb8086049ec4736c**`

并得到以下响应:

`**The server challenge is: 724edf24aea0d68b**`

然后就可以用普通的无腿子来破解了:

`**./assless-chaps 724edf24aea0d68b 9526fb8c23a90751cdd619b6cea564742e1e4bf33006ba41 hashes.db**`

[**Download**](https://github.com/sensepost/assless-chaps)