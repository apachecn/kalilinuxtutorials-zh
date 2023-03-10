# 无头打嗝–使用打嗝套件自动进行安全测试

> 原文：<https://kalilinuxtutorials.com/headless-burp-automate-security/>

Headless Burp 提供了对 Burp 的扩展，允许您通过命令行在 Headless 模式下运行 Burp Suite 的 Spider 和 Scanner 工具。

但是，它能做的更多！它可以生成一个类似 JUnit 的报告，该报告可以指示 CI 服务器在发现任何漏洞时将构建标记为“失败”。您还可以将一些问题标记为误报，这些问题将不会在下次扫描报告中报告。

## **无头打嗝建立**

```
./mvnw
```

在 target/headless-burp-scanner-master-SNAPSHOT-jar-with-dependencies . jar 中将该扩展打包为一个胖 jar

**也读作[Peda-Python Exploit 开发援助 GDB](https://kalilinuxtutorials.com/peda-python-exploit-development/)**

## **用途**

如上图所示安装延伸件或从 [BApp 商店](https://portswigger.net/bappstore/d54b11f7af3c4dfeb6b81fb5db72e381)安装延伸件

#### **使用**就地**建造延伸震击器**

**On *nix** :

```
java -Xmx1G -Djava.awt.headless=true \
-classpath headless-burp-scanner-master-SNAPSHOT-jar-with-dependencies.jar:burpsuite_pro_v1.7.31.jar burp.StartBurp \
--unpause-spider-and-scanner \
--project-file=project.burp -c config.xml
```

**关于 Cygwin** :

```
java -Xmx1G -Djava.awt.headless=true \
-classpath "headless-burp-scanner-master-SNAPSHOT-jar-with-dependencies.jar;burpsuite_pro_v1.7.31.jar" burp.StartBurp \
--unpause-spider-and-scanner \
--project-file=project.burp -c config.xml
```

#### **使用分机从** [**BApp 店**](https://portswigger.net/bappstore/d54b11f7af3c4dfeb6b81fb5db72e381)

```
java -Xmx1G -Djava.awt.headless=true \
-classpath burpsuite_pro_v1.7.31.jar burp.StartBurp \
--unpause-spider-and-scanner \
--project-file=project.burp -c config.xml
```

**在 Cygwin 上:**

```
java -Xmx1G -Djava.awt.headless=true \
-classpath "burpsuite_pro_v1.7.31.jar" burp.StartBurp \
--unpause-spider-and-scanner \
--project-file=project.burp -c config.xml
```

#### **配置**

```
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://nets.eu/burp/config">
    <reportType>HTML</reportType> <!-- JUNIT|HTML|XML -->
    <targetSitemap><![CDATA[http://localhost:5432]]></targetSitemap> <!-- atleast one of targetSitemap or scope must be specified -->
    <scope> <!-- atleast one of targetSitemap or scope must be specified -->
        <url><![CDATA[http://localhost:5432/]]></url> <!-- multiple allowed -->
        <exclusions> <!-- optional -->
            <exclusion><![CDATA[localhost:5432/#/logout]]></exclusion>
        </exclusions>
    </scope>
    <false-positives> <!-- optional -->
        <issue>
            <type>5244416</type>
            <path>.*</path>
        </issue>
        <issue>
            <type>5247488</type>
            <path>.*bower_components.*</path>
        </issue>
    </false-positives>
</config>
```

有关配置文件的示例，请参见 xsd 的 [config.xml](https://github.com/NetsOSS/headless-burp/blob/master/headless-burp-scanner/src/test/resources/config.xml) 和[headless-burp-scanner-config . xsd](https://github.com/NetsOSS/headless-burp/blob/master/headless-burp-scanner/src/main/resources/headless-burp-scanner-config.xsd)

#### **命令行选项**

```
--project-file=VAL          Open the specified project file; this will be created as a new project if the file does not exist (mandatory)
-c (--config) <file>        Configuration file (mandatory)
-p (--prompt)               Indicates whether to prompt the user to confirm the shutdown (useful for debugging)
-v (--verbose)              Enable verbose output

--diagnostics               Print diagnostic information
--use-defaults              Start with default settings
--collaborator-server       Run in Collaborator server mode
--collaborator-config=VAL   Specify Collaborator server configuration file; defaults to collaborator.config
--config-file=VAL           Load the specified project configuration file(s); this option may be repeated to load multiple files
--user-config-file=VAL      Load the specified user configuration file(s); this option may be repeated to load multiple files
--auto-repair               Automatically repair a corrupted project file specified by the --project-file option
```

## **场景**

该扩展被设计为多功能的，并支持多种场景

#### **场景 A:使用打嗝功能扫描 URL 是否存在安全问题**

1.  创建一个文件–config . XML，如下所示，并将要扫描的 URL 添加到范围中。

```
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://nets.eu/burp/config">
    <reportType>HTML</reportType>
    <targetSitemap><![CDATA[http://localhost:5432]]></targetSitemap>
    <scope>
        <url><![CDATA[http://localhost:5432/auth]]></url>
        <url><![CDATA[http://localhost:5432/users]]></url>
        <url><![CDATA[http://localhost:5432/users/1]]></url>
        <url><![CDATA[http://localhost:5432/users?search=asd]]></url>
        <url><![CDATA[http://localhost:5432/bar/foo]]></url>
    </scope>
</config>
```

2.  按照[用法](https://github.com/NetsOSS/headless-burp#usage-1)部分所示运行

#### **场景 B:使用 Burp 扫描 URL 的安全问题，但不扫描某些路径**

1.  向配置文件添加一个*排除*块。

```
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://nets.eu/burp/config">
    <reportType>HTML</reportType>
    <targetSitemap><![CDATA[http://localhost:5432]]></targetSitemap>
    <scope>
        <url><![CDATA[http://localhost:5432/auth]]></url>
        <url><![CDATA[http://localhost:5432/users]]></url>
        <url><![CDATA[http://localhost:5432/users/1]]></url>
        <url><![CDATA[http://localhost:5432/users?search=asd]]></url>
        <url><![CDATA[http://localhost:5432/bar/foo]]></url>
        <exclusions>
            <exclusion><![CDATA[localhost:5432/#/logout]]></exclusion>
            <exclusion><![CDATA[localhost:5432/#/users/delete]]></exclusion>
            <exclusion><![CDATA[localhost:5432/#/creepy/crawly]]></exclusion>
        </exclusions>
    </scope>
</config>
```

2.  按照[用法](https://github.com/NetsOSS/headless-burp#usage-1)部分所示运行

#### **场景 C:使用 Burp 扫描 URL 是否存在安全问题，但抑制扫描报告中的误报**

1.  将问题类型和路径为*(可以从 burp 扫描报告中检索)的*误报*块添加到配置文件中。你可以在这里找到更多关于[问题定义的细节](https://portswigger.net/kb/issues)*

```
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://nets.eu/burp/config">
    <reportType>HTML</reportType>
    <targetSitemap><![CDATA[http://localhost:5432]]></targetSitemap>
    <scope>
        <url><![CDATA[http://localhost:5432/auth]]></url>
        <url><![CDATA[http://localhost:5432/users]]></url>
        <url><![CDATA[http://localhost:5432/users/1]]></url>
        <url><![CDATA[http://localhost:5432/users?search=asd]]></url>
        <url><![CDATA[http://localhost:5432/bar/foo]]></url>
        <exclusions>
            <exclusion><![CDATA[localhost:5432/#/logout]]></exclusion>
            <exclusion><![CDATA[localhost:5432/#/users/delete]]></exclusion>
            <exclusion><![CDATA[localhost:5432/#/creepy/crawly]]></exclusion>
        </exclusions>
        <false-positives>
            <issue>
                <type>5244416</type>
                <path>.*</path>
            </issue>
            <issue>
                <type>5247488</type>
                <path>.*bower_components.*</path>
            </issue>
        </false-positives>
    </scope>
</config>
```

2.  按照[用法](https://github.com/NetsOSS/headless-burp#usage-1)部分所示运行

#### 场景 D:扫描不仅仅是 GET 请求。使用从运行功能测试中获得的数据作为扫描的输入

有时，仅仅搜索一个目标范围并在一个 URL 范围内执行并没有太大的价值。例如，当扫描使用 JavaScript 处理路由的 web 应用程序时。如果 Burp 扫描可以扫描更多“真实世界”的请求和响应，它可以发现更多。这样，它可以更有效地攻击目标 URL，并有可能发现比黑暗中的*射击*蜘蛛+扫描方法更多的东西。

要处理这种情况，最好让 burp 代理拦截一些到目标的真实流量，并为自己构建一个站点地图。 [Headless Burp Proxy](https://github.com/NetsOSS/headless-burp#headless-burp-proxy) 扩展提供了一种简单的方法来实现这一点。

1.  遵循[无头打嗝代理](https://github.com/NetsOSS/headless-burp#headless-burp-proxy)的指示，启动打嗝代理，并记住设置`--project-file`选项。这是存储用于扫描的“种子”数据的地方。
2.  通过设置 HTTP_PROXY 或类似的东西，配置您的功能/集成测试来通过 burp 代理(如果您使用扩展，默认为`4646`)。
3.  针对目标运行功能/集成测试。
4.  使用目标站点地图(通常是应用程序的基本 URL)、范围、排除、误报等创建一个 config.xml。

```
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://nets.eu/burp/config">
    <reportType>HTML</reportType>
    <targetSitemap><![CDATA[http://localhost:5432]]></targetSitemap>
    <scope>
        <url><![CDATA[http://localhost:5432]]></url>
        <exclusions>
            <exclusion><![CDATA[localhost:5432/#/logout]]></exclusion>
        </exclusions>
        <false-positives>
            <issue>
                <type>5244416</type>
                <path>.*</path>
            </issue>
        </false-positives>
    </scope>
</config>
```

5.  按照[用法](https://github.com/NetsOSS/headless-burp#usage-1)部分所示运行，并记住设置`--project-file`选项

### TL**；dr；**

无头打嗝扫描仪插件可以做到这些

*   在 headless 或 GUI 模式下运行 burp 扫描
*   指定目标站点地图并将 URL 添加到 Burp 的目标范围
*   使用任何集成/功能测试生成的“种子”请求/响应数据
*   将问题标记为误报，扫描报告中将不再报告这些问题。
*   搜索目标范围。
*   主动扫描目标范围。
*   生成 JUnit/HTML/XML 格式的扫描报告。
*   关闭打嗝

## **打嗝 Maven 插件**

Maven 插件，允许你在无头模式下运行 Burp Suite 的代理和扫描工具。

该插件本质上是一个包装器，包裹着无头打嗝代理服务器和无头打嗝扫描仪扩展。它提供了使用 [Burp 套件](https://portswigger.net/burp)将安全测试集成到项目构建生命周期的简单方法。

### **完整示例**

```
<build>
    ...
    <plugins>
        ...
        <plugin>
            <groupId>eu.nets.burp</groupId>
            <artifactId>burp-maven-plugin</artifactId>
            <version>master-SNAPSHOT</version>
            <configuration>
                <burpSuite>burp/burpsuite_pro_v1.7.31.jar</burpSuite>
                <burpProjectFile>target/headless-burp-project.burp</burpProjectFile>
                <burpConfig>burp/config.xml</burpConfig>
                <headless>true</headless>
                <promptOnExit>false</promptOnExit>
                <verbose>true</verbose>
                <skip>false</skip>
            </configuration>
            <executions>
                <execution>
                    <id>start-burp-proxy</id>
                    <phase>pre-integration-test</phase>
                    <goals>
                        <goal>start-proxy</goal>
                    </goals>
                </execution>
                <execution>
                    <id>stop-burp-proxy</id>
                    <phase>post-integration-test</phase>
                    <goals>
                        <goal>stop-proxy</goal>
                    </goals>
                </execution>
                <execution>
                    <id>start-burp-scan</id>
                    <phase>verify</phase>
                    <goals>
                        <goal>start-scan</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ...
    </plugins>
    ...
</build>
```

## **无头打嗝代理**

为 Burp 提供了一个扩展，允许您在无头模式下运行、停止和捕获 Burp 代理工具的结果。

### **特性**

*   在提供的端口上启动 burp 代理(默认`4646`)
*   注册一个关闭监听器，并在端口(默认`4444`)上等待一个关闭请求(默认`"SHUTDOWN"`)。
*   收到关闭请求时，保存 burp 项目文件以及所有关于代理请求和响应的信息，并最终关闭 Burp

## **用途**

#### **开始打嗝代理**

**在*nix:**

```
java -Xmx1G -Djava.awt.headless=true \
-classpath headless-burp-proxy-master-SNAPSHOT-jar-with-dependencies.jar:burpsuite_pro_v1.7.31.jar burp.StartBurp \
--project-file=project.burp
```

**在 Cygwin 上:**

```
java -Xmx1G -Djava.awt.headless=true \
-classpath "headless-burp-proxy-master-SNAPSHOT-jar-with-dependencies.jar;burpsuite_pro_v1.7.31.jar" burp.StartBurp \
--project-file=project.burp
```

#### **命令行选项**

```
--project-file=VAL          Open the specified project file; this will be created as a new project if the file does not exist (mandatory)
--proxyPort VAL             Proxy port
--shutdownPort VAL          Shutdown port
--shutdownKey VAL           Shutdown key
-p (--prompt)               Indicates whether to prompt the user to confirm the shutdown (useful for debugging)
-v (--verbose)              Enable verbose output

--diagnostics               Print diagnostic information
--use-defaults              Start with default settings
--collaborator-server       Run in Collaborator server mode
--collaborator-config=VAL   Specify Collaborator server configuration file; defaults to collaborator.config
--config-file=VAL           Load the specified project configuration file(s); this option may be repeated to load multiple files
--user-config-file=VAL      Load the specified user configuration file(s); this option may be repeated to load multiple files
--auto-repair               Automatically repair a corrupted project file specified by the --project-file option
```

#### **停止打嗝代理**

```
echo SHUTDOWN >> /dev/tcp/127.0.0.1/4444
or
echo SHUTDOWN | netcat 127.0.0.1 4444
or
echo SHUTDOWN | ncat 127.0.0.1 4444
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/NetsOSS/headless-burp)