---
title: 函数
---




> Python中的函数
- order: 6


在数学中，我们接触到了函数的概念，定义为一个集合A到集合B的映射。在编程语言中也有类似的概念，也是有输入参数到输出参数的机制。它有很多好处：
* 代码重用，可以将代码逻辑封装成函数，可以在多个地方调用。
* 将复杂的操作分解成小的，易于理解的函数可以提高可读性。
* 提供了一种抽象机制，有助于简化问题。
* 促进了并发和异步编程
* 测试将更加方便

::: {#4a189715-9e33-447a-8725-b2fbf89b8344 .cell execution_count=1}
``` {.python .cell-code}
def fib(n):
    """打印小于n的斐波拉契数列."""
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

fib(200)
```
:::


以上就是一个典型的`python`函数，包括这么几个性质：
* 定义函数：使用`def`关键字，后跟函数名和括号。
* 参数：函数可以接受参数，这些参数在括号内定义。
* 返回值：使用`return`语句返回函数的结果。
* 调用函数: 使用函数明加括号来调用函数。

## 参数类型
Python可以接受不同类型的参数：
- 位置参数

::: {#3917cf70-0dd4-4ba3-b5a9-b752d19cb701 .cell execution_count=3}
``` {.python .cell-code}
def add(a, b):
    return a + b

result = add(3, 5)
print(result)
```

::: {.cell-output .cell-output-stdout}
```
8
```
:::
:::


- 关键字参数
通过关键字`=`对应的值这样的形式来传参。

::: {#1b3c3e6e-695b-4268-88b4-9904b6dd0dee .cell execution_count=5}
``` {.python .cell-code}
def greet(name, greeting):
    return f"{greeting}, {name}!"

result = greet(greeting="你好", name="小明") 
print(result)
```

::: {.cell-output .cell-output-stdout}
```
你好, 小明!
```
:::
:::


 - 使用 `*args`这样的参数列表形式和``**kwargs``这样的关键字参数形式来代表可变数量的参数。

::: {#8bb11cb7-6b5c-4fd6-ab68-362be804394e .cell execution_count=6}
``` {.python .cell-code}
def sum_all(*args):
    return sum(args)

result = sum_all(1, 2, 3, 4) 
print(result)
```

::: {.cell-output .cell-output-stdout}
```
10
```
:::
:::


::: {#101c7763-76ad-46bb-8017-faed8c974ebf .cell execution_count=7}
``` {.python .cell-code}
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="小明", age=25, city="北京")
```

::: {.cell-output .cell-output-stdout}
```
name: 小明
age: 25
city: 北京
```
:::
:::


- 默认参数
默认参数允许在定义函数时为参数指定参数值，并且默认参数必须放在非默认参数之后。

::: {#1d1ecb40-a773-480d-939d-527dcecd4e21 .cell execution_count=8}
``` {.python .cell-code}
def greet(name, greeting="你好"):
    return f"{greeting}, {name}"

result1 = greet("小明")
```
:::


::: {#be55e809-8aae-425e-a2f4-8cc7565d3a3b .cell execution_count=9}
``` {.python .cell-code}
print(result1)
```

::: {.cell-output .cell-output-stdout}
```
你好, 小明
```
:::
:::


::: {#147d761f-7719-4b46-bf91-472261cad516 .cell execution_count=10}
``` {.python .cell-code}
result2 = greet("小明", "早上好")
print(result2)
```

::: {.cell-output .cell-output-stdout}
```
早上好, 小明
```
:::
:::


默认参数只会计算一次，因此当默认值是可变对象时候要特别小心。

::: {#4a99d4e8-7675-428b-9e7a-4b888361f081 .cell execution_count=11}
``` {.python .cell-code}
def f(a, L=[]):
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))
```

::: {.cell-output .cell-output-stdout}
```
[1]
[1, 2]
[1, 2, 3]
```
:::
:::


可以看到默认值在多次调用函数中会共享，为了避免这一情况的发生，可以改变默认值：

::: {#846c9ee1-0d87-47a5-9646-61a9fff82801 .cell execution_count=12}
``` {.python .cell-code}
def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```
:::


- 匿名函数(`lambda`)
`lambda`函数是一种小型匿名函数，可以有任何数量的参数，但只能有一个表达式。

::: {#9dae306d-831b-4207-9be5-3111d8479953 .cell execution_count=13}
``` {.python .cell-code}
def square(x):
    return x ** 2

print(square(4))
```

::: {.cell-output .cell-output-stdout}
```
16
```
:::
:::


::: {#aa9ad6fb-31b2-473d-8c03-9ee287d4f0c8 .cell execution_count=14}
``` {.python .cell-code}
squared_lambda = lambda x: x ** 2
print(squared_lambda(4))
```

::: {.cell-output .cell-output-stdout}
```
16
```
:::
:::


::: {#e653d9d7-ea19-42d1-b1e1-9c01e2598f75 .cell execution_count=15}
``` {.python .cell-code}
numbers = [1, 2, 3 ,4, 5]
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(squared_numbers)
```

::: {.cell-output .cell-output-stdout}
```
[1, 4, 9, 16, 25]
```
:::
:::


::: {#a6fa0bea-edd1-4580-962c-532f1321ccce .cell execution_count=16}
``` {.python .cell-code}
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key = lambda pair:pair[1])
print(pairs)
```

::: {.cell-output .cell-output-stdout}
```
[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```
:::
:::


__课后练习__ :创建一个函数计算购物车的总价，包括折扣等。

