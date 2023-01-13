# SSR Fire:自动 SSRF 探测器。只需给出域名和你的服务器

> 原文：<https://kalilinuxtutorials.com/ssr-fire/>

[![](img/9253e8af3478f5923bed497bc1dd582e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYaAFoZN8UHd_UOcLqRsZ3WttpZnnpIgrbcUfxYlQAnWxc4qfAbhpxbzFNMQIdDk-Dey4aOEytDcR1vBejtpC0kJdVVF4eyv69u9e9wiH_p28MWJSCMu7c44ERupra63glRvmQNrkPWDVMUxmG8A2SGVLH4M5Z-2Ts5JlCARqJHBL0TYaPIEVo0Ibg/s674/AVvXsEhh10PnIKy45SPiRpjS2fjFf4x2ie5fqMsOWno8LL015kvaQAdZcxDGcSxlreb_koP3N8mnWUbuSYR420hyHT9LzS2sW-U_lEAsST0z8ktQFShEW2mPlJWMxIZFDNRz_L5Kh4AL2qpUMAdwJE1HthKuSp-Pj4yFzgB-s2wRyedKc0vC7x5KO9zgpjcYw400-h384-390x220-1.png)

SSR Fire 是一款自动 SSRF 探测器。只要给域名和你的服务器，冷静！😉它还可以选择找到 XSS 和打开重定向。

### 句法

。/ssrfire . sh-d domain.com-s yourserver.com-f custom _ file . txt-c cookie

**domain.com**—>您要测试的域

**yourserver.com**——>你检测 SSRF 的服务器。打嗝合作者

**custom_file.txt** — >可选参数。你给你自己的自定义网址，而不是使用 gau

**cookies**——>可选参数。以经过身份验证的用户身份发送请求

如果你没有 burpsuite professional，你可以使用 awesome projectdiscovery 团队的 interact sh 作为你的服务器。

### 要求

由于这个使用了 GAU、FFUF、qsreplace 和 OpenRedirex，所以需要 GO 和 python 3.7+。您不需要安装这些工具，因为脚本 **setup.sh** 会安装所有的东西。你只需要安装 python 就可以了。即使你已经安装了工具，我也强烈建议你重新安装，这样在设置路径时就不会有冲突。

如果您不想再次安装这些工具，请将这些代码粘贴到您的。您的主目录和源中的配置文件。侧写他们。此外，您必须对第 10 行的 ssrfire.sh 做一个小的修改，在那里您必须替换 source /home/hari/。没有你的简介。配置文件路径。**(仅当您没有通过 setup.sh 安装工具时)**

**#将/path/替换为安装该工具的特定目录
#如果您已经为任何工具配置了路径，请将该代码替换为下面的代码。
ffuf(){
echo "用法:ffuf https://www.domain.com/FUZZ payloads . txt "
/path/to/ffuf/。/main-u $ 1-w $ 2-b $ 3-c-t 100
}
gau(){
echo "用法:gau domain . com "
/path/to/gau/。/main $ 1
}
gau _ s(){
/path/to/gau/。/main–subs $ 1
}
OpenRedireX(){
echo "用法:OpenRedireX URLs . txt payloads . txt "
python 3/path/to/OpenRedireX/OpenRedireX . py-l $ 1-p $ 2–关键字 FUZZ
}
QS replace(){
/path/to/QS replace/。/main $1
}**

**用途**

**chmod +x setup.sh
。/setup.sh(最好全部是— >强烈推荐)
。/ssrfire . sh-d domain.com-yourserver.com**

### 寻找 SSRF

现在，gau 开始获取该域的所有 URL。这可能需要很多时间。您可以在 output/domain.com/raw_urls.txt 查看到目前为止生成的输出

让它运行至少 10-15 分钟，然后如果你想继续，你可以。但是如果你想测试到目前为止获取的 URL，退出这个过程。将 raw_urls.txt 复制到 output/domain.com 中，并将其放在 domain.com 文件夹 Now run 之外

**。/SSL fire . sh-d domain.com-s yourserver.com-f/path/to/copied _ raw _ URLs . txt**

当询问是否删除现有文件夹时，选择是。

这将跳过 GAU 获取 URL 的过程。

现在，所有带参数的 URL 都将被过滤，yourserver.com 将被放入它们的参数值中。(final_urls.txt)

下一步是向所有最终的 URL 发出请求。

### 寻找 XSS

警告:这会产生大量流量。不要对您无权测试的网站使用此功能

这将测试所有获取的 URL，并根据输入在响应中的反映，将特定的 URL 添加到输出/domain . com/XSS-suspects . txt**(这可能包含误报)**

为了进一步测试这一点，您可以将这个列表输入到 XSS 检测工具(如 XSStrike)中来查找 XSS。

### 查找打开的重定向

只需输入有效负载文件的路径或使用默认的有效负载。我个人更喜欢 open redirex，因为它是专门设计来通过从列表中加载 URL 来检查打开的重定向的，它看起来更干净，不会淹没你的终端。

[**Download**](https://github.com/ksharinarayanan/SSRFire)