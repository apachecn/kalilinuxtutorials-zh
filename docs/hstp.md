# Hyper 网络上的简单超级服务传输协议

> 原文：<https://kalilinuxtutorials.com/hstp/>

[![](img/b90fe5f4de2c964b8b42b0432eb0ef8f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqFsUH2Iz-0ghZOX9Si0fNA009VjfWqk3l1H3-6rCbBMjxVvdXL3hQpk_sNqTuKFdVpMn5V13z0Oud3VZfkKLm33T6StJY8SMtVubIZChnoIHoHBVQQyS3xovI2ace9cNlELxfaYIH3pNVSNWLx3LiAumXpisxc7QMcQOaQMZFBjeCChe2fn0_x6KZ/s728/HSTP.png)

HSTP 协议旨在为超级服务传输协议开发应用层抽象。

```
HSTP is a recursion as nature of HSTP. This protocol implements itself as a interface. On every internet connected device, there is a HSTP instance. That's why the adoption is not needed. HSTP already running top of the internet. We have just now achieved to explain the protocol over protocols on heterogeneous networks. That's why do not compare with web2, web3 or vice versa
```

## 摘要

HSTP 是用于异构网络的应用表示接口。

HSTP 接口强制实施一组方法，以便能够与网络中的其他节点进行通信。因此，服务器、客户端和其他节点可以通过基于[信任的端到端加密方式](https://github.com/cagataycali/HSTP/blob/main/'./assets/schema.jpg')相互通信。到时候节点解析是基于[最快路径解析算法我写](https://github.com/cagataycali/HSTP/blob/main/assets/dns-resolution.jpg)。

**一个小概述**

想想看，我们在一个母亲和一个父亲幸福生活的情况下。他们有孩子了！突然，母亲需要定期服药来治疗疾病。这药对婴儿来说是毒药。婴儿在哭，母亲打电话给父亲，因为他是唯一可以信任的人来帮助婴儿。但是父亲有时不能呆在家里，他需要做一些事情来喂养婴儿。父亲听说一个送牛奶的人以低价出售新鲜优质的牛奶。父亲决定试着和送牛奶的人谈谈，送牛奶的人把牛奶送给父亲，父亲把牛奶带给母亲。母亲把牛奶喂给婴儿。宝宝现在很开心，宝宝睡着了，妈妈看到宝宝很开心。

这家人从来不从外面买牛奶，这是他们第一次给婴儿买牛奶:(妈妈不知道送奶员的号码，送奶员不知道家庭地址)

```
As steps:

0)  - Baby wants to drink milk.
1)  - Baby cries to the mom.
3)  - Mom see the baby is crying.
4)     - Mom checks the fridge. Mom sees the milk is empty. (Mother is only trusting the Father)
5)        - Mom calls the father.
6)        - Father calls the milkman.
7)        - Milkman delivers the milk to father.
8)        - Father delivers the milk to mom.
9)  - Mom gives the milk to the baby.
10) - Baby drinks the milk.
11) - Baby is happy.
12) - Baby sleeps.
13) - Mother see the baby is happy and sleeps.
14) - In order to be able to contact the milkman again, the mother asks the father to tell her that she wants the milkman to save the address of the house and the mobile phone of the mother.
15)     - Mother calls the father.
16)     - Father calls the milkman.
17)     - Milkman saves the address of the house and the mobile phone of the mother.

Oops, tomorrow baby wakes up and cries again,
0) - Baby wants to drink milk.
1) - Baby cries to the mom.
2) - Mom see the baby is crying.
3)    - Mom checks the fridge. Mom sees the milk is empty. (Mother is trusting the Father had right decision in the first place by giving the address to the milkman, and the milkman had right decision in the first place by saving the address of the house and the mobile phone of the mother.)
4)    - Mother calls the milkman (Mother is trusting the Father's decision only)
5)    - Milkman delivers the milk to mom.
6) - Mom gives the milk to the baby.
7) - Baby drinks the milk.
8) - Baby is happy.
9) - Baby sleeps.
10) - Mother see the baby is happy and sleeps.
11) - Mother is happy and the mother trust the milkman now. 
```

你正在阅读的这份文件表明，互联网人通过信任服务于客户来联系他人，这种信任只有通过提供良好的服务才能维持。信任是关键，但不足以生存。服务必须可靠、一致、便宜。除非人民决定不再要求你。

所以，这很容易，对吗？这么简单就明白了，故事里的那些人是谁？

*   宝宝是客户。
*   妈妈是客户。
*   父亲是客户。
*   送奶工是服务员。

还有，

*   宝宝可能是**【时间】**的服务器。
*   妈妈是宝宝的服务员。
*   爸爸是妈妈的服务员。
*   送奶员是父亲的服务员。
*   送奶员是妈妈的服务员。

孩子在可靠的人手中。没什么好担心的。他们爱你，等你长大有了孩子你就明白了。

//技术步骤解释很快，但没有你看到的那么难。

### 什么是 HSTP？

HSTP 是一个接口，它是应用层必须实现的一组方法。该接口用于与网络中的其他节点通信。该接口设计用于[异构网络](https://en.wikipedia.org/wiki/Heterogeneous_network)中。

### 什么是 HSTP 节点？

HSTP 应在网络连接设备/环境的任何层上实施。

HSTP 节点可以是任何链中的 TCP 服务器、HTTP 服务器、静态文件或契约。一个 HSTP 节点能够呼叫任何其它 HSTP 节点。因此，节点可以自由地相互呼叫，可以检查它们的系统状态，并且可以相互通信。

### 什么样的网络抽象层？

HSTP 已经在语言层面上实现了，由人来实现。英语是世界上最常用的语言。JavaScript 是众所周知的也是浏览器环境中最常用的语言。Solidity 用于基于 EVM 的链，hyperbees 用于基于 TCP 的网络，等等。

HSTP 接口应用于任何 HSTP 连接的设备/网络之间。

*   [宇宙]通过[HSTP]与[宇宙]对话
    *   【亲切】宇宙对话世界。
        *   【世界】地球用声音频率和 *HSTP* 交谈。
            *   【国家】西沙和*HSTP*X 音频。
                *   【社区】CommunityX Xish 上 Community Xi。
            *   【国家】Y 谈 Yish 和 *HSTP* 。
            *   【国家】Z 谈齐什与 *HSTP* 。
        *   [世界]火星用无线电频率交谈。
            *   UUU 一号与 UUU 一号交谈，而 HSTP 一号与他交谈。
                *   **信息:** UUU-1 可以调用，**宇宙/种类/世界/地球/X/社区 X/查询**
        *   [世界]木星与光频率对话，不实施 HSTP。
            *   信息:如果地球想和木星对话，我们可以在宇宙的木星代理上加一个 HSTP。
    *   【亲切】宇宙谈论原子和 *HSTP* 。
        *   【原子】…和 *HSTP* 。
            *   …还有 *HSTP*
                *   [Y] …和 *HSTP* 。
                    *   **信息:**【Y】可以与**宇宙/种类/世界/火星/细菌/UUU-1/查询对话**
        *   【原子】…和 *HSTP* 。
            *   …还有 *HSTP*
                *   [Y] …和 *HSTP* 。
                    *   **Info:**【Y】可以和**宇宙/类/世界/火星/细菌/UUU-1/查询** **Info:** 类宇宙可以和火星对话，火星也可以和类宇宙对话。

### HSTP 的目的是什么？

**无限扩展选项:**任何 TCP 连接的设备都可以通过 HSTP 与任何其他 TCP 连接的设备进行对话。这意味着任何网络浏览器都是另一个 HSTP 节点的服务，并且任何网络浏览器都可以调用任何其他网络浏览器。

**统一应用表现接口:** HSTP 是一个统一的接口，是应用层必须实现的一组方法。

**异构网络:**网络的任何参与者都可以与网络的其他参与者共享资源。资源可以是 CPU、内存、存储、网络等。

自从区块链技术公司称之为 web3 以来，人们就开始讨论 web 版本之间的差异。比较是增量式数字系统教育思维方式的表现。哪个更好:都不是。我们必须建立可以用统一协议对话的系统，在服务之下可以是任何东西。HSTP 正以此为目标。

### HSTP 的组成部分是什么？

**注册接口**注册接口设计用于 TCP 层，能够注册网络中的顶级 tld 节点。第一次实现 HSTP TCP 中继将解决 **hstp/**

注册表有两个界面部分:

*   **注册**方法，用于注册网络中的新节点。
*   **解析**方法，用于解析网络中的一个节点。

注册表实现需要两个 HSTP 节点，

1.  超级蜜蜂

*   异构网络将解析 RPC，TCP，HTTP，HSTP 等的注册表。

2.  任何 EVM 的连锁店。(以太坊，币安智能链，多边形等。)

*   Registry.sol 将解析 HSTP 节点的注册表。可以通过另一个网络转播。

**路由器接口**

出于演示目的，我们将使用以下实体示例:

```
// SPDX-License-Identifier: GNU-3.0-or-later
pragma solidity ^0.8.0;

import "./HSTP.sol";
import "./ERC165.sol";

enum Operation {
    Query,
    Mutation
}

struct Response {
    uint256 status;
    string body;
}

struct Registry {
    HSTP resolver;
}

// HSTP/Router.sol
abstract contract Router is ERC165 {
    event Log(address indexed sender, Operation operation, bytes payload);
    event Register(address indexed sender, Registry registry);
    mapping(string => Registry) public routes;

    function reply(string memory name, Operation _operation, bytes memory payload) public virtual payable returns(Response memory response) {
        emit Log(msg.sender, _operation, payload);
        // Traverse upwards and downwards of the tree.
        // Tries to find the closest path for given operation.
        // If the route is registered on HSTP node, reply from children node.
        // If the node do not have the route on this node, ask for parent.
        if (routes[name]) {
            if (_operation == Operation.Query) {
                return this.query(payload);
            } else if (_operation == Operation.Mutation) {
                return this.mutation(payload);
            }
        }
        return super.reply(name, _operation, payload);
    }

    function query(string memory name, bytes memory payload) public view returns (Response memory) {
        return routes[name].resolver.query(payload);
    }

    function mutation(string memory name, bytes memory payload) public payable returns (Response memory) {
        return routes[name].resolver.mutation(payload);
    }

    function register(string memory name, HSTP node) public {
        Registry memory registry = Registry({
            resolver: node
        });
        emit Register(msg.sender, registry);
        routes[name] = registry;
    }

    function supportsInterface(bytes4 interfaceId) public view virtual override returns (bool) {
        return interfaceId == type(HSTP).interfaceId;
    }
}

```

**HSTP 接口**

```
// SPDX-License-Identifier: GNU-3.0-or-later
pragma solidity ^0.8.0;

import "./Router.sol";

// Stateless Hyper Service Transfer Protocol for on-chain services.
// Will implement: EIP-4337 when it's on final stage.
// https://github.com/ethereum/EIPs/blob/master/EIPS/eip-4337.md
abstract contract HSTP is Router {
    constructor(string memory name) {
        register(name, this);
    }

    function query(bytes memory payload)
        public
        view
        virtual
        returns (Response memory);

    function mutation(bytes memory payload)
        public
        payable
        virtual
        returns (Response memory);
}
```

**示例 HSTP 节点**

HSTP 节点有权通过 super.reply(名称、操作、有效载荷)方法调用父路由器。HSTP 节点还可以通过调用 this.query(有效负载)或 this.mutation(有效负载)方法来调用子节点。

HSTP 节点可以是智能合同、web 浏览器或 TCP 连接设备。

节点完全有能力将更多的 HSTP 节点作为子服务添加到网络或自身。

```
 HSTP  HSTP
    /    \   /  \
  HSTP   HSTP  HSTP
        /    \
      HSTP  HSTP
    /       /
    HSTP   HSTP 
```

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.0;

import "hstp/HSTP.sol";

// Stateless Hyper Service Transfer Protocol for on-chain services.
contract Todo is HSTP("Todo") {

    struct ITodo {
        string todo;
    }

    function addTodo(ITodo memory request) public payable returns(Response memory response) {
        response.body = request.todo;
        return response;
    }

    // Override for HSTP.
    function query(bytes memory payload)
        public
        view
        virtual
        override
        returns (Response memory) {}

    function mutation(bytes memory payload)
        public
        payable
        virtual
        override
        returns (Response memory) {
            (ITodo memory request) = abi.decode(payload, (ITodo));
            return this.addTodo(request);
        }
}
```

### 提案

以太坊提案现在是草案，但是协议有 referance 实现 [Todo.sol](https://github.com/cagataycali/HSTP/blob/main/examples/Chain/Todo/Todo.sol) 。

### 运行在 HSTP 之上的令人敬畏的网络服务

[完整列表在此](https://github.com/cagataycali/awesome-web3-services)

### 你好世界

你现在可以测试 HSTP 并尝试混音。

### 怎么玩协议？

*   将下面的源代码复制到[https://remix.ethereum.org/](https://remix.ethereum.org/)
*   部署在任何 EVM 为基础的链。
*   调用函数并在 HSTP 上尝试不同的网络拓扑。

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.0;

import "hstp/HSTP.sol";

// Stateless Hyper Service Transfer Protocol for on-chain services.
contract Todo is HSTP("Todo") {

    struct TodoRequest {
        string todo;
    }

    function addTodo(TodoRequest memory request) public payable returns(Response memory response) {
        response.body = request.todo;
        return response;
    }

    // Override for HSTP.
    function query(bytes memory payload)
        public
        view
        virtual
        override
        returns (Response memory) {}

    function mutation(bytes memory payload)
        public
        payable
        virtual
        override
        returns (Response memory) {
            (TodoRequest memory todoRequest) = abi.decode(payload, (TodoRequest));
            return this.addTodo(todoRequest);
        }
}
```

[Click Here To Download](https://github.com/cagataycali/HSTP)