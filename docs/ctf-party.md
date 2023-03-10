# CTF 党:一个 Ruby 库，以提高和加速脚本/利用

> 原文：<https://kalilinuxtutorials.com/ctf-party/>

[![CTF-Party : A Ruby Library To Enhance & Speed Up Script/Exploit](img/def6c526d7c692920a4050aacf33fd3e.png "CTF-Party : A Ruby Library To Enhance & Speed Up Script/Exploit")](https://1.bp.blogspot.com/-ZmybnbIukzg/YF5az0BH1dI/AAAAAAAAIpk/pHunvwLLVUQNshMcMkUbyJI5X8GYVAvUACLcBGAsYHQ/s728/logo%25281%2529.png)

CTF 派对是一个库，通过修补字符串类来添加常用代码模式的短语法，来增强和加速 CTF 玩家(或安全研究人员、bug 赏金猎人、pentesters，但主要集中在 CTF)的脚本/漏洞开发写作。

哲学也是保持这个库是纯 ruby 的(没有依赖性),而不是重新实现另一个库已经做得很好的东西(例如, [xorcist](https://github.com/fny/xorcist) 用于 xor)。

例如，不要写:

**要求' base64 '

myvar = ' string '
myvar = base64 . strict _ encode 64(myvar)**

只写(更短更容易记住):

**要求' CTF _ party '

myvar = ' string '
myvar . to _ b64！**

**特性**

*   base64: `to_b64`、`to_b64!`、`from_b64`、`from_b64!`、`b64?`
*   文摘:`md5`、`md5!`、`sha1`、`sha1!`等。
*   标志:`flag`、`flag!`、`flag?`(应用/检查标志格式)
*   腐烂:`rot`、`rot!`、`rot13`、`rot13!`
*   十六进制:`hex2dec`、`dec2hex`、`to_hex`、`from_hex`、`hex2bin`、`bin2hex`和 bang 版本

**信用:**亚历山大·倪瓒

[**Download**](https://github.com/Orange-Cyberdefense/ctf-party)