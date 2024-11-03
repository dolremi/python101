---
title: 字典Dictionary
---




> 什么是字典
- order: 9


在Python中除了序列数据结构，字典作为一种键值对的映射数据结构，通过键(key)而不是数字索引来查找相关值。作为一种重要的数据结构，它是可变的并且无序的键值对集合。

:::{.callout_note}
在字典中，键是作为字典的索引，必须是唯一的，这样才能确保通过键可以找到相同的值，并且可以利用[哈希表](https://cloud.tencent.com/developer/article/1432801)快速查找
:::

## 创建
使用花括号{}创建，键和值用冒号:分隔,不同项之间用逗号,分隔。

::: {#0c3cf9ab .cell execution_count=1}
``` {.python .cell-code}
empty_dict = {}
coffee_dict = {'瑞幸': 10, '星巴克': 15, 'manner': 30, 'M stand': 35}
```
:::


## 键的特性
在字典中，键除了唯一的以外，必须是不可变类型。键可以是任何不可变类型；字符串和数字总是可以作为键。 如果一个元组只包含字符串、数字或元组则也可以作为键；如果一个元组直接或间接地包含了任何可变对象，则 __不能作为键__ 。 列表不能作为键，因为列表可以使用索引赋值、切片赋值或者`append()`和`extend()`等方法进行原地修改列表。

## 访问值
区别于序列数据结构，字典中的值是通过键作为索引访问的。

::: {#dba625da .cell execution_count=2}
``` {.python .cell-code}
print(f"瑞幸剩余库存是:{coffee_dict['瑞幸']}")
```

::: {.cell-output .cell-output-stdout}
```
瑞幸剩余库存是:10
```
:::
:::


## 修改和添加
通过按照`dict[key] = value`的格式可以快速实现修改或者添加新的键值对。

::: {#f2547438 .cell execution_count=3}
``` {.python .cell-code}
coffee_dict['星巴克'] = 23
coffee_dict
```

::: {.cell-output .cell-output-display execution_count=3}
```
{'瑞幸': 10, '星巴克': 23, 'manner': 30, 'M stand': 35}
```
:::
:::


::: {#00a9881e .cell execution_count=4}
``` {.python .cell-code}
coffee_dict['Beets Coffee'] = 50
coffee_dict
```

::: {.cell-output .cell-output-display execution_count=4}
```
{'瑞幸': 10, '星巴克': 23, 'manner': 30, 'M stand': 35, 'Beets Coffee': 50}
```
:::
:::


## 删除

::: {#92711230 .cell execution_count=6}
``` {.python .cell-code}
del coffee_dict['Beets Coffee']
```
:::


::: {#81f6c2ac .cell execution_count=7}
``` {.python .cell-code}
coffee_dict_modified = coffee_dict.pop('manner')
```
:::


::: {#11411f65 .cell execution_count=8}
``` {.python .cell-code}
coffee_dict_modified
```

::: {.cell-output .cell-output-display execution_count=8}
```
30
```
:::
:::


::: {#5186c7a9 .cell execution_count=9}
``` {.python .cell-code}
coffee_dict
```

::: {.cell-output .cell-output-display execution_count=9}
```
{'瑞幸': 10, '星巴克': 23, 'M stand': 35}
```
:::
:::


## 常用方法
下面罗列一些常用方法

::: {#a2374eb6 .cell execution_count=10}
``` {.python .cell-code}
coffee_dict.keys()
```

::: {.cell-output .cell-output-display execution_count=10}
```
dict_keys(['瑞幸', '星巴克', 'M stand'])
```
:::
:::


::: {#244564ce .cell execution_count=11}
``` {.python .cell-code}
coffee_dict.values()
```

::: {.cell-output .cell-output-display execution_count=11}
```
dict_values([10, 23, 35])
```
:::
:::


::: {#771556db .cell execution_count=13}
``` {.python .cell-code}
coffee_dict.items()
```

::: {.cell-output .cell-output-display execution_count=13}
```
dict_items([('瑞幸', 10), ('星巴克', 23), ('M stand', 35)])
```
:::
:::


::: {#9e787799 .cell execution_count=14}
``` {.python .cell-code}
coffee_dict.get('M stand')
```

::: {.cell-output .cell-output-display execution_count=14}
```
35
```
:::
:::


::: {#e6e913cf .cell execution_count=15}
``` {.python .cell-code}
coffee_dict.update({'Beets Coffee': 24})
```
:::


::: {#5dff0176 .cell execution_count=16}
``` {.python .cell-code}
coffee_dict
```

::: {.cell-output .cell-output-display execution_count=16}
```
{'瑞幸': 10, '星巴克': 23, 'M stand': 35, 'Beets Coffee': 24}
```
:::
:::


## 字典推导式
类似于列表推导式，字典也有自己方式快速建立字典

::: {#cdbdfcf9 .cell execution_count=17}
``` {.python .cell-code}
squares = {x: x**2 for x in range(5)}
```
:::


::: {#e3ea31fb .cell execution_count=18}
``` {.python .cell-code}
squares
```

::: {.cell-output .cell-output-display execution_count=18}
```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```
:::
:::


字典的查找、插入和删除操作都是十分高效的

#### 课后作业
利用字典的功能设计一个简单的聊天机器人，可以将用户常用的对话用字典的形式保存起来，用户通过选择固定的问题得到机器人的回答。


