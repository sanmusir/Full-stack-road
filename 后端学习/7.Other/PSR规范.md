### 前言
PSR是PHP标准推荐的简称，这个是php-fig组织制定的一套规范。至今，php-fig已经发布了五个规范：

- PSR-0：自动加载标准，2014-10-21该标准已经被废弃，使用PSR-4替代，不再细讲
- PSR-1：基本的编码风格
- PSR-2：编码风格（更严格）
- PSR-3：日志记录器接口
- PSR-4：自动加载

### PSR-1
- PHP 代码文件 必须 以 <?php 或 <?= 标签开始；
- PHP 代码文件 必须 以 不带 BOM 的 UTF-8 编码；
- PHP 代码中 应该 只定义类、函数、常量等声明，或其他会产生 副作用 的操作（如：生成文件输出以及修改 .ini 配置文件等），二者只能选其一；
- 命名空间以及类 必须 符合 PSR 的自动加载规范： [PSR-0（已废弃）或 PSR-4] 中的一个。
- 类的命名 必须 遵循 StudlyCaps 大写开头的驼峰命名规范；
- 类中的常量所有字母都 必须 大写，单词间用下划线分隔；
- 方法名称 必须 符合 camelCase 式的小写开头驼峰命名规范。

### PSR-2

- 代码 必须 遵循 [PSR-1] 中的编码规范 。
- 代码 必须 使用 4 个空格符而不是「Tab 键」进行缩进。
- 所有 PHP 文件 必须 使用 Unix LF (linefeed) 作为行的结束符。
- 所有 PHP 文件 必须 以一个空白行作为结束。
- 纯 PHP 代码文件 必须 省略最后的 ?> 结束标签。
- PHP 的 关键字 必须 使用小写形式。
- 每行的字符数 应该 软性保持在 80 个之内，理论上 一定不可 多于 120 个，但 一定不可 有硬性限制。
- 每个 namespace 命名空间声明语句和 use 声明语句块后面，必须 插入一个空白行。
- 类的开始花括号（{） 必须 写在函数声明后自成一行，结束花括号（}）也 必须 写在函数主体后自成一行。
- 方法的开始花括号（{） 必须 写在函数声明后自成一行，结束花括号（}）也 必须 写在函数主体后自成一行。
- 类的属性和方法 必须 添加访问修饰符（private、protected 以及 public），abstract 以及 final 必须 声明在访问修饰符之前，而 static 必须 声明在访问修饰符之后。
- 控制结构的关键字后 必须 要有一个空格符，而调用方法或函数时则 一定不可 有。
- 控制结构的开始花括号（{） 必须 写在声明的同一行，而结束花括号（}） 必须 写在主体后自成一行。
- 控制结构的开始左括号后和结束右括号前，都 一定不可 有空格符。

示例
```
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleMethod($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // 方法体
    }
}

```

### PSR-3
- 定义日志接口规范

### PSR-4
- 全限定类名必须拥有一个顶级命名空间名称，也称为供应商命名空间（vendor namespace）。
- 全限定类名可以有一个或者多个子命名空间名称。
- 全限定类名必须有一个最终的类名
- 下划线在全限定类名中没有任何特殊含义（在 PSR-0 中下划是有含义的）。
- 全限定类名可以是任意大小写字母的组合。
- 所有类名的引用必须区分大小写。

### composer自动加载
[深入解析 composer 的自动加载原理](https://segmentfault.com/a/1190000014948542)
