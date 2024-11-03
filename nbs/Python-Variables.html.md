---
title: 变量存储机制
---




> Python中的变量存储机制以及数据类型可变性


在变量是编程语言里重要的基本概念，在各类高级语言里都用变量来代表一块内存区域，某一时刻这块区域里存储了‘a’，又一时刻可能又被存储成了'c'， 正是由于该块内存里的值可以随时发生变化，我们称之这个代表内存区域的符号为变量。

想象一下你有一个超级神奇的衣柜（内存空间）。这个衣柜很特别，不是用来放衣服的，而是用来存放各种各样的"值"。让我们来看看这个衣柜是怎么工作的：

*变量名就像衣柜的标签* 🏷️

::: {#37b722b7-3e1c-4bbd-a7aa-3dd2d8b2b867 .cell execution_count=1}
``` {.python .cell-code}
a = 12
```
:::


这里的`a`就像是在衣柜上贴了一个标签，告诉你"这格柜子里放着数字12"

::: {#d2dcc5f9-0e42-4fd3-96b6-4b57f5b8664c .cell execution_count=2}
``` {.python .cell-code}
print(a)
```

::: {.cell-output .cell-output-stdout}
```
12
```
:::
:::


我们打印看看`a`的值，在这里Python在内存中创建了一个数12，并用a指向了它。

::: {#084f88a0-feb5-428f-898d-9e06536f4d3d .cell execution_count=3}
``` {.python .cell-code}
b = "Hello world"
```
:::


::: {#86f10561-322b-4e7f-ae7f-e41dc2931587 .cell execution_count=4}
``` {.python .cell-code}
print(b)
```

::: {.cell-output .cell-output-stdout}
```
Hello world
```
:::
:::


字符串也是一样的道理。此时Python在内存中创建了一个字符串"Hello world", 并用b指向了它。

我们一起来看一个有趣的现象🎭

::: {#f07da56f-50b4-416f-9b21-467b61036098 .cell execution_count=5}
``` {.python .cell-code}
x = 300
y = 300
print(x is y)
```

::: {.cell-output .cell-output-stdout}
```
False
```
:::
:::


::: {#c196688c-90dc-41fe-b106-dc14c06cae12 .cell execution_count=6}
``` {.python .cell-code}
small_x = 5
small_y = 5
print(small_x is small_y)
```

::: {.cell-output .cell-output-stdout}
```
True
```
:::
:::


咦？这是为什么呢？因为 Python 有个小机灵鬼行为：对于范围在-5到256之间的整数，Python 会提前在衣柜里准备好这些常用的数字，所以相同的小数字会指向同一个柜格！

想要真正复制一个列表？🔄

::: {#c15a9c7f-29d1-4740-bb60-e31e82d5afca .cell execution_count=7}
``` {.python .cell-code}
original = [1, 2, 3]
copy = original.copy()
```
:::


这就像是在衣柜里新开了一格，把原来的东西完完整整地复制了一份~

::: {#1021f711-33b9-4097-9510-f3db4c1f16a8 .cell execution_count=8}
``` {.python .cell-code}
print(f'a的id是{id(a)}')
```

::: {.cell-output .cell-output-stdout}
```
a的id是4368674248
```
:::
:::


::: {#81d65f13-ff6b-40e8-82dd-d924db786983 .cell execution_count=9}
``` {.python .cell-code}
print(f'b的id是{id(b)}')
```

::: {.cell-output .cell-output-stdout}
```
b的id是4441018352
```
:::
:::


`id()`函数就像是查看衣柜格子的编号，让你知道变量到底指向哪里, 才找到每个对象所在的内存位置。

::: {#40e17431-3d98-46e5-b2a7-04eefe1f34bf .cell execution_count=10}
``` {.python .cell-code}
?id
```

::: {.cell-output .cell-output-display}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-red-fg">Signature:</span> id<span class="ansi-blue-fg">(</span>obj<span class="ansi-blue-fg">,</span> <span class="ansi-blue-fg">/</span><span class="ansi-blue-fg">)</span>
<span class="ansi-red-fg">Docstring:</span>
Return the identity of an object.
This is guaranteed to be unique among simultaneously existing objects.
(CPython uses the object's memory address.)
<span class="ansi-red-fg">Type:</span>      builtin_function_or_method</pre>
```

:::

:::
:::


::: {#18a6116d-957e-4b9a-8296-5a5b260e46e0 .cell execution_count=11}
``` {.python .cell-code}
a = 13
print(f"a的id是{id(a)}")
```

::: {.cell-output .cell-output-stdout}
```
a的id是4368674280
```
:::
:::


::: {#7f0ae6c3-5184-4edf-b662-d3cd3cafaf2a .cell execution_count=12}
``` {.python .cell-code}
# 我们可以看看当执行a = b会发生什么
a = b
print(f'a的值是{a}, a的id值是{id(a)}')
print(f'b的值是{b}, b的id值是{id(b)}')
```

::: {.cell-output .cell-output-stdout}
```
a的值是Hello world, a的id值是4441018352
b的值是Hello world, b的id值是4441018352
```
:::
:::


当执行`a=b`以后，`a`和`b`指向同一个地址。如图
![image.png](Python-Variables_files/figure-html/f4d37c4e-32f6-42ee-aeef-7802e54edf0a-1-1ab4670d-b6d3-4f67-b7b5-120b0be7f1c4.png)

### 不可变数据类型
在Python中，不可变数据类型是指一旦创建就不能被修改的对象。让我们继续上面的例子重新给`a`赋值。

::: {#e42714ea-d682-4f79-9e79-44f198dff2b0 .cell execution_count=13}
``` {.python .cell-code}
a = 10
print(f'a的值是{a}, a的id值是{id(a)}')
print(f'b的值是{b}, b的id值是{id(b)}')
```

::: {.cell-output .cell-output-stdout}
```
a的值是10, a的id值是4368674184
b的值是Hello world, b的id值是4441018352
```
:::
:::


当执行完`a=10`以后, Python在内存中创建了一个整数10，并用a指向了它。b的值还有内存地址都不变。

::: {#4f9787e5-7f6f-4e91-b110-7dbde0df1db4 .cell execution_count=14}
``` {.python .cell-code}
b = "Python is fun"
print(f'b的值是{b}, b的id值是{id(b)}')
```

::: {.cell-output .cell-output-stdout}
```
b的值是Python is fun, b的id值是4441199920
```
:::
:::


### 可变数据类型
我们来看如果修改可变数据类型，会发生什么。

::: {#0b732900-d03f-4666-baca-c7da039d16f4 .cell execution_count=15}
``` {.python .cell-code}
list1 = [1, 2, 3]
list2 = list1

print(f"list1: {list1}, list1的id: {id(list1)}")
print(f"list2: {list2}, list2的id: {id(list2)}")
```

::: {.cell-output .cell-output-stdout}
```
list1: [1, 2, 3], list1的id: 4441079552
list2: [1, 2, 3], list2的id: 4441079552
```
:::
:::


::: {#d72f9a6a-ea1e-4340-83a0-25e398ef3086 .cell execution_count=16}
``` {.python .cell-code}
list1.append(4)
print(f"修改后list1: {list1}, list1的id: {id(list1)}")
print(f"list2: {list2}, list2的id: {id(list2)}")
```

::: {.cell-output .cell-output-stdout}
```
修改后list1: [1, 2, 3, 4], list1的id: 4441079552
list2: [1, 2, 3, 4], list2的id: 4441079552
```
:::
:::



* 创建列表 list1 = [1, 2, 3] 时,Python在内存中创建了这个列表对象。
* list2 = list1 使list2指向同一个列表对象。
* 当我们修改list1时(如append),实际上是修改了它指向的对象。因为list2指向同一个对象,所以list2也会看到这个变化。

::: {#c8af7da6-bc34-44be-8495-5db4dd444099 .cell execution_count=17}
``` {.python .cell-code}
def modify_list(lst):
    lst.append(5)

modify_list(list1)
print(f"函数调用后list1: {list1}")
print(f"函数调用后list2: {list2}")
```

::: {.cell-output .cell-output-stdout}
```
函数调用后list1: [1, 2, 3, 4, 5]
函数调用后list2: [1, 2, 3, 4, 5]
```
:::
:::


* 在Python中,函数参数是通过引用传递的。
* 当我们将list1传给函数modify_list时,函数内的lst参数指向与list1相同的对象。
* 因此,函数内对lst的修改会影响到list1和list2。

::: {#abd393b8-a7f8-4138-bc25-f0590dd98a5c .cell execution_count=18}
``` {.python .cell-code}
def create_object():
    temp = "这是一个临时对象"
    print(f"临时对象的id: {id(temp)}")

create_object()
```

::: {.cell-output .cell-output-stdout}
```
临时对象的id: 4440948048
```
:::
:::


* 在函数create_object中,我们创建了一个临时字符串对象。
* 当函数结束后,这个对象不再被任何变量引用,Python的垃圾回收机制会在适当的时候将其删除,释放内存。


