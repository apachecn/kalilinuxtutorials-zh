# Androwarn:针对恶意 Android 应用程序的静态代码分析器

> 原文：<https://kalilinuxtutorials.com/androwarn-static-code-analyzer/>

Androwarn 是一个工具，其主要目的是检测并警告用户 Android 应用程序开发的潜在恶意行为。

检测是通过对应用程序的 Dalvik 字节码(表示为 Smali)的静态分析来执行的，使用的是 [`**androguard**`](https://github.com/androguard/androguard) 库。

该分析导致根据用户选择的技术细节级别生成报告。

**特性**

*   针对不同恶意行为类别的字节码的结构和数据流分析
    *   **电话标识符泄露** : IMEI、IMSI、MCC、MNC、LAC、CID、运营商名称…
    *   **设备设置泄露**:软件版本、使用统计、系统设置、日志…
    *   **地理定位信息泄露** : GPS/WiFi 地理定位…
    *   **连接接口信息泄露** : WiFi 凭证，蓝牙 MAC 地址…
    *   **电话服务滥用**:高级短信发送、电话呼叫合成…
    *   **音频/视频流拦截**:通话录音、视频捕捉……
    *   **远程连接建立** : socket 开呼，蓝牙配对，APN 设置编辑…
    *   **PIM 数据泄露**:联系人、日历、短信、邮件、剪贴板……
    *   **外部存储器操作**:sd 卡上的文件访问…
    *   **PIM 数据修改**:添加/删除联系人、日历事件…
    *   **任意代码执行**:使用 JNI 的本机代码、UNIX 命令、权限提升…
    *   **拒绝服务**:事件通知停用、文件删除、进程终止、虚拟键盘禁用、终端关机/重启……
*   根据几个详细级别生成报告
    *   新手必备(`**-v 1**`)
    *   高级(`**-v 2**`)
    *   专家(`**-v 3**`)
*   根据多种格式生成报告
    *   明文`**txt**`
    *   从引导模板格式化的`html`
    *   JSON

**也可阅读-[Lynis:Unix/Linux 系统的安全审计工具](https://kalilinuxtutorials.com/lynis-security-auditing-tool/)**

**用途**

**选项**

用法:andro warn[-h]-I INPUT[-o OUTPUT][-v { 1，2，3}] [-r {txt，html，json}]
[-d]
[-L {debug，info，warn，error，critical，debug，INFO，WARN，ERROR，CRITICAL}]
[-w]
版本:1.4
可选参数:
-h，–帮助显示此帮助信息并退出
-i 输入，–输入输入
APK 文件/_.")-v {1，2，3}，–verbose { 1，2，3}
详细级别(基本 1、高级 2、专家 3)
(默认 1)
-r {txt，html，json}，–Report { txt，html，json}
报告类型(默认“html”)
-d，–Display-向 stdout -L 报告显示分析结果{调试、信息、警告、错误、关键、调试、信息、警告、错误、关键}

**常用用法**

**$ python Android warn . py-I my _ application _ to _ be _ analyzed . apk-r html-v 3**

默认情况下，报告在当前文件夹中生成。HTML 报告现在包含在一个独立的文件中，CSS/JS 资源被内联。

**样本应用**

已经构建了一个示例应用程序，集中了几种恶意行为。

APK 在`**_SampleApplication/bin/**`文件夹中可用，HTML 报告在`**_SampleReports**`文件夹中可用。

**依赖和安装**

*   python 2.7+andro guard+jinja 2+play _ scraper+arg parse
*   **最简单的方法**设置一切:`**pip install androwarn**`然后直接使用`**$ androwarn**`
*   或者 git 克隆存储库并`**pip install -r requirements.txt**`

**变更日志**

*   **版本 1.5—**2019/01/05:少量修复
*   **版本 1.4—**2019/01/04:代码清理和使用最新的雄激素版本
*   **版本 1.3—**2018/12/30:少量修复
*   **版本 1.2—**2018/12/30:少量修复
*   **版本 1.1—**2018/12/29:修复几个 bug，移除 Chilkat 依赖和 pip 打包
*   **版本 1.0—**从 2012 年到 2013 年

[**Download**](https://github.com/maaaaz/androwarn)