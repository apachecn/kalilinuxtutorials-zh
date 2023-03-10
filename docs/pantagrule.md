# Pantagrule:从真实世界的泄漏密码中生成的大型 Hashcat 规则集

> 原文：<https://kalilinuxtutorials.com/pantagrule/>

[![](img/d66d76f031a240c37ffe59f43cfa98a7.png)](https://1.bp.blogspot.com/-JnlYPR8UtRY/YTBO5PURDCI/AAAAAAAAKo0/0-mgMmxw1MUY8YkKOuczpByNXuWukMLugCLcBGAsYHQ/s992/download%2B%25281%2529.png)

**Pantagrule** 是 hashcat 密码破解程序的一系列规则，从大量真实世界的密码泄露数据中生成。虽然 Pantagrule 规则文件可能很大，但这些规则都是可调的，并且比许多现有的规则集执行得更好。

Pantagrule 是使用 PACK 的 Levenshtein 反向路径算法自动生成的(Kacherginsky，2013)。然后，根据 PACK 生成规则的次数对 PACK 的输出进行排序，以生成基本规则集。这个过程类似于 _NSAKEY 在 2014 年为密码破解比赛生成的规则(_NSAKEY，2014)，但是，Pantagrule 是从一组明显更大的密码中生成的。Pantagrule 的第二版是从公开的 hashes.org“founds”语料库开发的，这是一个同类最佳的公共词汇表。这产生了比原始变体更透明的结果，原始变体使用包含 842，643，513 个唯一密码的专有语料库。

当如此大的规则集通过 PACK 输入时，会产生数百万条规则。然而，由于大多数生成的规则只出现少数几次，所以大多数有用的规则是由算法最常生成的规则。该存储库包含 PACK 在遍历现有语料库时生成的规则子集。

**优化后的变体**

为了针对真实世界的数据生成规则的第二遍优化，使用 rockyou 单词表针对 Pwned 密码 NTLM 列表运行生成的前一百万条规则。任何破解密码的规则都被添加到它自己的列表中，表现较差的规则被丢弃。

创建了四种优化类型:

*   `**popular.rule**` : pantagrule.1m 针对 HIBP 集合的前 25，000，000 个密码运行。
*   `**random.rule**` : pantagrule.1m 针对从 HIBP 集中随机选择的 25，000，000 个密码运行。
*   `**hybrid.rule**`:最成功的`**popular**`和`**random**`规则的组合的排序列表，然后被切成两半，试图创建一个更轻的、“平衡的”规则集，在更大的样本集上工作。
*   `**one.rule**`:一个版本的*oneruleturethemall*，其中附加了执行最好的`**hybrid**`规则，并且列表被截断为`**dive**`规则集的大小。有趣的是，OneRuleToRuleThemAll 和 Pantagrule 之间只有几千条规则重叠，这使得这两种策略互为补充。Pantagrule 的`**one**`比这个大小的其他已知列表执行得更好，建议您在尝试一个更大的变体之前从这个规则集开始。

**粉红豹 hashorg.v6**

在这些大型规则集取得成功后，人们尝试使用 royce 变量的逆变量，其中使用了最初的 Pantagrule 方法，但两组数据是不同的。Pantagrule 现在使用公共的 hashes.org“founds”列表作为其规则生成的单词列表基础，然后针对来自“我被 pwn 了吗”的 *V6* NTLM 列表进行优化。鉴于所用数据的完全公开性质，它还允许公布原始再现性数据，包括`pantagrule.v2.1m.rule`，这是该方法生成的前一百万条规则。V5 和 V6 的数据与前 2500 万个密码相同。

对于这个版本，`**one**`的生成方式发生了变化。为了生成`**one**`，完整的 100 万列表被附加到`**OneRuleToRuleThemAll.rule**`，然后在 Pwned V6 上校准整个集合，而不是仅仅附加规则和截断。

规则的命名约定现在已经变成了格式`**pantagrule.${corpus}.${trainingversion}.${extension}**`。这就更容易理解规则是为了什么而优化的。例如，对于`**pantagrule.hashorg.v6.random**`，我们使用了以 hashes.org 为基础的`random`方法生成规则，并针对 Pwned 密码 V6 进行了优化。

**原规则**

最初的规则是使用专有的单词表以及使用`rockyou.txt`作为基础的 Pwned 密码 NTLM v5 集来训练的。因为“训练数据”和验证数据是相同的，所以看到它们针对 V5 数据集进行优化是有意义的。

#### 的`**royce**`变种

应 hashcat 贡献者 Royce Williams 的请求，hashes.org 基金会列表也对前 100 万规则进行了优化。这是因为 HIBP 语料库相对较脏，而 hashes.org 基金会的列表可能会产生一个更实用的规则集用于现实世界的破解。这些被添加为`**royce**`变体。总的来说，`**royce**`优化似乎包含的规则更少，而`**random.royce**`在长尾密码上比最初的`**random**`有效得多。在一些变体上，性能并没有比现有规则有所提高，但是考虑到原始 Pantagrule 的训练和验证数据都来自于 *Pwned Passwords* 数据集，这似乎并不令人惊讶。Pantagrule `**royce**`变体存在于`**rules/royce**`文件夹中。

**性能对比其他常用规则**

为了测试 Pantagrule 策略相对于其他规则集的任何成功，我们将运行 Pwned Passwords V5 的前 2500 万个密码和 Pwned Passwords V5 的前 1 亿个密码的验证数据，以了解规则在破解每个规则集的“长尾”方面的有效性。规范的`**rockyou.txt**`将是我们的字典和基线。

最初的变体生成是在运行 hashcat v5.1.0 的 8x 1070Ti 钻机上完成的。`**royce**` Pantagrule 变体是在运行 hashcat git build `**v5.1.0-1774-gf96594ef**`的 4x 镭龙 VII 钻机上创建的。hashorg.v6 变种是在一个 NVIDIA Tesla M4、一个 1070Ti 和 hashcat `**v6.1.0**`上创建和验证的(非常慢)。

为了注意针对非常常见的密码的规则性能，0-25M 被分解到自己的列中。 *RPP* 列是 100M 数据集上每百分比的*规则。这是通过使用公式`**rpp = Math.round(num_rules / (0_100m_percent - 6.450))**`计算的。这个数字越大，按破解百分比运行的规则就越多。这有助于意识到规则集中的收益递减，并给出了在较慢的散列上运行规则的放大成本的概念。*

| 规则 | 规则数量 | V5 25M | V5 100M 米 | 心率血压乘积 |
| --- | --- | --- | --- | --- |
| 没有规则(只有 rockyou.txt) | Zero | 16.549% | 6.450% | 不适用的 |
| pantagrule.private.v5.one | Ninety-nine thousand and ninety-two | 79.814% | 69.417% | One thousand five hundred and seventy-four |
| pantagrule.private.v5.hybrid | Three hundred and fifty-five thousand two hundred and five | 81.346% | 73.372% | Five thousand three hundred and eight |
| pantagrule.private.v5.popular | Four hundred and seventy-eight thousand seven hundred and thirty-six | **81.792%** | 73.544% | Seven thousand one hundred and thirty-five |
| pantagrule.private.v5.random | Six hundred and sixteen thousand two hundred and thirty-six | 81.687% | 69.805% | Eight thousand eight hundred and twenty-eight |
| pantagrule.hashorg.v6.one | Ninety-nine thousand and ninety-two | 74.500% | 60.573% | One thousand eight hundred and thirty-one |
| pantagrule.hashorg.v6.hybrid | Three hundred and thirty-nine thousand nine hundred and fifty-three | 77.649% | 68.341% | Five thousand four hundred and ninety-three |
| pantagrule.hashorg.v6.popular | Five hundred and fourteen thousand four hundred and sixteen | 80.668% | 72.377% | Six thousand nine hundred and thirty-one |
| pantagrule.hashorg.v6.random | Six hundred and thirty-eight thousand seven hundred and seventy-three | 80.603% | 72.713% | Eight thousand six hundred and fourteen |
| pantagrule . private . has horg . one . royce | Ninety-nine thousand and ninety-two | 79.618% | 69.092% | One thousand five hundred and eighty-two |
| pantagrule . private . has horg . hybrid . royce | Three hundred and fourteen thousand two hundred and sixty-eight | 81.068% | 73.082% | Four thousand seven hundred and sixteen |
| pantagrule . private . has horg . popular . royce | Four hundred and twenty thousand nine hundred and eighty-four | 81.386% | 73.102% | Six thousand three hundred and sixteen |
| pantagrule . private . has horg . random . royce | Five hundred and ninety-two thousand two hundred and thirty-five | 81.659% | **74.010%** | Eight thousand seven hundred and sixty-six |
| best64 | Sixty-four | 45.117% | 24.985% | three |
| hob064 | sixty-eight | 37.786% | 19.773% | five |
| OneRuleToRuleThemAll | Fifty-two thousand and fourteen | 78.058% | 64.541% | Eight hundred and ninety-five |
| d3adhob0 | Fifty-seven thousand five hundred and forty-eight | 51.274% | 34.800% | Two thousand and thirty |
| 跳水 | Ninety-nine thousand and ninety-two | 77.111% | 63.314% | One thousand seven hundred and forty-three |
| _NSAKEY V1 | One hundred and twenty-three thousand two hundred and eighty-nine | 76.42% | 64.121% | Two thousand one hundred and thirty-eight |
| _NSAKEY V2 | One hundred and twenty-three thousand two hundred and eighty-nine | 76.882% | 64.472% | Two thousand one hundred and twenty-four |

**结论**

这项工作证实了在使用 rockyou 字典时，PACK LRP 算法在现代数据集上的局限性。虽然 LRP 算法确实生成了增加破解百分比的规则，但这是在搜索空间大幅增加的情况下实现的。由于这个原因，Pantagrule 在困难的破解需要特殊规则的情况下最有用。

值得注意的是，如果您可以使用 PACK 来生成基于特定语料库的规则，然后用它来定位您剩余的哈希，那么您可能会比使用这些大型规则集产生更高的破解百分比。例如，Pantagrule V2 在 PPv5 上的表现不如 v5 校准的规则集。

自从最初的 Pantagrule 发布以来，这些规则已经在大型技术公司和咨询公司的多个红队项目中得到证明。最初的`**pantagrule.1m**`列表破解了剩余的 HIBP 哈希中的 8%,这些哈希经受住了用于生成 Pantagrule、上述通用规则集、7 字符字母数字蛮力和 KoreLogic 的 PathWell 拓扑的语料库。

就连元规则的作者*One Rule to Rule Them All*(Hunt，2017)也表示，没有比其他规则更好的规则。每个用例都是不同的，每个规则源都可能在特定的散列转储或特定的单词列表上对您有更大的帮助。注意，这个数据并没有显示*已经破解了什么*；一些规则破解了其他规则没有破解的散列。

[Download](https://github.com/rarecoil/pantagrule)