---
title: 序列型数据结构
---




> Sequence数据结构
- order: 7


在Python中，[序列]((https://docs.python.org/zh-cn/3/glossary.html#term-sequence))使用整数索引进行高效的元素访问，包括字符串string, 列表list和元组tuple，其中字符串可以看作是字符的序列，list和tuple看作是任意Python 对象的序列。

首先我们来回顾一下序列型数据结构的运算符跟数学运算符的区别吧。

::: {#531e399b-d6c0-4a33-91f8-ea6daaeee6cc .cell execution_count=1}
``` {.python .cell-code}
t1 = [1, 2, 4, 'a']
t2 = [5, 6]
print(t1 + t2)
```

::: {.cell-output .cell-output-stdout}
```
[1, 2, 4, 'a', 5, 6]
```
:::
:::


这里`+`号将两个list合并成一个list.

::: {#787f1e60-61b4-4dd0-8cd4-f49772addf23 .cell execution_count=2}
``` {.python .cell-code}
a = [10, 45, 53]
b = 3 * [a]
print(b)
```

::: {.cell-output .cell-output-stdout}
```
[[10, 45, 53], [10, 45, 53], [10, 45, 53]]
```
:::
:::


这里乘号`*`对原序列进行了复制。

::: {#57761af4-c68e-470e-b41e-2a041f8add8c .cell execution_count=3}
``` {.python .cell-code}
a[2] = -49
print(b)
```

::: {.cell-output .cell-output-stdout}
```
[[10, 45, -49], [10, 45, -49], [10, 45, -49]]
```
:::
:::


:::{.callout-note}
这里的复制是浅复制，因此如果原序列更改了某个元素，复制的序列并不会改变
:::

当然，我们可以通过创建新的列表来实现两个列表的同步。

::: {#ec74b51d-c22b-424b-8644-0fc0864c43de .cell execution_count=4}
``` {.python .cell-code}
a = [10, 45, 53]
b = [list(a) for j in range(3)]
print(b)

a[2] = -49
print(b)
```

::: {.cell-output .cell-output-stdout}
```
[[10, 45, 53], [10, 45, 53], [10, 45, 53]]
[[10, 45, 53], [10, 45, 53], [10, 45, 53]]
```
:::
:::


作为序列数据结构的常用操作方式，解包可以应用到所有序列数据结构中。

::: {#1970aebc-6a7d-4233-9f24-593f4b9bc755 .cell execution_count=5}
``` {.python .cell-code}
name = "Micheal"
a,b,c,d,e,f,g = name
```
:::


::: {#79aeeea8-d58f-4481-be5d-5c3fa343f381 .cell execution_count=6}
``` {.python .cell-code}
print(b)
```

::: {.cell-output .cell-output-stdout}
```
i
```
:::
:::


当需要比较两个序列数据结构时，它会从第一个元素开始比较每一个元素直到最后一个元素。对于字符串,采用[字典序](https://blog.csdn.net/oNever_say_love/article/details/49617611)lexicographical order的规则来比较

::: {#c93c5457-8cee-49b0-bab8-3815dd19a32e .cell execution_count=7}
``` {.python .cell-code}
a = [-3, -9, -18, -7, 5]
print(any([t > 0 for t in a]))
```

::: {.cell-output .cell-output-stdout}
```
True
```
:::
:::


::: {#0d504a15-b8a3-4e0e-8d50-60afcff3995a .cell execution_count=8}
``` {.python .cell-code}
print(all([t > 0 for t in a]))
```

::: {.cell-output .cell-output-stdout}
```
False
```
:::
:::


内置的`min`和`max`函数只能用于可以排序的序列数据结构

::: {#ca633863-b4dd-4eb8-93ad-cce7568becab .cell execution_count=9}
``` {.python .cell-code}
a = [4.3, 8.9, 3.5, -12.3]
print(min(a))
print(b)
```

::: {.cell-output .cell-output-stdout}
```
-12.3
i
```
:::
:::


## list列表
作为最常用的数据结构，是一个有序的，可变的序列，可以包含不同数据类型的元素。

### 创建
列表的创建可以通过中括号来创建

::: {#507acc15-a994-4df8-bedf-cd68cc8184fb .cell execution_count=10}
``` {.python .cell-code}
empty_list = []
```
:::


::: {#2de7a240-fd1c-4f3a-be94-ebca519c30e8 .cell execution_count=11}
``` {.python .cell-code}
mixed_list = [-34, 0.618, False, '列表创建', 5+5j]
```
:::


::: {#af4bee99-257e-4542-86de-019fd4553893 .cell execution_count=12}
``` {.python .cell-code}
coffee_list = ['瑞幸', '星巴克', 'manner', 'M stand']
```
:::


### 长度
作为一种序列数据结构，可以通过`len()`函数获取列表长度。

::: {#4c646b1b-316e-47d9-be2d-dd35b11a5f9d .cell execution_count=13}
``` {.python .cell-code}
print(f"咖啡总数是{len(coffee_list)}种")
```

::: {.cell-output .cell-output-stdout}
```
咖啡总数是4种
```
:::
:::


### 访问元素
`list`作为一种序列数据结构，可以通过索引进行访问，索引依然是从$0$开始.

::: {#aa13809a-8fd0-4e5d-ab07-be9d04299d04 .cell execution_count=14}
``` {.python .cell-code}
print(f"第一个咖啡品牌{coffee_list[0]}")
```

::: {.cell-output .cell-output-stdout}
```
第一个咖啡品牌瑞幸
```
:::
:::


::: {#168d7035-11a9-4fcb-a4e7-4e6f18f1ec2d .cell execution_count=15}
``` {.python .cell-code}
print(f"第二个咖啡品牌{coffee_list[1]}")
```

::: {.cell-output .cell-output-stdout}
```
第二个咖啡品牌星巴克
```
:::
:::


### 修改元素
作为可变的数据结构，不同于字符串任何时候我们都可以改变列表的某一元素

::: {#83263468-0b08-43e3-acce-3c90a598e511 .cell execution_count=16}
``` {.python .cell-code}
coffee_list[2] = '精品咖啡'
coffee_list
```

::: {.cell-output .cell-output-display execution_count=16}
```
['瑞幸', '星巴克', '精品咖啡', 'M stand']
```
:::
:::


::: {#3498ec83 .cell execution_count=17}
``` {.python .cell-code}
id(coffee_list)
```

::: {.cell-output .cell-output-display execution_count=17}
```
4390838976
```
:::
:::


可以看到上面的列表id 并没有发生变化

### 常用操作
下面罗列了列表的一些常用操作，大多数对列表本身进行了修改。

- 在列表末尾添加元素

::: {#d9f7ccbf .cell execution_count=18}
``` {.python .cell-code}
coffee_list.append('Peets coffee')
coffee_list
```

::: {.cell-output .cell-output-display execution_count=18}
```
['瑞幸', '星巴克', '精品咖啡', 'M stand', 'Peets coffee']
```
:::
:::


- 将可迭代对象的所有元素添加到列表末尾

::: {#b6436b40 .cell execution_count=19}
``` {.python .cell-code}
coffee_list.extend(['其他品牌', '咖啡豆'])
coffee_list
```

::: {.cell-output .cell-output-display execution_count=19}
```
['瑞幸', '星巴克', '精品咖啡', 'M stand', 'Peets coffee', '其他品牌', '咖啡豆']
```
:::
:::


- 删除并返回指定位置的元素，默认最后一个

::: {#de11a715 .cell execution_count=20}
``` {.python .cell-code}
coffee_list.pop()
coffee_list
```

::: {.cell-output .cell-output-display execution_count=20}
```
['瑞幸', '星巴克', '精品咖啡', 'M stand', 'Peets coffee', '其他品牌']
```
:::
:::


- 删除首次出现的指定元素

::: {#2eba0be0 .cell execution_count=22}
``` {.python .cell-code}
coffee_list.remove('M stand')
coffee_list
```

::: {.cell-output .cell-output-display execution_count=22}
```
['Peets coffee', '其他品牌', '星巴克', '瑞幸', '精品咖啡']
```
:::
:::


- 对列表进行排序

::: {#74abb946 .cell execution_count=21}
``` {.python .cell-code}
coffee_list.sort()
coffee_list
```

::: {.cell-output .cell-output-display execution_count=21}
```
['M stand', 'Peets coffee', '其他品牌', '星巴克', '瑞幸', '精品咖啡']
```
:::
:::


#### 课后练习 

设计一个奶茶店的订单系统，使用前面介绍的list的基本操作,满足一下功能
- 当用户下单后，生成一个新订单进入订单列表中
- 订单完成后，需要从订单系统中删除
- 需要可以展示当前还有多少订单
- 所有的功能可以用函数表示

### 队列推导式
在列表数据结构中，有一个强大而简洁的特性，它允许我们以一种简洁的方式创建新的列表。
- 列表推导式通常比等效的`for`循环快，但是非常大的列表，可能会消耗大量内存
- 虽然列表推导式可以使代码更简洁，但过于复杂的推导式可能会降低可读性

基本语法：``new_list = [expression for item in iterable]``

::: {#6473d45b .cell execution_count=23}
``` {.python .cell-code}
squares = [x**2 for x in range(10)]
print(squares)  
```

::: {.cell-output .cell-output-stdout}
```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
:::
:::


带条件的列表推导式： `new_list = [expression for item in iterable if condition]`

::: {#9d4aa623 .cell execution_count=24}
``` {.python .cell-code}
even_squares = [x**2 for x in range(10) if x % 2 == 0]
print(even_squares)  
```

::: {.cell-output .cell-output-stdout}
```
[0, 4, 16, 36, 64]
```
:::
:::


还可以结合函数运行

::: {#c2055efa .cell execution_count=25}
``` {.python .cell-code}
def is_even(n):
    return n % 2 == 0

even_numbers = [x for x in range(20) if is_even(x)]
print(even_numbers)
```

::: {.cell-output .cell-output-stdout}
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
:::
:::


## tuple(元组）
与`list`对应的是不可变序列类型就是`tuple`数据类型,可以作为以下用途:
- 作为字典的键，因为字典的键值必须不可变
- 返回多个值的函数
- 在某些情况下可以提高性能

### 创建
使用圆括号()创建，元素之间用逗号分隔。

::: {#d6f4d140 .cell execution_count=26}
``` {.python .cell-code}
empty_tuple = ()
mixed_tuple = (-34, 0.618, False, '列表创建', 5+5j)
coffee_tuple = ('瑞幸', '星巴克', 'manner', 'M stand')
```
:::


### 不可变性
:::{.callout-note}
tuple一旦创建不可以改变，这是它与list最大的区别。
:::

::: {#130debe0 .cell execution_count=27}
``` {.python .cell-code}
coffee_tuple[2] = 'Peets coffee'
```

::: {.cell-output .cell-output-error}

::: {.ansi-escaped-output}

```{=html}
<pre><span class="ansi-red-fg">---------------------------------------------------------------------------</span>
<span class="ansi-red-fg">TypeError</span>                                 Traceback (most recent call last)
Cell <span class="ansi-green-fg">In[27], line 1</span>
<span class="ansi-green-fg">----&gt; 1</span> coffee_tuple[<span style="color:rgb(98,98,98)">2</span>] <span style="color:rgb(98,98,98)">=</span> <span style="color:rgb(175,0,0)">'</span><span style="color:rgb(175,0,0)">Peets coffee</span><span style="color:rgb(175,0,0)">'</span>

<span class="ansi-red-fg">TypeError</span>: 'tuple' object does not support item assignment</pre>
```

:::

:::
:::


### 解包操作
同样可以将tuple解包到多个变量。

::: {#c639acd6 .cell execution_count=28}
``` {.python .cell-code}
coffee1, coffee2, coffee3, coffee4 = coffee_tuple
```
:::


### 常用方法
tuple的方法只有两个: `count`和`index`

::: {#6e93b42f .cell execution_count=29}
``` {.python .cell-code}
coffee_tuple.count('manner')
```

::: {.cell-output .cell-output-display execution_count=29}
```
1
```
:::
:::


::: {#0e1e381c .cell execution_count=30}
``` {.python .cell-code}
coffee_tuple.index('manner')
```

::: {.cell-output .cell-output-display execution_count=30}
```
2
```
:::
:::


#### 课后练习
结合列表和元组设计一个音乐播放列表，使用元组存储歌曲信息
- 设计一个函数返回当前歌曲列表，需要打印歌曲名称和歌手名称
- 设计一个函数返回列表中某一个歌曲序号下的歌曲名称，歌手名称，年代，歌曲流派信息
- 设计一个函数添加一个新的歌曲


