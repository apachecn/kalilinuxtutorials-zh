# 路径审计器:检测不安全的路径访问模式

> 原文：<https://kalilinuxtutorials.com/path-auditor-detecting-unsafe-path-access-patterns/>

路径审计器是一个通过审计 libc 函数来发现文件访问相关漏洞的工具。

**路径审计师**的思路大致如下:

*   审核二进制文件执行的对文件系统相关的 libc 函数的每个调用。
*   检查 syscall 中使用的路径是否是用户可写的。在这种情况下，非特权用户可以用符号链接替换目录或文件。
*   将所有违规记录为潜在漏洞。

我们使用 LD_PRELOAD 来挂钩所有与文件系统相关的库调用，并将遇到的任何违规记录到 syslog 中。

这不是官方支持的谷歌产品。

**又读-[node crypto:用 NodeJs](https://kalilinuxtutorials.com/nodecrypto-ransomware-written-nodejs/) 写的 Linux 勒索软件 **

**漏洞示例**

让我们来看一个该工具可以检测的漏洞类型的示例。 [CVE-2019-3461](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-3461) 是 tmpreaper 中的一个 bug，这是一个遍历/tmp 并删除旧文件的工具。它通常以 root 用户身份作为 cron 作业运行。因为它不想删除 tmp 之外的文件，所以它使用下面的代码来检查一个目录是否是一个挂载点:

**if(S _ ISDIR(sb . ST _ mode)){
char * dst；
if((dst = malloc(strlen(ent->d _ name)+3))= = NULL)
message(LOG _ FATAL，“malloc 失败。\ n ")；
strcpy(dst，ent->d _ name)；
strcat(dst，"/X ")；
重命名(ent- > d_name，dst)；
if(errno = = ex dev){
free(dst)；
消息(LOG_VERBOSE，
"跳过不同设备上的文件:` %s/%s'\n "，
dirname，ent->d _ name)；
继续；
}
// […]**

简而言之，这段代码调用`**rename("/tmp/foo", "/tmp/foo/x")**`，如果`**"/tmp/foo"**`是一个挂载点，它将返回`EXDEV`。如果`**"/tmp/foo"**`由除 root 之外的任何用户拥有，PathAuditor 会将此调用标记为潜在漏洞。为了理解其中的原因，我们必须考虑在执行 rename syscall(简化)时内核中会发生什么:

*   内核遍历路径`**"/tmp/foo"**`寻找第一个参数。
*   内核遍历路径`**"/tmp/foo/x"**`寻找第二个参数。
*   如果源和目标在不同的文件系统上，则返回 EXDEV。
*   否则，将文件从第一个目录移动到第二个目录。

这里有一个竞争条件，因为`**"/tmp/foo"**`将被解析两次。如果是用户控制的，用户可以在任何时候用不同的文件替换它。特别是，我们希望 **`"/tmp/foo"`** 首先成为一个目录，以通过 tmpreaper 代码中的`**if(S_ISDIR)**`检查。然后，在代码进入系统调用之前，我们用一个文件替换它。当内核解析第一个参数时，它将看到一个包含用户控制内容的文件。现在我们再次替换它，这次用一个符号链接到同一个文件系统上的任意目录。内核将第二次解析路径，跟随符号链接并将受控文件移动到选定的目录。

相同的文件系统限制是因为重命名在文件系统之间不起作用。但是在某些 Linux 发行版中，默认情况下/tmp 只是 rootfs 上的一个文件夹，您可以利用这个 bug 将一个文件移动到/etc/cron，它将作为 root 执行。

**怎么跑？**

为了进行试验，您需要使用 [bazel](https://bazel.build) 构建 libpath_auditor.so，并使用 LD_PRELOAD 将其加载到二进制文件中。任何违规都将被记录到系统日志中，因此请确保系统正在运行。

> >**bazel build//pat auditor/libc:libpath _ auditor . so** >>LD _ PRELOAD =/path/to/bazel-bin/path auditor/libc/libpath _ auditor . so cat/tmp/foo/bar
>>tail/var/log/syslog

通过将它添加到/etc/ld.so.preload，也可以在系统上的所有进程上运行它。不过要注意的是，这仅建议在测试系统上运行，因为它会导致不稳定。

作为快速入门，您可以尝试这个项目附带的 docker 容器:

docker build-t path auditor-示例。
docker run-it path auditor-example
# LD _ PRELOAD =/path auditor/bazel-bin/path auditor/libc/libpath _ auditor . so cat/tmp/foo/bar
# cat/var/log/syslog

[**Download**](https://github.com/google/path-auditor)