---
title: 异常处理
---




> 怎么处理异常？
- order: 10


在Python中，错误可以分为两种：__语法错误__ 和 __异常__。其中语法错误是学习Python中常见的错误，如下例：

::: {#9ddb99cb .cell execution_count=1}
``` {.python .cell-code}
if True print("Hello world")
```

::: {.cell-output .cell-output-error}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-cyan-fg">  Cell </span><span class="ansi-green-fg">In[1], line 1</span>
<span class="ansi-red-fg">    if True print("Hello world")</span>
            ^
<span class="ansi-red-fg">SyntaxError</span><span class="ansi-red-fg">:</span> invalid syntax
</pre>
```

:::

:::
:::


语法错误是解析器解析时发现程序编写时的语法错误，作为程序员应该要极力避免的错误。这里我们主要讨论另一类错误，异常。

## 什么是异常?
异常是程序执行过程中发生的事件，通常会影响程序的正常执行。它们是Python对象，表示一个错误状态。当Python脚本发生异常时，如果不进行处理，程序将终止执行，并输出错误信息。

## 异常处理机制
Python的异常处理使用`try`、`except`、`else`和`finally`语句块来捕获和处理异常。

### 基本语法

::: {#099c924a .cell execution_count=2}
``` {.python .cell-code}
try:
    # 可能引发异常的代码
except ExceptionType:
    # 处理特定异常
else:
    # 如果没有异常发生时执行的代码
finally:
    # 无论是否发生异常都会执行的代码
```

::: {.cell-output .cell-output-error}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-cyan-fg">  Cell </span><span class="ansi-green-fg">In[2], line 3</span>
<span class="ansi-red-fg">    except ExceptionType:</span>
    ^
<span class="ansi-red-fg">IndentationError</span><span class="ansi-red-fg">:</span> expected an indented block after 'try' statement on line 1
</pre>
```

:::

:::
:::


`try`：将可能引发异常的代码放在此块中。
`except`：捕获并处理特定类型的异常。
`else`：在没有发生任何异常时执行的代码块（可选）。
`finally`：无论是否发生异常，都会执行的代码块（通常用于清理资源）。

:::{.callout_note}
注意与`if`区别看待，`if`条件判断一般用于场景
:::

###  捕获异常

::: {#4f1385b2 .cell execution_count=3}
``` {.python .cell-code}
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

::: {.cell-output .cell-output-stdout}
```
Error: division by zero
```
:::
:::


## 抛出异常
可以使用`raise`语句手动抛出异常。这在满足特定条件时非常有用

::: {#c316cffe .cell execution_count=4}
``` {.python .cell-code}
def check_positive(value):
    if value < 0:
        raise ValueError("Value must be non-negative.")
```
:::


## 常见内置异常
Python定义了多种内置异常类型，包括但不限于：
* `ValueError`：传入无效参数。
* `TypeError`：操作或函数应用于不适当类型的对象。
* `IndexError`：序列中没有该索引。
* `KeyError`：字典中没有该键。
* `FileNotFoundError`：文件未找到。


