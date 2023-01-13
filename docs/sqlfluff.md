# SQLFluff:一个面向人类的 SQL Linter 和自动格式化程序

> 原文：<https://kalilinuxtutorials.com/sqlfluff/>

[![SQLFluff : A SQL Linter And Auto-Formatter For Humans](img/89ceb0ba1c9320e80494277bb4f507f9.png "SQLFluff : A SQL Linter And Auto-Formatter For Humans")](https://1.bp.blogspot.com/-1vVKIVrMsEo/YLcfNw_LglI/AAAAAAAAJSI/hpS4gw1tZbgz6BbH3nrxwVe49a7X2Qz_ACLcBGAsYHQ/s728/sqlfluff-wide%2B%25281%2529.png)

SQLFluff 是一个方言灵活且可配置的 SQL linter。SQLFluff 的设计考虑到了 ELT 应用程序，它还可以与 jinja 模板和 dbt 一起工作。SQLFluff 将自动修复大多数林挺错误，让您将时间集中在重要的事情上。

**入门**

首先，安装软件包并运行`**sqlfluff lint**`或**T1。**

**$ pip install SQL fluff
$ echo "从 tbl 中选择 a+b；">test . SQL
$ sqlfluff lint test . SQL
= =[test . SQL]FAIL
L:1 | P:1 | L003 |单个缩进使用的空格数不是 4 的倍数
L: 1 | P: 14 | L006 |运算符应该用一个空格括起来，除非在行首/末尾
L: 1 | P: 27 | L001 |不必要的尾随空格**

也可以用 [SQLFluff online](https://online.sqlfluff.com/) 来玩一玩。

有关完整的 CLI 用法和规则参考，请参见文档。

**文档**

欲查看完整文档，请访问 docs.sqlfluff.com。

**发布**

SQLFluff 处于测试阶段——预计该工具会随着未来版本中潜在的非向后兼容 api 和配置变化而发生显著变化。如果你想加入，请考虑[贡献](https://github.com/sqlfluff/sqlfluff/blob/master/CONTRIBUTING.md)。

每月都会发布新版本。欲了解更多信息，请访问[版本](https://github.com/sqlfluff/sqlfluff/releases)。

**松弛时的 SQLFluff**

我们在 Slack 上有一个快速发展的社区，快来加入我们吧！

[https://join . slack . com/t/sqlfluff/shared _ invite/ZT-o1f 4x 0 e 8-pZzarAIlQmKj _ 6 zwd 16 w0g](https://join.slack.com/t/sqlfluff/shared_invite/zt-o1f4x0e8-pZzarAIlQmKj_6ZwD16w0g)

[**Download**](https://github.com/sqlfluff/sqlfluff)