Basic Coding Standard
=====================
基本代码编写标准
=====================

This section of the standard comprises what should be considered the standard
coding elements that are required to ensure a high level of technical
interoperability between shared PHP code.


这部分标准用来保证共享代码的技术互操作性。


The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].


不同紧要性的关键词：MUST,MUST NOT,REQUIRED,SHALL,SHALL NOT,SHOULD,SHOULD NOT,RECOMMENDED,MAY,OPTIONAL。

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md


1. Overview
1. 概述
-----------

- Files MUST use only `<?php` and `<?=` tags.
- 代码文件仅必须[MUST]使用 `<?php` 和 `<?=` 标记。

- Files MUST use only UTF-8 without BOM for PHP code.
- 代码文件仅必须[MUST]使用UTF-8 without BOM的字符集编码。

- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but SHOULD NOT do both.
- 代码文件（可能被其他代码包含），其中不应该同时包含存声明（类，方法，常量等）和可能引起副作用的代码（生成，输出，改变 初始化数据和设置等）。

- Namespaces and classes MUST follow [PSR-0][].
- 命名空间和类名必须遵循[PSR-0]。

- Class names MUST be declared in `StudlyCaps`.
- 类名必须声明成单词首字母全大写格式，如：HappyPerson。

- Class constants MUST be declared in all upper case with underscore separators.
- 类常量必须使用全大写字母和下划线组成。

- Method names MUST be declared in `camelCase`.
- 方法名称必须声明成首个单词首个字母小写，其他单词首个字母大写，如：slowLife()。

2. Files
2. 详细解析
--------

### 2.1. PHP Tags
### 2.1. PHP标签

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

PHP代码必须使用形如：`<?php ?>`的长标签或形如<?= ?>的短标签；不可以使用其他的标签类型。

### 2.2. Character Encoding
### 2.2. 字符编码

PHP code MUST use only UTF-8 without BOM.

PHP代码仅必须使用UTF-8不带BOM的编码格式。

### 2.3. Side Effects
### 2.3. 副作用

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

一个文件应该声明新的字符（如,类，方法，常量等。）和没用副作用的代码，否则就应该只包含会引起副作用的逻辑代码，
但是不可以同时包含

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

“副作用”是指执行逻辑没有直接声明的类、方法或常量等。*仅仅包含文件*

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

"副作用"包含但是不限于下列情况：产生输出、使用`require`或`include`、连接外部服务、修改
初始化设置、产生错误或者异常、修改全局或静态变量、文件I/O操作等等。

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

以下的例子包含了声明和副作用的列子，提醒我们应该注意一些什么：

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. Namespace and Class Names
----------------------------

Namespaces and classes MUST follow [PSR-0][].

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

Class names MUST be declared in `StudlyCaps`.

Code written for PHP 5.3 and after MUST use formal namespaces.

For example:

```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

Code written for 5.2.x and before SHOULD use the pseudo-namespacing convention
of `Vendor_` prefixes on class names.

```php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```

4. Class Constants, Properties, and Methods
-------------------------------------------

The term "class" refers to all classes, interfaces, and traits.

### 4.1. Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Properties

This guide intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### 4.3. Methods

Method names MUST be declared in `camelCase()`.
