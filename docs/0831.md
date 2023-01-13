# PHP stan——PHP 静态分析工具——不用运行就能发现代码中的错误

> 原文：<https://kalilinuxtutorials.com/phpstan-php-static-analysis-tool/>

[![PHPStan – PHP Static Analysis Tool – Discover Bugs In Your Code Without Running It](img/f2839ef3a890efbf2576088e4324452c.png "PHPStan – PHP Static Analysis Tool – Discover Bugs In Your Code Without Running It")](https://1.bp.blogspot.com/-Qtbf8fDwyR8/XWYGi04HmxI/AAAAAAAACPo/sC6QyPiTk4wYnuN5jGHiERdZkU6QBu5rACLcBGAs/s1600/phpstan_1%2B%25281%2529.png)

PHPStan 专注于在不实际运行代码的情况下发现代码中的错误。甚至在你为代码编写测试之前，它就能捕捉到所有类型的错误。它使 PHP 更接近于编译语言，因为在运行实际代码行之前，可以检查每一行代码的正确性。

**先决条件**

PHPStan 要求 PHP >= 7.1。你必须在 PHP 7.x 的环境中运行它，但是实际的代码不需要使用 PHP 7.x 的特性。(为 PHP 5.6 和更早版本编写的代码可以在 7.x 上运行，无需修改。)

PHPStan 最适合现代面向对象代码。代码的类型越强，提供给 PHPStan 的信息就越多。

正确注释和类型提示的代码(类属性、函数和方法参数、返回类型)不仅有助于静态分析工具，也有助于使用代码的其他人理解代码。

**安装**

要开始对代码执行分析，需要在 [Composer](https://getcomposer.org/) 中使用 PHPStan:

composer require–dev phps tan/phps tan

Composer 将 PHPStan 的可执行文件安装在它的`**bin-dir**`中，默认为`**vendor/bin**`。

如果您有相互冲突的依赖关系，或者您想全局安装 PHPStan，最好的方法是通过 PHAR 归档。你可以在[发布说明](https://github.com/phpstan/phpstan/releases)下面找到最新的稳定 PHAR 档案。您还可以使用 [phpstan/phpstan-shim](https://packagist.org/packages/phpstan/phpstan-shim) 包通过 Composer 安装 phpstan，而不会有依赖冲突的风险。

也可以通过 Docker 使用 [PHPStan。](https://github.com/phpstan/docker-image)

**第一次跑**

要让 PHPStan 分析您的代码库，您必须使用`analyse`命令并将其指向正确的目录。

因此，例如，如果您在目录`src`和`tests`中有您的类，您可以像这样运行 PHPStan:

**供应商/bin/phpstan 分析 src 测试**

PHPStan 可能会发现一些错误，但是不要担心，您的代码可能会很好。第一次运行时发现的错误往往是:

*   传递给函数的额外参数(例如，函数需要两个参数，代码传递三个)
*   传递给 print/sprintf 函数的额外参数(例如，格式字符串包含一个占位符，代码传递两个值来替换)
*   死代码中的明显错误
*   需要定义的神奇行为。见[扩展性](https://github.com/phpstan/phpstan#extensibility)。

在修复了代码中的明显错误之后，请查看下一节中的所有配置选项，这些选项将使报告的错误数为零，从而使 PHPStan 适合作为持续集成脚本的一部分运行。

**也可理解为-[子许可:安全&侦察工具，利用证书透明性](https://kalilinuxtutorials.com/sublert-security-certificate-transparency/)**

**规则等级**

如果您想使用 PHPStan，但是您的代码库跟不上强类型和 PHPStan 的严格检查，您可以通过将`**--level**`传递给`**analyse**`命令，从当前的 8 个级别中进行选择(0 是最宽松的，7 是最严格的)。默认级别是`**0**`。

这个特性支持 PHPStan 检查的增量采用。您可以从较低的规则级别开始使用 PHPStan，并在喜欢的时候增加规则级别。

也可以用`**--level max**`作为最高级的别名。这将确保在升级到新版本的 PHPStan 时，您将始终使用最高级别。请注意，这可能会在升级到新版本时造成重大障碍，因为您可能需要修复大量代码才能将错误数量降至零。

**配置**

配置文件通过`-c`选项传递给`phpstan`可执行文件:

供应商/bin/phpstan 分析-l 4 -c phpstan.neon src 测试

使用自定义项目配置文件时，必须将`**--level**` **(** `**-l**` **)** 选项传递给`**analyse**` 命令(此处默认值不适用)。

如果没有明确提供配置文件，PHPStan 将在当前目录中查找名为`phpstan.neon`或`phpstan.neon.dist`的文件。

解决方案优先级如下:

1.  如果命令行上提供了配置文件，则使用该文件。
2.  如果配置文件`phpstan.neon`存在于当前目录中，它将被使用。
3.  如果配置文件`phpstan.neon.dist`存在于当前目录中，它将被使用。
4.  如果以上都不成立，将不使用任何配置。

[霓虹灯文件格式](https://ne-on.org/)与 YAML 非常相似。以下所有选项都是`parameters`部分的一部分。

**配置变量**

*   `**%rootDir%**`–PHPStan 所在的根目录(即 Composer 安装中的`**vendor/phpstan/phpstan**`)
*   `**%currentWorkingDirectory%**`–执行 PHPStan 的当前工作目录

#### 配置选项

*   `**tmpDir**`**–指定 PHPStan 缓存使用的临时目录(默认为`**sys_get_temp_dir() . '/phpstan'**`)**
*   **`**level**`–指定分析级别–如果指定，则不需要`**-l**`选项**
*   **`**paths**`**–指定分析的路径–如果指定，路径不需要作为参数传递****

 ******自动加载**

PHPStan 使用 Composer autoloader，因此自动加载类的最简单方法是通过 composer.json 中的`**autoload**` **/** `**autoload-dev**`部分

**指定扫描路径**

如果 PHPStan 抱怨一些不存在的类，并且您确定这些类存在于代码库中，并且出于某种原因您不想使用 Composer autoloader，您可以使用`**autoload_directories**`和`**autoload_files**` **和**数组参数指定要扫描的目录和要包含的具体文件:

**参数:
自动加载目录:
–% rootDir %/../../../build
autoload _ files:
–% rootDir %/../../../generated/routes/generated route list . PHP**

`**%rootDir%**`展开到 PHPStan 所在的根目录。

**全球安装自动加载**

PHPStan 支持使用 [`**composer global**`](https://getcomposer.org/doc/03-cli.md#global) 或通过 [PHAR 档案](https://github.com/phpstan/phpstan#installation)进行全球安装。在这种情况下，它不是项目自动加载程序的一部分，但它支持从驻留在`vendor/`中的当前工作目录自动发现 Composer 自动加载程序:

CD/path/to/project
PHP stan analyse src tests #在/path/to/project/vendor/autoload . PHP 中查找自动加载程序

如果您将依赖项安装在不同的路径中，或者您从不同的目录运行 PHPStan，那么您可以使用`**--autoload-file|-a**`选项指定自动加载程序的路径:

**phpstan 分析–autoload-file =/path/to/autoload . PHP src 测试**

**从分析中排除文件**

如果你的代码库包含一些被故意破坏的文件(例如，为了测试你的应用程序在含有无效 PHP 代码的文件上的行为)，你可以使用`**excludes_analyse**`数组参数排除它们。每行的字符串用作 [`**fnmatch**`](https://secure.php.net/manual/en/function.fnmatch.php) 函数的模式。

参数:
excludes _ analyse:
–% root dir %/../../../tests/ */data/*

**包含自定义扩展**

如果您的代码库包含扩展名不是标准的 php 文件。php 扩展名，然后可以将它们添加到`**fileExtensions**`数组参数中:

参数:
文件扩展名:
–PHP
–模块
–Inc

**万能物品箱**

没有预定义结构的类在 PHP 应用程序中很常见。它们被用作数据的通用持有者——可以在它们上面设置和读取任何属性。值得注意的例子包括`**stdClass**` **、** `**SimpleXMLElement**`(这些是默认启用的)、带有数据库查询结果的对象等。使用`**universalObjectCratesClasses**`数组参数让 PHPStan 知道在您的代码库中使用了哪些具有这些特征的类:

参数:
通用对象创建类:
–迪比\ Row
–棘轮\连接接口

**将非显式赋值变量添加到作用域**

如果您在 catch 块中使用 try 块中的一些变量，请将`**polluteCatchScopeWithTryAssignments**`布尔参数设置为`**true**`。

try {
$ author = $ this->getLoggedInUser()；
$ post = $ this->post repository->get byid($ id)；
} catch(PostNotFoundException $ e){
//$ author 大概就是在这里定义的
throw new article by authorcannot published($ author)；
}

如果您正在枚举 if-elseif 分支中所有可能的情况，并且 PHPStan 在条件后报错未定义的变量，您可以编写一个 else 分支，并抛出一个异常:

if(something is true()){
$ foo = true；
} else if(orsomethingelistrue()){
$ foo = false；
} else {
抛出新的 shoutnothapenexception()；
}
doFoo($ foo)；

我建议将`**polluteCatchScopeWithTryAssignments**`设置为`**false**`,因为这样可以得到更清晰、更易维护的代码。

**自定义提前终止方法调用**

前面的例子表明，如果条件分支以抛出异常结束，则该分支不必定义在条件分支结束后使用的变量。

但是异常并不是提前终止方法执行的唯一方式。一些特定的方法调用也可能被项目开发人员视为提前终止——比如通过抛出内部异常来停止执行的`**redirect()**`。

if(something is true()){
$ foo = true；
} else if(orsomethingelistrue()){
$ foo = false；
} else {
$this- >重定向('主页')；
}
doFoo($ foo)；

可以通过指定一个类来配置这些方法，在该类的实例上调用这些方法，如下所示:

参数:
early terminating method calls:
Nette \ Application \ UI \ Presenter:
–redirect
–redirect URL
–send JSON
–send response

**用正则表达式忽略错误消息**

如果代码库中的某个问题不容易修复，或者只是想以后再处理，那么您可以使用正则表达式从分析结果中排除错误消息:

参数:
ignore errors:
–' #调用未定义的方法[a-zA-Z0-9 \ _]+::method()# '
–' #调用未定义的方法[a-zA-Z0-9 \ _]+::expects()# '
–' #访问未定义的属性 PHPUnit _ Framework _ mock object _ mock object::\ $[a-zA-Z0-9 _]+# '
–' #调用未定义的方法 PHPUnit _ Framework _ mock object _ mock object

要排除特定目录或文件中的错误，请指定一个`path`或`paths`以及`**message**`:

参数:
ignore errors:
–
消息:' #调用未定义的方法[a-zA-Z0-9\_]+::method()#'
路径:% currentWorkingDirectory %/some/dir/some file . PHP
–
消息:' #调用未定义的方法[a-zA-Z0-9\_]+::method()#'
路径:
–% currentWorkingDirectory %/some/dir/*
–% currentWorkingDirectory %/t

如果某些模式不再出现在结果中，PHPStan 会通知您，您必须从配置中删除这些模式。您可以通过在 PHPStan 配置中将`**reportUnmatchedIgnoredErrors**`设置为`**false**` 来关闭此行为。

**自举文件**

如果您需要在 PHPStan 运行之前在 PHP 运行时初始化某些东西(比如您自己的自动加载器)，您可以提供自己的引导文件:

参数:
bootstrap: %rootDir%/../../../phpstan-bootstrap.php

**自定义规则**

PHPStan 允许编写自定义规则来检查您自己的代码库中的特定情况。您的规则类需要实现`**PHPStan\Rules\Rule**`接口，并在配置文件中注册为服务:

服务:
–
类:MyApp \ PHP stan \ Rules \ DefaultValueTypesAssignedToPropertiesRule
标签:
–PHP stan . Rules . rule

*   要获得如何实现规则的灵感，请转到 [src/Rules](https://github.com/phpstan/phpstan/tree/master/src/Rules) 查看大量内置规则。
*   还可以查看 [phpstan-strict-rules](https://github.com/phpstan/phpstan-strict-rules) 存储库，了解针对 phpstan 的额外严格和固执己见的规则！
*   还要检查[PHP stan-deprecation-rules](https://github.com/phpstan/phpstan-deprecation-rules)中检测不赞成使用的类、方法、属性、常量和特征的规则！

**自定义错误格式化程序**

PHPStan 通过格式化程序输出错误。您可以通过在新类中实现`**ErrorFormatter**`接口来定制输出，并将其添加到配置中。有关现有的格式化程序，请参见下一章。

接口错误格式化程序
{
/**
*格式化错误并输出到控制台。
*
* @ param \ PHP stan \ Command \ analysis result $ analysis result
* @ param \ Symfony \ Component \ Console \ Style \ output Style $ Style
* @ return int 错误代码。
*/
公共函数 format errors(
analysis result $ analysis result，
\ Symfony \ Component \ Console \ Style \ output Style $ Style
):int；
}

在您的`**phpstan.neon**`中注册格式化程序:

services:
error formatter . awesome:
class:App \ PHP stan \ awesome error formatter

使用`**errorFormatter.**`后的名称部分作为 CLI 选项值:

vendor/bin/phps tan analyse-c phps tan . neon-l 4–错误格式 awesome src 测试

**要使用的现有错误格式器**

您可以将以下关键字传递给`**--error-format=X**`参数，以影响输出:

*   `**table**`:默认。按文件分组的错误，彩色的。供人食用。
*   `**raw**`:每行包含一个错误，带有文件路径、行号和错误描述
*   `**checkstyle**`:创建 checkstyle.xml 兼容输出。请注意，您必须将输出重定向到一个文件中，以便捕获结果供以后处理。
*   `**json**`:创建缩小的。不带空格的 json 输出。请注意，您必须将输出重定向到一个文件中，以便捕获结果供以后处理。
*   `**prettyJson**`:创造人类可读的。带有空白和缩进的 json 输出。请注意，您必须将输出重定向到一个文件中，以便捕获结果供以后处理。

**类反射扩展**

PHP 中的类可以使用类似于`**__get**` **、** `**__set**`和`**__call**`的类方法来公开在运行时决定的“神奇”属性和方法。因为 PHPStan 完全是关于静态分析的(在不运行代码的情况下测试代码的错误)，所以它必须事先知道那些属性和方法。

当 PHPStan 偶然发现内置类反射未知的属性或方法时，它会遍历所有已注册的类反射扩展，直到找到定义该属性或方法的扩展。

由于循环引用问题，类反射扩展不能在构造函数中注入`**PHPStan\Broker\Broker**`(用于获取类反射的服务)，但是扩展可以通过 setter 实现`**PHPStan\Reflection\BrokerAwareExtension**`接口来获取 Broker。

**属性类反射扩展**

此扩展类型必须实现以下接口:

命名空间 PHPStan \ Reflection
接口属性 classreflectionextension
{
公共函数 has property(class reflection $ class reflection，string $ property name):bool；
公共函数 getProperty(class reflection $ class reflection，string $ property name):property reflection；
}

很可能你还必须实现一个新的`**PropertyReflection**`类:

命名空间 PHPStan \ Reflection
接口属性反射
{
公共函数 getType():Type；
公共函数 getDeclaringClass():class reflection；
公共函数 is static():bool；
公共函数 is private():bool；
公共函数 is public():bool；
}

这是在项目的 PHPStan 配置文件中注册扩展的方法:

服务:
类:App \ PHP stan \ propertiesfromannotationclassreflectionextension 标签:
PHP stan . broker . propertiescsreflectionextension

**方法类反射扩展**

此扩展类型必须实现以下接口:

命名空间 PHPStan \ Reflection
接口 MethodsClassReflectionExtension
{
公共函数 has method(class reflection $ class reflection，string $ method name):bool；
公共函数 get method(class reflection $ class reflection，string $ method name):method reflection；
}

很可能你还必须实现一个新的`**MethodReflection**`类:

命名空间 PHPStan \ Reflection
接口方法 Reflection
{
公共函数 getDeclaringClass():class reflection；
公共函数 get prototype():self；
公共函数 is static():bool；
公共函数 is private():bool；
公共函数 is public():bool；
公共函数 getName():string；
/* *
* @ return \ PHP stan \ Reflection \ parameter Reflection[]
*/
公共函数 get parameters():array；
公共函数 is variadic():bool；
公共函数 get returntype():Type；
}

这是在项目的 PHPStan 配置文件中注册扩展的方法:

服务:
–
类:App \ PHPStan \ EnumMethodsClassReflectionExtension
标签:
–PHPStan . broker . methodsclassreflectionextension

**动态返回型扩展**

如果方法的返回类型不总是相同的，而是依赖于传递给该方法的参数，则可以通过编写和注册扩展来指定返回类型。

因为您必须编写带有类型解析逻辑的代码，所以它可以像您希望的那样复杂。

编写完示例扩展后，变量`**$mergedArticle**`将具有正确的类型:

$ merge Dar ticle = $ this-> entityManager-> merge($ article)；
// $mergedArticle 将与$article 具有相同的类型

这是动态返回类型扩展的接口:

命名空间 PHPStan \ Type
使用 PhpParser \ Node \ Expr \ method call；
使用 PHPStan \ Analyser \ Scope
使用 PHPStan \ Reflection \ method Reflection；
接口 dynamicmethodreturntype extension
{
公共函数 getClass():string；
公共函数 isMethodSupported(method reflection $ method reflection):bool；
公共函数 getTypeFromMethodCall(method reflection $ method reflection，MethodCall $methodCall，Scope $ Scope):Type；
}

这就是如何编写正确解析 EntityManager::merge()返回类型的扩展:

公共函数 getClass():string
{
return \ Doctrine \ ORM \ EntityManager::class；
}
公共函数 isMethodSupported(method reflection $ method reflection):bool
{
return $ method reflection->getName()= = = ' merge '；
}
公共函数 getTypeFromMethodCall(method Reflection $ method Reflection，MethodCall $methodCall，Scope $ Scope):Type
{
if(count($ method call->args)= = = 0){
return \ PHP stan \ Reflection \ parameters sacceptor selector::selectFromArgs(
$ Scope，
$methodCall- > args，
$ method Reflection->get variants()
)--
}
$ arg = $ method call->args[0]->值；
返回$ scope->getType($ arg)；
}

最后，在项目的配置文件中注册 PHPStan 的扩展:

服务:
–
类:App \ PHP stan \ EntityManagerDynamicReturnTypeExtension
标签:
–PHP stan . broker . dynamicmethodreturntypeextension

还有一个类似的功能:

*   **静态方法**使用`**DynamicStaticMethodReturnTypeExtension**`接口和`**phpstan.broker.dynamicStaticMethodReturnTypeExtension**`服务标签。
*   使用`**DynamicFunctionReturnTypeExtension**`接口和`**phpstan.broker.dynamicFunctionReturnTypeExtension**`服务标签的**功能**。

**类型指定扩展**

这些扩展允许您基于某些预先存在的条件指定表达式的类型。有几个例子可以很好地说明这一点:

if (is_int($variable)) {
//这里我们可以确定$variable 是整数
}
//使用 PHPUnit 的 asserts
self::assertNotNull($ variable)；
//在这里我们可以确定 variable 不为空

由于循环引用问题，类型指定扩展不能在构造函数中注入`**PHPStan\Analyser\TypeSpecifier**`,但是扩展可以实现`**PHPStan\Analyser\TypeSpecifierAwareExtensio**n`接口以通过 setter 获得 TypeSpecifier。

这是指定类型扩展的接口:

命名空间 PHPStan \ Type
使用 PhpParser \ Node \ Expr \ static call；
使用 PHPStan \ Analyser \ Scope
使用 PHP stan \ Analyser \ specified types；
使用 PHPStan \ Analyser \ TypeSpecifierContext；
使用 PHPStan \ Reflection \ method Reflection；
接口 staticmethodtypespecificingextension
{
公共函数 getClass():string；
公共函数 isStaticMethodSupported(method reflection $ static method reflection，StaticCall $node，TypeSpecifierContext $ context):bool；
公共函数 specify types(method reflection＄static method reflection，static call＄node，Scope＄Scope，TypeSpecifierContext＄context):specified types；
}

这就是为上面的第二个例子编写扩展的方式:

公共函数 getClass():string
{
return \ PHPUnit \ Framework \ Assert::class；
}
公共函数 isStaticMethodSupported(method reflection $ static method reflection，StaticCall $node，TypeSpecifierContext $ context):bool；
{
//这个$context 参数告诉我们是否处于 if 条件中(就像这个例子)。
return $ static method reflection->getName()= = = ' assertNotNull '&&$ context->null()；
}
公共函数 specify types(method reflection $ static method reflection，StaticCall $node，Scope $scope，TypeSpecifierContext $ context):specifiertypes
{
//假设扩展实现\ PHP stan \ Analyser \ TypeSpecifierAwareExtension。
return $ this->Type specifier->create($ node->var，\ PHP stan \ Type \ Type combinator::remove null($ scope->getType($ node->var)，$ context)；
}

最后，在项目的配置文件中注册 PHPStan 的扩展:

服务:
–
类:App \ PHP stan \ assertnotnulltypespecificyingextension
标签:
–PHP stan . type specifier . staticmethodtypescificyingextension

还有一个类似的功能:

*   **使用`**MethodTypeSpecifyingExtension**`接口和`**phpstan.typeSpecifier.methodTypeSpecifyingExtension**`服务标签的动态方法**。
*   使用`**FunctionTypeSpecifyingExtension**`接口和`**phpstan.typeSpecifier.functionTypeSpecifyingExtension**`服务标签的**功能**。

[**Download**](https://github.com/phpstan/phpstan)****