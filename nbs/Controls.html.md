---
title: 控制语句
---




> 条件控制语句
- order: 5


根据布尔变量的值作为判断形成了`if`语句的判断原型，可以从最简单的语句开始。

::: {#2f0c1c82-4f47-4360-a572-16e0398a8f21 .cell execution_count=6}
``` {.python .cell-code}
temp = 37.5
if temp >= 38:
    print("你已经发烧了!")
else:
    print("你的体温正常")
    print("注意保持!")
```

::: {.cell-output .cell-output-stdout}
```
你的体温正常
注意保持!
```
:::
:::


从上面的例子中，通过简单的`if ... else ...`语句判断`temp`是否高于38，打印相应的语句。

## 多重条件
第一个例子中只有一个判断条件：即输入变量是否大于38。如果有多个判断条件，比如接着上面的例子通过温度再细分，可以用到`elif`去添加更多的判断条件。

::: {#283e9030-be98-4783-9e7d-02950a9d4b78 .cell execution_count=7}
``` {.python .cell-code}
temp = 38.5
if temp > 40:
    print("哦！小心，这是高烧!")
elif temp >= 38:
    print("嗯！这是低烧。")
elif temp >= 37:
    print("测试")
else:
    print("你的体温正常")
```

::: {.cell-output .cell-output-stdout}
```
嗯！这是低烧。
```
:::
:::


__课后练习__: 设计一段程序，完成下面任务：根据用户输入的成绩，打印不同的成绩结果，其中大于90，打印`A`, 80-90; 打印`B`, 70-79, 打印`C`; 60-69,打印`D`;其余的打印`F`。
包括了`input`，`if...elif`的使用,还有输入格式必须是数字。

## Match语句
Python 3.10以后，引入Match语句，可以根据变量值来判断进入不同的分支。

::: {#bf62b910-2a42-4caa-989c-b410a039cfd5 .cell execution_count=9}
``` {.python .cell-code}
day = "Sunday"
match day.lower():
        case "monday" | "tuesday" | "wednesday" | "thursday" | "friday":
            print("Weekday")
        case "saturday" | "sunday":
            print("Weekend")
        case _:
            print("Invalid day")
```

::: {.cell-output .cell-output-stdout}
```
Weekend
```
:::
:::


__课后练习__: 设计一个程序使用`match`语句， 根据不同的[HTTP状态码](https://baike.baidu.com/item/HTTP%E7%8A%B6%E6%80%81%E7%A0%81/5053660?fr=ge_ala)来判断显示不同的提示语句，当状态码是404，显示"not found"; 当状态码是400，显示"bad request";当状态码是500, 显示"Internal server error";其他显示"Something wrong with the service"

## 逻辑条件判断
通过判断条件的组合，`if`语句可以完成多个变量的同时判断。

::: {#9c9edcd9-931f-436b-b1a5-6292b4f23ecc .cell execution_count=10}
``` {.python .cell-code}
age = 18
sex = "F"
if age >= 18 and sex == "F":
    print("成年女性")
```

::: {.cell-output .cell-output-stdout}
```
成年女性
```
:::
:::


## 三元运算符
简单的逻辑判断可以通过简单的三元运算符来实现。

::: {#fa45605e-1a40-4c5a-8afe-405c90b1eed8 .cell execution_count=11}
``` {.python .cell-code}
x = 3242389
"偶数" if x % 2 == 0 else "奇数"
```

::: {.cell-output .cell-output-display execution_count=11}
```
'奇数'
```
:::
:::


::: {#55565190-033b-43bb-ad6b-908773766428 .cell execution_count=12}
``` {.python .cell-code}
x
```

::: {.cell-output .cell-output-display execution_count=12}
```
3242389
```
:::
:::


__课后练习__: 改造第一个例子，采用三元运算符判断温度是否超过38.

## 循环语句控制
当我们需要对于一系列的输入进行批量处理的时候，需要通过循环语句来控制，最常用的`for`循环和`while`循环。

## `for`循环
一般`for`循环跟`range`函数配合使用，`range(start, stop)`函数会返回从`start`到`stop`范围内的一系列数字，当没有提供`start`值时，默认为0， 可以从以下函数解释中查找这个函数的详细解释。[1, 6)

::: {#727a7acc-b55a-47b3-84c6-3423780c9572 .cell execution_count=14}
``` {.python .cell-code}
?range
```

::: {.cell-output .cell-output-display}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-red-fg">Init signature:</span> range<span class="ansi-blue-fg">(</span>self<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">/</span><span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">*</span>args<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">**</span>kwargs<span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">Docstring:</span>     
range(stop) -&gt; range object
range(start, stop[, step]) -&gt; range object
Return an object that produces a sequence of integers from start (inclusive)
to stop (exclusive) by step.  range(i, j) produces i, i+1, i+2, ..., j-1.
start defaults to 0, and stop is omitted!  range(4) produces 0, 1, 2, 3.
These are exactly the valid indices for a list of 4 elements.
When step is given, it specifies the increment (or decrement).
<span class="ansi-red-fg">Type:</span>           type
<span class="ansi-red-fg">Subclasses:</span>     </pre>
```

:::

:::
:::


::: {#3cd770d0-62b7-43e0-ad8b-2ac8e22f3008 .cell execution_count=21}
``` {.python .cell-code}
for i in range(1, 6):
    print( '*' * i)
```

::: {.cell-output .cell-output-stdout}
```
*
**
***
****
*****
```
:::
:::


::: {#94666c92-e0c4-4f0b-a5c5-f3bcf1a42087 .cell execution_count=22}
``` {.python .cell-code}
?enumerate
```

::: {.cell-output .cell-output-display}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-red-fg">Init signature:</span> enumerate<span class="ansi-blue-fg">(</span>iterable<span class="ansi-blue-fg">,</span> start<span class="ansi-blue-fg">=</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">Docstring:</span>     
Return an enumerate object.
  iterable
    an object supporting iteration
The enumerate object yields pairs containing a count (from start, which
defaults to zero) and a value yielded by the iterable argument.
enumerate is useful for obtaining an indexed list:
    (0, seq[0]), (1, seq[1]), (2, seq[2]), ...
<span class="ansi-red-fg">Type:</span>           type
<span class="ansi-red-fg">Subclasses:</span>     </pre>
```

:::

:::
:::


也可以通过枚举函数`enumerate()`来实现。

::: {#d6eb1ef6-c30e-41ff-ba00-601e3802a8e4 .cell execution_count=24}
``` {.python .cell-code}
fruits = ['苹果', '香蕉', '梨子']
for index, fruit in enumerate(fruits):
    print(f"{index}.{fruit}")
```

::: {.cell-output .cell-output-stdout}
```
0.苹果
1.香蕉
2.梨子
```
:::
:::


::: {#18411e3d-6995-47e4-9346-de97a75ed605 .cell execution_count=26}
``` {.python .cell-code}
fruits[1]
```

::: {.cell-output .cell-output-display execution_count=26}
```
'香蕉'
```
:::
:::


__课后练习__  ：利用`for`循环语句打印9*9乘法表。

## 多重循环
在有些问题中，需要循环的嵌套来完成某些任务。

::: {#7f7acdd8-fe9b-4f4f-b70f-ffd625d6fd91 .cell execution_count=32}
``` {.python .cell-code}
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i}*{j} = {i*j} ", end="")
    print(" ") 
```

::: {.cell-output .cell-output-stdout}
```
1*1 = 1 1*2 = 2 1*3 = 3 1*4 = 4 1*5 = 5  
2*1 = 2 2*2 = 4 2*3 = 6 2*4 = 8 2*5 = 10  
3*1 = 3 3*2 = 6 3*3 = 9 3*4 = 12 3*5 = 15  
4*1 = 4 4*2 = 8 4*3 = 12 4*4 = 16 4*5 = 20  
5*1 = 5 5*2 = 10 5*3 = 15 5*4 = 20 5*5 = 25  
```
:::
:::


## `break`语句
如果在循环中，遇到满足某些条件需要跳出整个循环，`break`语句就可以发挥作用了。它可以用于跳出最内层的循环。

::: {#aae44394-e3cf-4389-a016-dc84b865b116 .cell execution_count=33}
``` {.python .cell-code}
for i in range(10):
    if i == 5:
        break
    print(i)
```

::: {.cell-output .cell-output-stdout}
```
0
1
2
3
4
```
:::
:::


在上面的循环中，原本是打印0到9的数字，但是`if`语句判断当前值是否是5，通过`break`推出当前循环，因此打印了从0到4的数字 

::: {#4f986d45-9f1b-46fd-bc0c-8e1e7b0bb6d7 .cell execution_count=35}
``` {.python .cell-code}
for i in range(10):
    for j in range(10):
        if i + j > 10:
            break
        print(f"{i} + {j}")
```

::: {.cell-output .cell-output-stdout}
```
0 + 0
0 + 1
0 + 2
0 + 3
0 + 4
0 + 5
0 + 6
0 + 7
0 + 8
0 + 9
1 + 0
1 + 1
1 + 2
1 + 3
1 + 4
1 + 5
1 + 6
1 + 7
1 + 8
1 + 9
2 + 0
2 + 1
2 + 2
2 + 3
2 + 4
2 + 5
2 + 6
2 + 7
2 + 8
3 + 0
3 + 1
3 + 2
3 + 3
3 + 4
3 + 5
3 + 6
3 + 7
4 + 0
4 + 1
4 + 2
4 + 3
4 + 4
4 + 5
4 + 6
5 + 0
5 + 1
5 + 2
5 + 3
5 + 4
5 + 5
6 + 0
6 + 1
6 + 2
6 + 3
6 + 4
7 + 0
7 + 1
7 + 2
7 + 3
8 + 0
8 + 1
8 + 2
9 + 0
9 + 1
```
:::
:::


## `continue`语句
如果在循环中，遇到满足某些条件需要跳出当前循环，采用`continue`语句可以当前目标。同样的，`continue`也是用于跳出最内层的循环。

::: {#351f4859-d041-4ab8-afdf-90b214b89322 .cell execution_count=36}
``` {.python .cell-code}
for i in range(10):
    if i == 5:
        continue
    print(i)
```

::: {.cell-output .cell-output-stdout}
```
0
1
2
3
4
6
7
8
9
```
:::
:::


将前面例子中的`break`替换为`continue`，我们可以看到当`i`值为5时，跳过了打印的操作直接进入下一个循环。

## 与`else`结合的循环语句
在Python中，循环语句有一个特殊的`else`语句，当循环正常执行完以后会执行`else`语句。

::: {#8e5ec392-bcfc-47c0-b255-3f07e193097e .cell execution_count=37}
``` {.python .cell-code}
for i in range(5):
    print(i)
else:
    print("循环正常结束。")
```

::: {.cell-output .cell-output-stdout}
```
0
1
2
3
4
循环正常结束。
```
:::
:::


::: {#828f9b24-aa91-4e92-aebf-fc4d922bc238 .cell execution_count=38}
``` {.python .cell-code}
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("This won't be printed")
```

::: {.cell-output .cell-output-stdout}
```
0
1
2
```
:::
:::


将上个例子的`break`改成了`continue`，循环可以正常结束，`else`后的逻辑可以正常执行

::: {#e11622c4-5acd-4283-ab0c-66470dd5e566 .cell execution_count=39}
``` {.python .cell-code}
for i in range(5):
    if i == 3:
        continue
    print(i)
else:
    print("This won't be printed")
```

::: {.cell-output .cell-output-stdout}
```
0
1
2
4
This won't be printed
```
:::
:::


__课后练习__ :设计一个猜数字的游戏，一共可以猜五次，如果猜的数字比实际数字大则提示用户你猜的数字太大了，如果猜的数字比实际数字小则提示用户你猜的数字太小了，如果猜中了则游戏退出提示用户恭喜你猜对了。如果五次都没有猜中则打印游戏结束你没有猜对。

## `while`循环
类似于`for`循环，`while`循环是另一种常见的循环控制语句。

::: {#73db6738-e855-4e06-a62e-4bf5ed9a3f8f .cell execution_count=40}
``` {.python .cell-code}
import time

seconds = 5
while seconds > 0:
    print(seconds)
    time.sleep(1)
    seconds -= 1
print("时间到!")
```

::: {.cell-output .cell-output-stdout}
```
5
4
3
2
1
时间到!
```
:::
:::


与`for`循环一样，`while`循环可以结合`break`和`continue`一起使用。

::: {#697d2043-bc19-4e77-8ce9-1a1b3bd0639d .cell execution_count=41}
``` {.python .cell-code}
num = 0
while True:
    num += 1
    if num % 3 == 0:
        continue
    if num > 50:
        break
    print(num, end=" ")

print("\n结束操作")

```

::: {.cell-output .cell-output-stdout}
```
1 2 4 5 7 8 10 11 13 14 16 17 19 20 22 23 25 26 28 29 31 32 34 35 37 38 40 41 43 44 46 47 49 50 
结束操作
```
:::
:::



