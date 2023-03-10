# 再现:简单边缘服务器/反向代理

> 原文：<https://kalilinuxtutorials.com/reproxy/>

[![Reproxy : Simple Edge Server / Reverse Proxy](img/606015337e7448a1b48e36c799df1cee.png "Reproxy : Simple Edge Server / Reverse Proxy")](https://1.bp.blogspot.com/-meHPy67zCzI/YIfhiSGi6-I/AAAAAAAAI3A/JZlXG3VSUHIWgGRSSW9jACMyOY7ThPNmwCLcBGAsYHQ/s728/logo-bg-svg.png)

**Reproxy** 是一个简单的边缘 HTTP(s)服务器/反向代理，支持各种提供者(docker、static、file)。一个或多个提供者提供关于所请求的服务器、所请求的 URL、目标 URL 和健康检查 URL 的信息。它以单个二进制文件或 docker 容器的形式分发。

*   使用[自动终止 SSL 让我们加密](https://letsencrypt.org/)
*   支持用户提供的 SSL 证书
*   简单但灵活的代理规则
*   静态命令行代理规则提供程序
*   基于文件的动态代理规则提供程序
*   具有自动发现功能的 Docker 提供程序
*   支持多个(虚拟)主机
*   可选流量压缩
*   用户定义的限制和超时
*   单一二元分布
*   码头集装箱配送
*   内置静态资产服务器
*   具有路由信息和普罗米修斯度量的管理服务器

服务器(主机)可以设置为 FQDN，即 **`s.example.com`或** `*`(全部捕捉)。请求的 url 可以是正则表达式，例如`^/api/(.*)`，目的地 url 可能有正则表达式匹配的组，即 **`http://d.example.com:8080/$1`。对于上面的例子，`http://s.example.com/api/something?foo=bar`** 将被代理到 **`http://d.example.com:8080/something?foo=bar`。**

为了方便起见，带有结尾`/`和不带正则表达式组的请求扩展到`/(.*)`，在这些情况下，目的地扩展到`**/$1**`。即**`/api/`->-`http://127.0.0.1/service`**将翻译成**->-`http://127.0.0.1/service/$1`-**

HTTP 和 HTTPS 都支持。对于 HTTPS，可以使用静态证书以及自动化的 ACME(让我们加密)证书。可选的资产服务器可用于提供静态文件。启动重新代理需要至少定义一个提供程序。其余的参数是严格可选的，并且有相同的默认值。

示例:

*   使用静态提供者:`**reproxy --static.enabled --static.rule="example.com/api/(.*),https://api.example.com/$1"**`
*   自动对接发现:`**reproxy --docker.enabled --docker.auto**`

**安装**

*   对于二进制发行版，在[发布部分](https://github.com/umputun/reproxy/releases)选择合适的文件
*   docker 容器可在 [Docker Hub](https://hub.docker.com/r/umputun/reproxy) 以及 [Github 容器注册表](https://github.com/users/umputun/packages/container/reproxy/versions)上获得。即`docker pull umputun/reproxy`或`docker pull ghcr.io/umputun/reproxy`。

最新稳定版本有`:vX.Y.Z`标签(别名为`:latest`),当前主版本有`:master`标签。

**供应商**

各种提供商提供的代理规则。目前包括`file`、`docker`和`static`。每个提供者可以为代理请求和静态(资产)定义多个路由规则。用户可以同时设置多个提供商。

*参见[示例](https://github.com/umputun/reproxy/tree/master/examples)中各种提供商的示例*

**静态**

这是直接在命令行(或环境)中定义所有映射规则的最简单的提供程序。支持多个规则。每个规则是 3 或 4 个逗号分隔的元素`server,sourceurl,destination,[ping-url]`。例如:

*   `*,^/api/(.*),https://api.example.com/$1,`–将所有请求代理到任何主机/服务器，前缀为`/api`到`https://api.example.com`
*   `example.com,/foo/bar,https://api.example.com/zzz,https://api.example.com/ping`–将所有请求代理到`example.com`，并将`/foo/bar`的 url 代理到`https://api.example.com/zzz`。使用`https://api.example.com/ping`进行健康检查

最后一个(第 4 个)元素定义了用于健康报告的可选 ping url。即`*,^/api/(.*),https://api.example.com/$1,https://api.example.com/ping`。更多详情请参见[健康检查](https://github.com/umputun/reproxy#ping-and-health-checks)章节。

**文件**

`**reproxy --file.enabled --file.name=config.yml**`

`config.yml`的例子:

```
default: # the same as * (catch-all) server
  - { route: "^/api/svc1/(.*)", dest: "http://127.0.0.1:8080/blah1/$1" }
  - {
      route: "/api/svc3/xyz",
      dest: "http://127.0.0.3:8080/blah3/xyz",
      "ping": "http://127.0.0.3:8080/ping",
    }
srv.example.com:
  - { route: "^/api/svc2/(.*)", dest: "http://127.0.0.2:8080/blah2/$1/abc" }

```

这是一个动态提供程序，文件更改将自动应用。

**码头工人**

Docker provider 支持完全自动的发现(使用`--docker.auto`),无需额外配置，默认情况下会将所有请求(如`https://server/<container_name>/(.*)`)重定向到给定容器的内部 IP 和暴露的端口。将只检测活动的(运行中的)容器。

此默认值可通过标签进行更改:

*   `reproxy.server`–要匹配的服务器(主机名)。也可以是逗号分隔的服务器列表。
*   `reproxy.route`–来源路线(位置)
*   `reproxy.dest`–目的地路径。注意:这不是完整的 url，而只是将附加到容器的 ip:port 的路径
*   `reproxy.port`–被发现集装箱的目的港
*   `reproxy.ping`–目的容器的 ping 路径。
*   `reproxy.enabled`–从再现目的地启用(`yes`、`true`、`1`)或禁用(`no`、`false`、`0`)集装箱。

请注意:如果没有`--docker.auto`，目的地集装箱必须至少有一个`reproxy.*`标签才能被视为潜在目的地。

使用`--docker.auto`，所有具有暴露端口的集装箱将被视为路线目的地。有三种方法可以限制它:

*   用`--docker.exclude`明确排除一些容器，即`--docker.exclude=c1 --docker.exclude=c2 ...`
*   仅允许使用`--docker.network`的特定 docker 网络
*   设置标签`reproxy.enabled=false`或`reproxy.enabled=no`或`reproxy.enabled=0`

这是一个动态提供程序，容器状态的任何更改都将自动应用。

**SSL 支持**

SSL 模式(默认为无)可以设置为`auto` (ACME/LE 证书)、`static`(现有证书)或`none`。如果`auto`开启，将自动为所有发现的服务器名称颁发 SSL 证书。用户可以通过设置`--ssl.fqdn`值来覆盖它

**测井**

默认情况下，不会生成请求日志。这可以通过设置`--logger.enabled`来打开。日志(自动旋转)具有 [Apache 组合日志格式](http://httpd.apache.org/docs/2.2/logs.html#combined)

用户也可以使用`--logger.stdout`打开标准输出日志。它不会影响文件日志记录，但会输出一些关于已处理请求的最小信息，如下所示:

```
2021/04/16 01:17:25.601 [INFO]  GET - /echo/image.png - xxx.xxx.xxx.xxx - 200 (155400) - 371.661251ms
2021/04/16 01:18:18.959 [INFO]  GET - /api/v1/params - xxx.xxx.xxx.xxx - 200 (74) - 1.217669m 
```

**资产服务器**

用户可以打开资产服务器(默认情况下关闭)来提供静态文件。只要`--assets.location`被设置，它就将`assets.root`下的每个非代理请求视为对静态文件的请求。可以在没有任何代理提供者的情况下使用资产服务器；在这种模式下，reproxy 充当静态内容的简单 web 服务器。

除了公共资产服务器之外，还支持多个自定义静态服务器。每个提供者都有不同的方法来定义这样一个静态规则，有些提供者可能根本不支持它。例如，多个静态服务器在静态(命令行提供者)、文件提供者中是有意义的，甚至对于 docker 提供者也是有用的。

1.  静态提供者——如果源元素以`assets:`为前缀，它将被视为文件服务器。例如，`*,assets:/web,/var/www,`将通过位于`/var/www`目录之上的文件服务器来服务所有的`/web/*`请求。
2.  文件提供者–设置可选字段`assets: true`
3.  码头供应商—`reproxy.assets=web-root:location`，即`reproxy.assets=/web:/var/www`。

资产服务器支持使用`--assets.cache=<duration>`参数进行缓存控制。`0s`持续时间(默认)关闭缓存控制。持续时间是一系列十进制数字，每个数字都有可选的分数和单位后缀，如“300ms”、“1.5h”或“2h45m”。有效的时间单位是“ns”、“us”(或“s”)、“ms”、“s”、“m”、“h”和“d”。

有两种方法可以设置缓存持续时间:

1.  所有静态资产的单一值。这就像`--assets.cache=48h`一样简单。
2.  不同 mime 类型的自定义持续时间。它应该包括两部分——默认值和 mime:duration 对。在命令行中，这看起来像多个`--assets.cache`选项，即`--assets.cache=48h --assets.cache=text/html:24h --assets.cache=image/png:2h`。环境值应该用逗号分隔，例如`ASSETS_CACHE=48h,text/html:24h,image/png:2h`

**更多选项**

*   `--gzip`为响应启用 gzip 压缩。
*   `--max=N`允许设置请求的最大大小(默认 64k)
*   `--header`设置添加到每个代理响应的额外报头。例如，这是如何使用 docker compose 完成的:

```
  environment:
      - HEADER=
          X-Frame-Options:SAMEORIGIN,
          X-XSS-Protection:1; mode=block;,
          Content-Security-Policy:default-src 'self'; style-src 'self' 'unsafe-inline';
```

*   `--timeout.*`服务器和代理传输的各种超时。参见[所有应用选项](https://github.com/umputun/reproxy#all-application-options)中的`timeout`部分

**平&健康检查**

reproxy 为此提供了两个端点:

*   `/ping`以`pong`响应，并指示重新启动和运行
*   如果所有目标服务器都用`200`响应了它们的 ping 请求，则`/health`返回`200 OK`状态；如果任何服务器用非 200 代码响应，则`417 Expectation Failed`返回。它还返回 json 主体，其中包含关于通过/失败的服务的详细信息。

**管理 API**

可选，可用`--mgmt.enabled`开启。在`mgmt.listen`上暴露 2 个端点(地址:端口):

*   `GET /routes`–所有已发现路线的列表
*   `GET /metrics`–返回普罗米修斯指标(`http_requests_total`、`response_status`和`http_response_time_seconds`)

*参见[示例/指标](https://github.com/umputun/reproxy/examples/metrics)*

**所有应用选项**

```
 -l, --listen=                     listen on host:port (default: 127.0.0.1:8080) [$LISTEN]
  -m, --max=                        max request size (default: 64000) [$MAX_SIZE]
  -g, --gzip                        enable gz compression [$GZIP]
  -x, --header=                     proxy headers [$HEADER]
      --signature                   enable reproxy signature headers [$SIGNATURE]
      --dbg                         debug mode [$DEBUG]

ssl:
      --ssl.type=[none|static|auto] ssl (auto) support (default: none) [$SSL_TYPE]
      --ssl.cert=                   path to cert.pem file [$SSL_CERT]
      --ssl.key=                    path to key.pem file [$SSL_KEY]
      --ssl.acme-location=          dir where certificates will be stored by autocert manager (default: ./var/acme) [$SSL_ACME_LOCATION]
      --ssl.acme-email=             admin email for certificate notifications [$SSL_ACME_EMAIL]
      --ssl.http-port=              http port for redirect to https and acme challenge test (default: 80) [$SSL_HTTP_PORT]
      --ssl.fqdn=                   FQDN(s) for ACME certificates [$SSL_ACME_FQDN]

assets:
  -a, --assets.location=            assets location [$ASSETS_LOCATION]
      --assets.root=                assets web root (default: /) [$ASSETS_ROOT]
      --assets.cache=               cache duration for assets (default: 0s) [$ASSETS_CACHE]

logger:
      --logger.stdout               enable stdout logging [$LOGGER_STDOUT]
      --logger.enabled              enable access and error rotated logs [$LOGGER_ENABLED]
      --logger.file=                location of access log (default: access.log) [$LOGGER_FILE]
      --logger.max-size=            maximum size in megabytes before it gets rotated (default: 100) [$LOGGER_MAX_SIZE]
      --logger.max-backups=         maximum number of old log files to retain (default: 10) [$LOGGER_MAX_BACKUPS]

docker:
      --docker.enabled              enable docker provider [$DOCKER_ENABLED]
      --docker.host=                docker host (default: unix:///var/run/docker.sock) [$DOCKER_HOST]
      --docker.network=             docker network [$DOCKER_NETWORK]
      --docker.exclude=             excluded containers [$DOCKER_EXCLUDE]
      --docker.auto                 enable automatic routing (without labels) [$DOCKER_AUTO]

file:
      --file.enabled                enable file provider [$FILE_ENABLED]
      --file.name=                  file name (default: reproxy.yml) [$FILE_NAME]
      --file.interval=              file check interval (default: 3s) [$FILE_INTERVAL]
      --file.delay=                 file event delay (default: 500ms) [$FILE_DELAY]

static:
      --static.enabled              enable static provider [$STATIC_ENABLED]
      --static.rule=                routing rules [$STATIC_RULES]

timeout:
      --timeout.read-header=        read header server timeout (default: 5s) [$TIMEOUT_READ_HEADER]
      --timeout.write=              write server timeout (default: 30s) [$TIMEOUT_WRITE]
      --timeout.idle=               idle server timeout (default: 30s) [$TIMEOUT_IDLE]
      --timeout.dial=               dial transport timeout (default: 30s) [$TIMEOUT_DIAL]
      --timeout.keep-alive=         keep-alive transport timeout (default: 30s) [$TIMEOUT_KEEP_ALIVE]
      --timeout.resp-header=        response header transport timeout (default: 5s) [$TIMEOUT_RESP_HEADER]
      --timeout.idle-conn=          idle connection transport timeout (default: 90s) [$TIMEOUT_IDLE_CONN]
      --timeout.tls=                TLS hanshake transport timeout (default: 10s) [$TIMEOUT_TLS]
      --timeout.continue=           expect continue transport timeout (default: 1s) [$TIMEOUT_CONTINUE]

mgmt:
      --mgmt.enabled                enable management API [$MGMT_ENABLED]
      --mgmt.listen=                listen on host:port (default: 0.0.0.0:8081) [$MGMT_LISTEN]

Help Options:
  -h, --help                        Show this help message 
```