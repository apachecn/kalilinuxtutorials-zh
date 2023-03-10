# xeno scan——用 C++编写的开源内存扫描仪

> 原文：<https://kalilinuxtutorials.com/xenoscan-memory-scanner/>

**XenoScan** 是一个内存扫描器，可以用来扫描进程的内存，定位重要值的具体位置。这些类型的工具通常在入侵视频游戏时使用，因为它们允许用户在内存中定位代表游戏状态的值。

XenoScan 是用 C++编写的，有一个 Lua 前端，我一直致力于开发比我见过的任何其他内存扫描器都更高级的功能。值得注意的是，它有办法枚举并返回目标内存空间中所有复杂的数据结构(比如 std::list 和 std::map ),它甚至可以扫描任何类实例，并将发现的实例按其底层类型分组。

**也读作[dbg shell——Windows 调试器引擎的 PowerShell 前端](https://kalilinuxtutorials.com/dbgshell/)**

## **XenoScan 子项目**

### **XenoLua**

XenoLua 是 Lua 的包装器，提供了大量的功能。最值得注意的是，它提供了一个`LuaVariant`类，该类封装了在`C` / `C++`和`Lua`类型之间进行转换的功能。此外，它在`LuaPrimitive`类中有帮助函数用于处理 Lua。

### **XenoScanEngine**

XenoScanEngine 是该项目的核心。它包含用于扫描、数据结构检测和其他一切的代码。

### **XenoScanLua**

XenoScanLua 将 XenoScanEngine 与 XenoLua 联系起来，为扫描器提供一个 Lua 可脚本化的前端。目前，这是扫描仪的唯一入口。

此外，这个项目包含一些测试代码，确保一切正常工作。一个测试是一个 **`.cpp`** 、一个 `**.h**` 和一个`.lua`文件的组合。关于如何使用扫描仪的示例，您可以查看`.lua`测试文件。

## **编译**

*XenoScan* 使用 *CMake* ，已经过 Visual Studio 2017 测试。理论上，只要使用 CMake 生成项目文件，您应该能够使用任何现代编译器来构建代码。在编译之前，您需要确保已经签出了子模块。一旦完成，你还必须构建 *luajit* 子模块，以便 *XenoScan* 可以链接库。

如果您使用的是 Visual Studio，这应该很容易。只需在 VS 的*开发者命令提示符下运行`buildmsvc2017.bat`。作为一个例子，为 *Visual Studio 2017* 构建一个项目，我运行*

```
cd C:\path\to\XenoScan
buildmsvc2017.bat
```

这将使一个名为 `XenoScan.sln` 的文件出现在我的`build`目录中(例如`C:\path\to\XenoScan\build`)。

XenoScan 的主要开发是在这个版本的 Visual Studio 上完成的。

## **平台**

代码被设计成平台无关的。理论上，要在任何其他平台上编译，您需要

1.  为目标 IDE/编译器创建项目/make 文件。
2.  从项目中删除`ScannerTargetWindows.cpp`和 `ScannerTargetWindows.h` 文件。
3.  为您的平台实现`ScannerTarget`接口。
4.  将您的实现添加到项目中。
5.  ？？？？*利润*

## **特性**

**基本扫描功能支持以下类型:**

*   整数类型*:
    *   `int8_t`
    *   `uint8_t`
    *   `int16_t`
    *   `uint16_t`
    *   `int32_t`
    *   `uint32_t`
    *   `int64_t`
    *   `uint64_t`
*   `float`
*   `double`
*   ascii 字符串
*   宽弦
*   自定义数据结构(想想`C++` `struct`)
    *   可以由整数和小数类型的任意组合组成

[* *Lua 前端可能会卡在 64 位整数上，但是扫描仪库支持。*]

**扫描支持以下类型的匹配:**

*   等于
*   大于
*   大于或等于
*   不到
*   小于或等于
*   范围(`min <= check <= max`)

**此外，还有检测以下类型的所有实例的功能:**

*   `std::map`
*   `std::list`
*   任何有虚函数表的类

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/nickcano/XenoScan) **信用:黑客**