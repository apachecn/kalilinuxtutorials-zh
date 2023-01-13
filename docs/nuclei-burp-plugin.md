# nucleus-Burp-Plugin:Burp suite 的 nucleus 插件

> 原文：<https://kalilinuxtutorials.com/nuclei-burp-plugin/>

[![](img/28df0ec4bfd7bf713fb7e0dff732bfda.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9cGfJKQxT6bPImze3z_Aw8YFzC9Hd7tAM9lktgVfDKmlVEdJOPnaLk4O2AYCA5g765cVRZB2Oo0_q9aHvdY6Pq7TBfl-GzrD5uKtgUBircG5EDvD3pkmdL-1dDRNfzAbY-2Dhd9PMLf85nt2XkeD2IA30e69aYG73RPlnxT7bj90rwBWNYTK3Av6B/s728/download%20(1).png)

**nucleus-Burp-Plugin**是一个用于帮助`**nuclei**`模板生成的`**BurpSuite**`插件。

## 特征

### 模板匹配器生成

*   使用从`**Proxy**`历史或`**Repeater**`上下文中选择的响应片段创建`**Word**`和`**Binary**`匹配器
*   多行选择被拆分成单独的单词以提高可读性
*   为包含非`**ASCII**`字符的选择创建二元匹配器
*   `**part**`字段是根据选择是在请求头中还是在请求体中自动设置的
*   每个生成的模板都自动包含一个状态匹配器，使用响应的`**HTTP**`状态代码

### 请求模板生成

*   在`**Intruder**`选项卡中，选择的有效载荷位置可用于生成请求模板，使用以下攻击类型之一:`**Battering ram**`、`**Pitchfork**`或`**Cluster bomb**`
*   从`**Proxy**`或 **`Repeater`** 选项卡下的`**HTTP**`请求中选择的文本片段可用于生成攻击类型默认为`**Battering ram**`的请求模板

### 模板执行

*   生成的模板可以立即执行，为了方便起见，输出显示在同一个窗口中
*   该插件使用从所需请求中提取的绝对 nuclei 路径、绝对模板路径和目标信息，自动生成 CLI 命令
*   存储唯一的已执行命令的历史记录，可以在当前会话中快速搜索和重新执行

### 实验特征

*   (非上下文的)`**YAML**`属性和值**自动完成**，使用来自核 **`JSON`模式**的保留字
*   **语法高亮显示`**YAML**`属性的**，基于保留字

### 生产力

*   几乎每个动作都可以使用键盘快捷键触发:
    *   **F1** :打开细胞核模板文件
    *   **Ctrl + Enter** :执行当前模板
    *   **Ctrl + Shift + E** :跳转到模板编辑器
    *   **Ctrl + L** :跳转到 CLI 输入字段
    *   **Ctrl + R** :显示 CLI 参数助手
    *   **Ctrl + S** :保存当前模板
    *   **Ctrl +加减**:增大/减小字体大小
    *   **Ctrl + Q** :退出
*   标签支持:
    *   **Ctrl + Tab** 或 **Ctrl + PageDown** :打开下一个标签页
    *   **Ctrl + Shift + Tab** 或 **Ctrl + PageUp** :打开上一页
    *   **Ctrl+【1-9】**:移动到第 n 页签
    *   **鼠标在标签上向上/向下滚动**:导航到下一个或上一个标签
    *   **Ctrl + W** 或**鼠标中键点击**:关闭当前页签
*   如果模板保存到新位置，模板路径会自动更新
*   保存时建议使用`**template-id**`作为文件名

### 设置

*   该插件试图自动检测并完成配置值
*   代码使用来自进程的环境变量`**PATH**`的值搜索 nuclei 二进制路径。
    **注意**:与独立的 BurpSuite jar 相反，BurpSuite 二进制文件可能无法访问当前用户的`**PATH**`变量。
*   目标模板路径根据默认的 nuclei 模板目录计算，在`**<USER_HOME>/.config/nuclei/.templates-config.json**`下配置
*   当前登录的操作系统用户的名称用作模板作者配置的默认值

### 外观和感觉

*   模板发生器窗口支持深色和浅色主题。在`**User Options**`下，根据所选的 BurpSuite 主题选择呈现的主题
*   支持**彩色**细胞核输出
*   模板编辑器和命令输出中可修改的字体大小

## 构建代码

使用`**mvn clean package -DskipTests**`自己构建项目。它需要 Maven `**3.x**`和 Java `**11+**`。

在 MacOS 上，插件的依赖关系可以用自制软件来满足:`**brew install mvn openjdk@11**`

或者，可以从 Actions 部分下载不同的构建。构建的工件可以在最新构建的`**Artifacts**`部分找到。这些工件是在每次提交后生成的，但是只存储有限的时间。

## 安装

*   自己构建代码或下载预构建/发布版本
*   转到 BurpSuite 中的`**Extender**`
*   点击`**Extensions**`选项卡中的`**Add**`按钮
*   保持`**Java**`上的`**Extension Type**`
*   选择插件 **( `.jar`** )的路径

[**Download**](https://github.com/projectdiscovery/nuclei-burp-plugin)