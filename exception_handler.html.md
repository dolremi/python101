# 异常处理


<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

在Python中，错误可以分为两种：**语法错误** 和
**异常**。其中语法错误是学习Python中常见的错误，如下例：

``` python
if True print("Hello world")
```

    SyntaxError: invalid syntax (3732902256.py, line 1)
    [0;36m  Cell [0;32mIn[1], line 1[0;36m[0m
    [0;31m    if True print("Hello world")[0m
    [0m            ^[0m
    [0;31mSyntaxError[0m[0;31m:[0m invalid syntax

语法错误是解析器解析时发现程序编写时的语法错误，作为程序员应该要极力避免的错误。这里我们主要讨论另一类错误，异常。

## 什么是异常?

异常是程序执行过程中发生的事件，通常会影响程序的正常执行。它们是Python对象，表示一个错误状态。当Python脚本发生异常时，如果不进行处理，程序将终止执行，并输出错误信息。

## 异常处理机制

Python的异常处理使用`try`、`except`、`else`和`finally`语句块来捕获和处理异常。

### 基本语法

``` python
try:
    # 可能引发异常的代码
except ExceptionType:
    # 处理特定异常
else:
    # 如果没有异常发生时执行的代码
finally:
    # 无论是否发生异常都会执行的代码
```

    IndentationError: expected an indented block after 'try' statement on line 1 (1192898691.py, line 3)
    [0;36m  Cell [0;32mIn[2], line 3[0;36m[0m
    [0;31m    except ExceptionType:[0m
    [0m    ^[0m
    [0;31mIndentationError[0m[0;31m:[0m expected an indented block after 'try' statement on line 1

`try`：将可能引发异常的代码放在此块中。
`except`：捕获并处理特定类型的异常。
`else`：在没有发生任何异常时执行的代码块（可选）。
`finally`：无论是否发生异常，都会执行的代码块（通常用于清理资源）。

<div class="callout_note">

注意与`if`区别看待，`if`条件判断一般用于场景

</div>

### 捕获异常

``` python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

    Error: division by zero

## 抛出异常

可以使用`raise`语句手动抛出异常。这在满足特定条件时非常有用

``` python
def check_positive(value):
    if value < 0:
        raise ValueError("Value must be non-negative.")
```

## 常见内置异常

Python定义了多种内置异常类型，包括但不限于： \*
`ValueError`：传入无效参数。 \*
`TypeError`：操作或函数应用于不适当类型的对象。 \*
`IndexError`：序列中没有该索引。 \* `KeyError`：字典中没有该键。 \*
`FileNotFoundError`：文件未找到。