# Teatime:一个区块链 RPC 攻击框架

> 原文：<https://kalilinuxtutorials.com/teatime/>

[![Teatime : A Blockchain RPC Attack Framework](img/edf0559edb48d03b72abd8bda972873f.png "Teatime : A Blockchain RPC Attack Framework")](https://1.bp.blogspot.com/-HOPRUXpK12o/YERqMwEi1mI/AAAAAAAAIcM/3XcwDSjjOoY1v1ZQGSnv0iZg5WuU2B1SACLcBGAsYHQ/s728/blockchain%25281%2529.png)

Teatime 是一个 RPC 攻击框架，旨在使发现区块链节点中的错误配置变得容易。它可以检测各种各样的问题，从信息泄露到打开帐户，以及配置操作。

目标是使工具能够扫描易受攻击的节点，并最大限度地降低由于常见漏洞导致的基于节点的攻击的风险。Teatime 使用基于插件的体系结构，因此用您自己的检查来扩展库很简单。

请注意，该库仍然是一个概念证明，缺少文档。如果有你想看的插件，请随时在 Twitter 上联系我！

**安装**

Teatime 运行在 Python 3.6+上。

*   要开始，只需运行

**$ pip3 安装下午茶**

*   或者，克隆存储库并运行

安装$ pip3。

*   或者直接通过 Python 的`setuptools`:

**$ python3 setup.py 安装**

**例子**

要开始，只需实例化一个`Scanner`类，并传入目标 IP、端口、节点类型和实例化插件列表。考虑以下示例，以检查节点是否已同步和正在挖掘:

```
from teatime.scanner import Scanner
from teatime.plugins.context import NodeType
from teatime.plugins.eth1 import NodeSync, MiningStatus

TARGET_IP = "127.0.0.1"
TARGET_PORT = 8545
INFURA_URL = "Infura API Endpoint"

def get_scanner():
    return Scanner(
        ip=TARGET_IP,
        port=TARGET_PORT,
        node_type=NodeType.GETH,
        plugins=[
            NodeSync(infura_url=INFURA_URL, block_threshold=10),
            MiningStatus(should_mine=False)
        ]
    )

if __name__ == '__main__':
    scanner = get_scanner()
    report = scanner.run()
    print(report.to_dict())
```

查看示例目录，获取更多小示例！Teatime 是完全类型化的，所以如果阅读文档不是您的首选，也可以随意探索 IDE 中的选项。🙂

**未来发展**

Teatime 的未来是不确定的，尽管我很乐意添加超出 RPC 接口的更广泛的检查，特别是针对以下技术:

*   以太坊 2.0
*   Filecoin
*   IPFS 吗

如果你想为更小的、不太有意义的链集成插件，比如比特币或以太坊仿冒品，请随意分叉项目并单独集成它们。

[**Download**](https://github.com/dmuhs/teatime)