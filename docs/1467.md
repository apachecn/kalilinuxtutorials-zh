# 填充 Oracle 攻击者:CLI 工具和库，可轻松执行填充 Oracle 攻击

> 原文：<https://kalilinuxtutorials.com/padding-oracle-attacker/>

[![Padding Oracle Attacker : CLI Tool & Library To Execute Padding Oracle Attacks Easily](img/b7bbef7c53a0ed6eb88903f0e444f37e.png "Padding Oracle Attacker : CLI Tool & Library To Execute Padding Oracle Attacks Easily")](https://1.bp.blogspot.com/-wuq1Koesn4s/XxQ8j841MFI/AAAAAAAAG74/X6EbSEwfcd4yn1EhdQv4LBBCG5ak-clPwCLcBGAsYHQ/s1600/padding-oracle-attacker.gif)

CLI 工具和库可轻松执行[填充 oracle 攻击](https://en.wikipedia.org/wiki/Padding_oracle_attack)，支持并发网络请求和优雅的 UI。

**安装**

确保安装了 Node.js，然后运行

**$ npm 安装-全局填充-Oracle-攻击者
或
$ yarn 全局添加填充-Oracle-攻击者**

CLI 用法

```
Usage
  $ padding-oracle-attacker decrypt <url> hex:<ciphertext_hex> <block_size> <error> [options]
  $ padding-oracle-attacker decrypt <url> b64:<ciphertext_b64> <block_size> <error> [options]

  $ padding-oracle-attacker encrypt <url> <plaintext>          <block_size> <error> [options]
  $ padding-oracle-attacker encrypt <url> hex:<plaintext_hex>  <block_size> <error> [options]

  $ padding-oracle-attacker analyze <url> [<block_size>] [options]

Commands
  decrypt                  Finds the plaintext (foobar) for given ciphertext (hex:0123abcd)
  encrypt                  Finds the ciphertext (hex:abcd1234) for given plaintext (foo=bar)
  analyze                  Helps find out if the URL is vulnerable or not, and
                           how the response differs when a decryption error occurs
                           (for the <error> argument)

Arguments
  <url>                    URL to attack. Payload will be inserted at the end by default. To specify
                           a custom injection point, include {POPAYLOAD} in a header (-H),
                           request body (-d) or the URL
  <block_size>             Block size used by the encryption algorithm on the server
  <error>                  The string present in response when decryption fails on the server.
                           Specify a string present in the HTTP response body (like PaddingException)
                           or status code of the HTTP response (like 400)

Options
  -c, --concurrency        Requests to be sent concurrently                      [default: 128]
      --disable-cache      Disable network cache. Saved to                       [default: false]
                           poattack-cache.json.gz.txt by default
  -X, --method             HTTP method to use while making request               [default: GET]
  -H, --header             Headers to be sent with request.
                             -H 'Cookie: cookie1' -H 'User-Agent: Googlebot/2.1'
  -d, --data               Request body
                             JSON string: {"id": 101, "foo": "bar"}
                             URL encoded: id=101&foo=bar
                           Make sure to specify the Content-Type header.

  -e, --payload-encoding   Ciphertext payload encoding for {POPAYLOAD}           [default: hex]
                             base64          FooBar+/=
                             base64-urlsafe  FooBar-_
                             hex             deadbeef
                             hex-uppercase   DEADBEEF
                             base64(xyz)     Custom base64 ('xyz' represent characters for '+/=')

  --dont-urlencode-payload Don't URL encode {POPAYLOAD}                          [default: false]

  --start-from-1st-block   Start processing from the first block instead         [default: false]
                           of the last (only works with decrypt mode)

Examples
  $ poattack decrypt http://localhost:2020/decrypt?ciphertext=
      hex:e3e70d8599206647dbc96952aaa209d75b4e3c494842aa1aa8931f51505df2a8a184e99501914312e2c50320835404e9
      16 400
  $ poattack encrypt http://localhost:2020/decrypt?ciphertext= "foo bar 🦄" 16 400
  $ poattack encrypt http://localhost:2020/decrypt?ciphertext= hex:666f6f2062617220f09fa684 16 400
  $ poattack analyze http://localhost:2020/decrypt?ciphertext=

Aliases
  poattack
  padding-oracle-attack
```

**库 API**

const { decrypt，encrypt } = require(' padding-Oracle-攻击者')
//或
import { decrypt，encrypt } from ' padding-Oracle-攻击者'

const { blockCount，totalSize，foundBytes，interBytes } = await decrypt(options)

const { block count，totalSize，foundBytes，inter bytes，final request } = await encrypt(options)

**解密(选项:对象):许诺
加密(选项:对象):许诺**

*   **必需选项**

**url:字串**

要攻击的 URL。默认情况下，有效负载将附加在末尾。若要指定自定义注入点，请在 URL、标头(requestOptions.headers)或请求正文(requestOptions.data)中包含{POPAYLOAD}

**块大小:数量**

服务器上加密算法使用的块大小。

**is decryptionsuccess:({ status code，headers，body }) = >布尔型**

如果服务器响应指示解密成功，则返回 true 的函数。

**密文:缓冲(仅解密)**

要解密的密文。

**明文:缓冲区(仅加密)**

要加密的明文。将自动添加填充。示例:Buffer.from('foo bar '，' utf8 ')

*   **可选选项**

并发:数量= 128

并发发送网络请求。

**isCacheEnabled:boolean = true**

默认情况下，响应被缓存并保存到 poattack-cache.json.gz.txt。设置为 false 将禁用缓存。

**requestOptions: {方法，头，数据}
request options . method:string**

发出请求时使用的 HTTP 方法。默认情况下获取。POST、PUT、DELETE 是一些有效的选项。

**request options . headers:{ string:string }**

与请求一起发送的标头。示例:{ ' Content-Type ':' application/x-www-form-urlencoded ' }

**request options . body:string**

请求正文。可以是 JSON 字符串、URL 编码的参数等。必须手动设置内容类型标头。

logMode:'完整' | '最小' | '无' = '完整'

**完整:**将所有内容记录到控制台(默认)
**最小:**仅在启动和完成后记录到控制台
**无:**不将任何内容记录到控制台

transformPayload:(密文:Buffer) = >字符串

函数在发出请求时将密文转换成字符串。默认情况下，密文以十六进制编码，并插入到注入点(URL 结尾，除非{POPAYLOAD}存在)。

*   **可选选项(仅解密)**

已经找到:缓冲区

已知/发现可以跳过的明文字节(从末尾开始)。如果您提供十个字节的缓冲区，最后十个字节将被跳过。

initFirstPayloadBlockWithOrigBytes:boolean = false

用原始密文字节而不是零初始化第一个有效载荷块。
例:abcdef12345678ff 11111111111111 而不是 000000000000ff 11111111111111

startFromFirstBlock:boolean = false

从第一个块而不是最后一个块开始处理。

makeInitialRequest:boolean = true

使用提供的原始密文发出初始请求，并将服务器响应记录到控制台，以允许用户确保网络请求被正确发送。

*   **可选选项(仅加密)**

makefailrequest:boolean = true

找到新明文的密文字节后，使用找到的字节发出最终请求，并将服务器响应记录到控制台。

lastCiphertextBlock:缓冲区

最后一个块的自定义密文。默认情况下，最后一个块是零(00000000000000)。

**显影**

padding-oracle-attacker 是用 TypeScript 编写的。如果您想修改源文件并运行它们，您可以先将文件编译成 JS，然后使用 node 运行它们，或者使用 ts-node。
示例:纱线构建然后节点分布/cli …或简称 ts-节点 src/cli …

纱线构建或 npm 运行构建

将 src 目录中的 TypeScript 文件构建为 JS 文件，并将它们输出到 dist 目录。

纱线清洁或 npm 运行清洁

删除目录。

纱线棉绒或 npm 运行棉绒

使用 eslint 链接文件。

纱线测试或 npm 运行测试

使用 ava 链接并运行测试。

节点 test/helpers/vulnerable-server . js

运行易受填充 oracle 攻击的测试服务器 http://localhost:2020

[**Download**](https://github.com/KishanBagaria/padding-oracle-attacker)