---
title: 基本数据类型
---




> 介绍Python中的基本数据类型和使用场景
- order: 2


在计算机世界，数据需要通过0和1来表示。而Python作为一种我们与计算机的交流语言，提供了一个基本数据类型的工具箱，每个基本数据类型就是一个个工具。掌握了这些数据类型，你就可以通过编程了指挥计算机为你服务了!

每种数据类型都有它的的特点和适用场景：

1. 不同的数据类型占用不同的内存空间,这让计算机能更高效地运行
2. 不同的数据类型支持不同的操作,比如数字可以做运算,字符串可以拼接
3. 合适的数据类型让代码更清晰易懂,也更不容易出错

Python的数据类型就像一个个特制的容器，每种特制容器都是为了存放特定类型的数据而设计。下面就让我们逐个了解每个容器吧:

## 整数 (int)
首先我们来看最熟悉的整数，在Python中我们可以用整数类型可以代表任何数学中的整数，这里注意Python中的整数是没有大小限制的哦。

::: {#53f51c20-1538-43d3-82df-b213562262c8 .cell execution_count=1}
``` {.python .cell-code}
x = 2
y = -56
big_num = 44823098509234
```
:::


我们在数学中学到的各类算数运算都可以直接使用在整数上。

::: {#a35791b5-f1cd-4eb7-822b-1310096d9639 .cell execution_count=2}
``` {.python .cell-code}
1+ 2 * 4 - 7
```

::: {.cell-output .cell-output-display execution_count=2}
```
2
```
:::
:::


:::{.callout-important}
Python中整数可以无限大，其内部采用一种**变长数组**的存储方式，将一个大整数分割成了一个个*数字块*.
:::

::: {#655d976c-aab6-4511-963a-4b3692a08b84 .cell execution_count=3}
``` {.python .cell-code}
print(big_num)
```

::: {.cell-output .cell-output-stdout}
```
44823098509234
```
:::
:::


## 浮点数(Float)
当你需要的数字带有小数点，这时我们就需要浮点数(Float)这个专属容器了，例如下面这个例子：

::: {#37b8abcd-8ed1-4209-881e-4322d1b87a23 .cell execution_count=4}
``` {.python .cell-code}
pi = 3.1415926
```
:::


### 浮点数是怎么存储的呢?
浮点数采用了IEEE754标准双精度标准，包含了三个关键部分。

| 符号位(1位)|指数位(11位)| 尾数位(52位)
|---------- |----------|------------|
| +/-       |   2^指数  |  1. xxxxx  |

让我们通过一个形象的比喻来理解：

* 符号位就像一个正负号开关（+ 或 -）
* 指数位就像是科学计数法中的"10的多少次方"
* 尾数位就像是具体的数字部分

::: {#3d2753bc-2dd0-4083-a416-8ecc5e75b093 .cell execution_count=5}
``` {.python .cell-code}
import struct
import binascii

def float_to_binary(num):
    # 将浮点数打包成二进制
    packed = struct.pack('!d', num)
    # 转换成十六进制查看
    hex_str = binascii.hexlify(packed).decode('utf-8')
    # 转换成二进制字符串
    binary = bin(int(hex_str, 16))[2:].zfill(64)
    return binary

# 查看3.14的二进制表示
binary = float_to_binary(3.14)
print(f"符号位: {binary[0]}")
print(f"指数位: {binary[1:12]}")
print(f"尾数位: {binary[12:]}")
```

::: {.cell-output .cell-output-stdout}
```
符号位: 0
指数位: 10000000000
尾数位: 1001000111101011100001010001111010111000010100011111
```
:::
:::


以上就是通过数字3.14作为例子展示浮点数的存储结构。

我们再来看看浮点数里面的一些特殊值吧

::: {#fcf895f9-20d1-4d90-a4a5-936d5daa040a .cell execution_count=6}
``` {.python .cell-code}
inf = float('inf')
print(f"正无穷大是：{inf}")
ninf = float('-inf')
print(f"负无穷大是：{ninf}")
nan = float('nan') 
print(f"非数字是：{nan}") 
```

::: {.cell-output .cell-output-stdout}
```
正无穷大是：inf
负无穷大是：-inf
非数字是：nan
```
:::
:::


:::{.callout-warning}
使用浮点数时候要特别小心精度问题。
:::

::: {#29a6a80a-c6dc-49ec-a973-6c5fd4747dcc .cell execution_count=7}
``` {.python .cell-code}
result = 0.1 + 0.2

# 打印结果
print(f"0.1 + 0.2 = {result}")

# 检查是否等于0.3
print(f"结果是否等于0.3：{result == 0.3}")

# 查看更多小数位
print(f"结果的更多小数位：{result:.17f}")
```

::: {.cell-output .cell-output-stdout}
```
0.1 + 0.2 = 0.30000000000000004
结果是否等于0.3：False
结果的更多小数位：0.30000000000000004
```
:::
:::


::: {#5843b924-0ff1-42d9-acde-bbd5b90bd530 .cell execution_count=8}
``` {.python .cell-code}
x = 0.1 + 0.2
y = 0.3
def is_close(a, b, rel_tol=1e-9):
    return abs(a-b) <= rel_tol * max(abs(a), abs(b))

print(is_close(x, y))  
```

::: {.cell-output .cell-output-stdout}
```
True
```
:::
:::


采用近似比较来解决上面的精度问题。

::: {#5363db4e-3788-4065-8997-1bac2ecfdab3 .cell execution_count=9}
``` {.python .cell-code}
price = 0.1
total = price * 3
print(total)
```

::: {.cell-output .cell-output-stdout}
```
0.30000000000000004
```
:::
:::


上面这个精度问题，可以采用`Decimal`来解决。

::: {#94847a0c-0d05-4b63-a69b-dee0d4b7faaa .cell execution_count=10}
``` {.python .cell-code}
from decimal import Decimal
price = Decimal('0.1')
total = price * 3
print(total) 
```

::: {.cell-output .cell-output-stdout}
```
0.3
```
:::
:::


## 布尔值(bool)
作为最简单的数据类型，只有`True`和`False`两种状态。
* 只有两个可能的值：True 和 False
* 用于逻辑运算和控制流
* 实际上是 int 的子类，True 等同于 1，False 等同于 0

::: {#cd8dc054-85a9-4f54-8551-b5c0ac89bfce .cell execution_count=11}
``` {.python .cell-code}
is_python_fun = True
is_coding_hard = False
```
:::


::: {#ee255ce4-fdf9-455b-b513-f208caa5ae5c .cell execution_count=12}
``` {.python .cell-code}
print(type(True))   # 输出: <class 'bool'>
print(type(False))  # 输出: <class 'bool'>
```

::: {.cell-output .cell-output-stdout}
```
<class 'bool'>
<class 'bool'>
```
:::
:::


实际上布尔值是`int`的子类，`True`等同于1, `False`等同于0.

::: {#bf6b01ba-2295-45d0-8d11-497af2e9618a .cell execution_count=13}
``` {.python .cell-code}
print(f"布尔值是整型的子类吗？ {issubclass(bool, int)}") 
```

::: {.cell-output .cell-output-stdout}
```
布尔值是整型的子类吗？ True
```
:::
:::


::: {#badbe0d2-b73e-47ec-b476-320eb9004e6d .cell execution_count=14}
``` {.python .cell-code}
print(True + 0)   
print(False + 0)  
print(True - False)  
print(False * 2)  
```

::: {.cell-output .cell-output-stdout}
```
1
0
1
0
```
:::
:::


## 复数(Complex)
Python对复数的支持非常优雅，就像是给了每个数字一个"虚数小伙伴"！我们看看他们是怎么建立的吧。

::: {#e1ba2dac-2eab-485c-83c1-549ff350fd95 .cell execution_count=15}
``` {.python .cell-code}
z1 = 3 + 4j
z2 = complex(3, 4) 
```
:::


::: {#51b0999b-4550-4fbe-95e4-8f8938665c57 .cell execution_count=16}
``` {.python .cell-code}
print(z1)
```

::: {.cell-output .cell-output-stdout}
```
(3+4j)
```
:::
:::


::: {#78611bc5-df72-4de5-a314-2634c9d1e089 .cell execution_count=17}
``` {.python .cell-code}
print(z2)
```

::: {.cell-output .cell-output-stdout}
```
(3+4j)
```
:::
:::


::: {#74584ee3-a719-4f93-abb6-f1e7cc1a38ff .cell execution_count=18}
``` {.python .cell-code}
c = 3 + 1j
print(c)
```

::: {.cell-output .cell-output-stdout}
```
(3+1j)
```
:::
:::


:::{.callout-caution}
注意3+j 在Python中必须用`3+1j`表示
:::

::: {#d50adbc1-57b5-4681-aae0-5a3c5b1623a2 .cell execution_count=19}
``` {.python .cell-code}
z1 = 1 + 2j
z2 = 3 + 4j

print(z1 + z2)    
print(z1 * z2)    
print(z1 / z2)    
print(z1 ** 2)    
```

::: {.cell-output .cell-output-stdout}
```
(4+6j)
(-5+10j)
(0.44+0.08j)
(-3+4j)
```
:::
:::


## NoneType
`None`就像是Python世界的"虚无"，它表示"什么都没有"或"不存在"。

::: {#db8d19d9-3af1-459e-b830-7798999d0c6d .cell execution_count=20}
``` {.python .cell-code}
result = None
```
:::


可以用于函数的默认返回值

::: {#82085587-7130-429c-956f-c54cdaca71e2 .cell execution_count=21}
``` {.python .cell-code}
def say_hello():
    print("Hello!")

result = say_hello()
print(say_hello())
```

::: {.cell-output .cell-output-stdout}
```
Hello!
Hello!
None
```
:::
:::


或者用于初始化。

::: {#919001e6-c535-457d-9c86-0404e4437904 .cell execution_count=22}
``` {.python .cell-code}
user_input = None
data_from_api = None
```
:::


:::{.callout-caution}
注意`None`有些场景特别容易出错。
:::

::: {#a67c01fe-25c1-4caa-8ce9-583d14374f78 .cell execution_count=23}
``` {.python .cell-code}
print(f"None是False吗？{bool(None)}")
```

::: {.cell-output .cell-output-stdout}
```
None是False吗？False
```
:::
:::


::: {#885c978d-530b-41ee-81ce-ff237f03f00a .cell execution_count=24}
``` {.python .cell-code}
print(f"None == False? {None == False}")
```

::: {.cell-output .cell-output-stdout}
```
None == False? False
```
:::
:::


::: {#69a2a771-3f15-46a8-88c7-4537458a0efd .cell execution_count=25}
``` {.python .cell-code}
print(f"None is False? {None is False}")
```

::: {.cell-output .cell-output-stdout}
```
None is False? False
```
:::
:::


::: {#9477a8a6-4291-41c9-a7f2-28375f338c6d .cell execution_count=26}
``` {.python .cell-code}
if None:
    print("这不会执行")
```
:::


::: {#e3aa2295-666a-4d76-b44d-895e39574f38 .cell execution_count=27}
``` {.python .cell-code}
empty_list = []
print(empty_list is None)
```

::: {.cell-output .cell-output-stdout}
```
False
```
:::
:::


## 字符串(str)
字符串作为Python中文本处理的基本数据格式，就像一个装文字的口袋，可以装下任何文字内容并且拥有丰富的操作方法。字符串是不可变数据，因此每次操作都会形成新的字符串。

::: {#51e74e7a-66c9-405a-818e-651c94a4fa8a .cell execution_count=28}
``` {.python .cell-code}
hello = "hello"
world = "world"
combined = hello + " " + world
print(f"{hello}的id是{id(hello)}")
print(f"{world}的id是{id(world)}")
print(f"{combined}的id是{id(combined)}")
```

::: {.cell-output .cell-output-stdout}
```
hello的id是4386131184
world的id是4397209200
hello world的id是4397211248
```
:::
:::


::: {#416adac8-7440-4376-9efc-507d10ed923a .cell execution_count=29}
``` {.python .cell-code}
multi = ''' 多行 输入
 的方法
 测试'''
```
:::


::: {#9be0859f-b4ba-4f7f-a408-21a28a52b496 .cell execution_count=30}
``` {.python .cell-code}
hello_space = hello + " "
print(f"{hello_space}的id是{id(hello_space)}")
```

::: {.cell-output .cell-output-stdout}
```
hello 的id是4397206896
```
:::
:::


### 字符串合并

::: {#8d105dc9-c3ca-49eb-a36a-7c73f8464fce .cell execution_count=31}
``` {.python .cell-code}
introduce = "indroduce" + " me"
print(introduce)
```

::: {.cell-output .cell-output-stdout}
```
indroduce me
```
:::
:::


::: {#d7398786-107d-48e4-ab84-ad1e606e14de .cell execution_count=32}
``` {.python .cell-code}
test = ["Hello", "World","c++", "PYTHON"]
sentence = ", ".join(test)
print(sentence)
```

::: {.cell-output .cell-output-stdout}
```
Hello, World, c++, PYTHON
```
:::
:::


### 重复字符串

::: {#f0ac6e3b-9fce-4e8c-9541-2941e5d2e2f1 .cell execution_count=33}
``` {.python .cell-code}
repeat = "Na" * 6 + " Batman!" * 7
print(repeat)  
```

::: {.cell-output .cell-output-stdout}
```
NaNaNaNaNaNa Batman! Batman! Batman! Batman! Batman! Batman! Batman!
```
:::
:::


### 索引与切片

切片的基本语法是:`sequence[start:stop:step]`

::: {#6f14e14f-d07f-468e-af9e-1cf651fdeb9d .cell execution_count=34}
``` {.python .cell-code}
text = "Python" 
print(text[0]) 
print(text[1:4])  
print(text[::-1]) 
```

::: {.cell-output .cell-output-stdout}
```
P
yth
nohtyP
```
:::
:::


::: {#fea879f9-fb43-4733-b151-1394346cdd06 .cell execution_count=35}
``` {.python .cell-code}
greeting = "Hello"
try:
    greeting[0] = 'h'
except TypeError as e:
    print(f"Error: {e}")
```

::: {.cell-output .cell-output-stdout}
```
Error: 'str' object does not support item assignment
```
:::
:::


### 查找与切换

::: {#4fd36eb5-1925-4588-8510-81d840309ce4 .cell execution_count=36}
``` {.python .cell-code}
sentence = "你好，这是Python课程。"
print(sentence.find("是")) 
new_sentence = sentence.replace("你", "您")
print(new_sentence)  
print(sentence)
```

::: {.cell-output .cell-output-stdout}
```
4
您好，这是Python课程。
你好，这是Python课程。
```
:::
:::


### 字符串分割

::: {#8ebbbd2d-9685-4693-9042-ab0bb13380fd .cell execution_count=37}
``` {.python .cell-code}
txt = "we have apple banana and cherry."
fruits = txt.split(" ")
print(fruits) 
print(f"这里一共有{len(fruits)}个单词")
```

::: {.cell-output .cell-output-stdout}
```
['we', 'have', 'apple', 'banana', 'and', 'cherry.']
这里一共有6个单词
```
:::
:::


### 大小写切换

::: {#8450e9e5-1054-4dad-926e-6d7ce8fd3603 .cell execution_count=38}
``` {.python .cell-code}
text = "Artificial Intelligent is fun"
print(text.upper())      
print(text.lower())     
print(text.capitalize())
```

::: {.cell-output .cell-output-stdout}
```
ARTIFICIAL INTELLIGENT IS FUN
artificial intelligent is fun
Artificial intelligent is fun
```
:::
:::


### 去除空格

::: {#2e64a194-8023-4984-acdc-c8bc7880a597 .cell execution_count=39}
``` {.python .cell-code}
text = "   Python   "
print(text.strip()) 
```

::: {.cell-output .cell-output-stdout}
```
Python
```
:::
:::


### 字符串检查

::: {#db3de415-a8e9-4516-bb20-ec8835bd3467 .cell execution_count=40}
``` {.python .cell-code}
print("Python".startswith("Py"))  
print("Oth".isdigit())            
```

::: {.cell-output .cell-output-stdout}
```
True
False
```
:::
:::


::: {#efafbbde-7f7f-467e-977a-53e16a5268ce .cell execution_count=41}
``` {.python .cell-code}
text = "Hello, world"
print(text.endswith("word"))
```

::: {.cell-output .cell-output-stdout}
```
False
```
:::
:::


::: {#5c95a7af-6410-40bf-a8ce-d4c9a7c80e1f .cell execution_count=42}
``` {.python .cell-code}
text = "abc"
print(text.isalpha())
```

::: {.cell-output .cell-output-stdout}
```
True
```
:::
:::


### 字符串格式化
Python的字符串格式化有这么几种：

* %符号

::: {#b90296b0-2213-4285-b4a2-30059ebaabe8 .cell execution_count=43}
``` {.python .cell-code}
name = "Tom"
age = 22
formatted = "My name is %s and I am %d years old." %(name, age)
print(formatted)
```

::: {.cell-output .cell-output-stdout}
```
My name is Tom and I am 22 years old.
```
:::
:::


* `format()`方法

::: {#6ad331d1-847d-42b2-808f-040a73b82a21 .cell execution_count=44}
``` {.python .cell-code}
# 使用 format() 方法
name = "Alice"
age = 30
print("My name is {} and I'm {} years old".format(name, age))
```

::: {.cell-output .cell-output-stdout}
```
My name is Alice and I'm 30 years old
```
:::
:::


* f-strings由Python 3.6引入的最便捷的字符串格式方法

::: {#ad6ba62e-d478-40ff-b554-029f76c92143 .cell execution_count=45}
``` {.python .cell-code}
name = "Judy"
age = 40
country = "USA"
print(f"My name is {name} and I'm {age} years old from {country}")
```

::: {.cell-output .cell-output-stdout}
```
My name is Judy and I'm 40 years old from USA
```
:::
:::


::: {#1d01e93a-6ea2-447e-8ad0-8a30ea021a60 .cell execution_count=46}
``` {.python .cell-code}
pi = 3.1415926
print(f"Pi is {pi:.3f}")
```

::: {.cell-output .cell-output-stdout}
```
Pi is 3.142
```
:::
:::


到此我们可以回顾一下Python的主要数据类型，如下表。

| 数据类型  | 描述  | 是否可变  | 示例 |
|--------- |------|---------|------|
| 整数 (int) | 表示整数 | 否 | `42`, `-10`, `0` |
| 浮点数 (float) | 表示小数 | 否 | `3.14`, `-0.001`, `2.0e-3` |
| 布尔 (bool) | 表示真或假 | 否 | `True`, `False` |
| 字符串 (str) | 表示文本 | 否 | `"Hello"`, `'Python'` |
| 复数 (complex) | 表示复数 | 否 | `3+4j`, `2-1j` |
| NoneType | 表示空值 | 不适用 | `None` |

下面让我们开始设计我们的奶茶店"Python奶茶屋",先看看这些基本数据类型能帮我们做些什么?
1. 订单备注 - 记录客人的各种特殊要求，就像给奶茶贴上的小纸条。
2. 账单系统 - 包括今日订单总数，今日应收，平均评分。
3. 检查状态 - 包括订单状态，是否放冰，是否放糖，是否线上订单。

