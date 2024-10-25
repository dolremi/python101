---
title: Set
---




与序列数据结构不同的是,set 作为一种无序，可变的集合，其中的元素是唯一的，可以看作是数学中的集合概念：


- 元素在set中没有特定的顺序
- 每个元素只能出现一次
- 可以添加或者删除元素
- 元素必须是不可变类型

## 创建
使用花括号{}或者`set()`函数创建

::: {#3a14cf2b .cell execution_count=1}
``` {.python .cell-code}
empty_set = set()
mixed_set = (-34, 0.618, False, '列表创建', 5+5j)
coffee_set = set(['瑞幸', '星巴克', 'manner', 'M stand'])
```
:::


:::{.callout-note}
花括号{}创建的是空字典，不是空集合
:::

## 添加元素

::: {#e807852d .cell execution_count=2}
``` {.python .cell-code}
coffee_set.add('Beets coffee')
```
:::


::: {#c83f0709 .cell execution_count=3}
``` {.python .cell-code}
coffee_set
```

::: {.cell-output .cell-output-display execution_count=3}
```
{'Beets coffee', 'M stand', 'manner', '星巴克', '瑞幸'}
```
:::
:::


::: {#39441046 .cell execution_count=4}
``` {.python .cell-code}
coffee_set.update(['雀巢','精品'])
```
:::


::: {#713b2a4a .cell execution_count=5}
``` {.python .cell-code}
coffee_set
```

::: {.cell-output .cell-output-display execution_count=5}
```
{'Beets coffee', 'M stand', 'manner', '星巴克', '瑞幸', '精品', '雀巢'}
```
:::
:::


## 删除元素

::: {#221de692 .cell execution_count=6}
``` {.python .cell-code}
coffee_set.remove('精品')
```
:::


::: {#77f81072 .cell execution_count=7}
``` {.python .cell-code}
coffee_set
```

::: {.cell-output .cell-output-display execution_count=7}
```
{'Beets coffee', 'M stand', 'manner', '星巴克', '瑞幸', '雀巢'}
```
:::
:::


::: {#079d9338 .cell execution_count=8}
``` {.python .cell-code}
coffee_set.pop()
```

::: {.cell-output .cell-output-display execution_count=8}
```
'瑞幸'
```
:::
:::


:::{.callout_note}
在集合`set`里`pop()`函数是随机移除一个元素
:::

::: {#350e8bfe .cell execution_count=9}
``` {.python .cell-code}
coffee_set
```

::: {.cell-output .cell-output-display execution_count=9}
```
{'Beets coffee', 'M stand', 'manner', '星巴克', '雀巢'}
```
:::
:::


## 集合操作

::: {#1a0b6f8d .cell execution_count=10}
``` {.python .cell-code}
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
print(set1 | set2)  
print(set1 & set2)  
print(set1 - set2)  
print(set1 ^ set2) 
```

::: {.cell-output .cell-output-stdout}
```
{1, 2, 3, 4, 5, 6}
{3, 4}
{1, 2}
{1, 2, 5, 6}
```
:::
:::


## 冻结集合
`frozenset`是不可变版本的`set`.

::: {#eb99fc6e .cell execution_count=11}
``` {.python .cell-code}
frozen = frozenset([1, 2, 3])
```
:::


## 性能
集合的查找、添加和删除操作的平均时间复杂度为O(1),使其在处理唯一性和成员资格检查时非常高效。


