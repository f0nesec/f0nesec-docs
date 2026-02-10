# re 模块

> Python 正则表达式库。
>

## 1.1 正则表达式基础语法

**元字符：** 具有固定含义的字符，只可以匹配单个字符。

**常用元字符：**

```python
.					匹配除换行符以外的任意字符
\w				匹配字母或数字或下划线
\s				匹配任意的空字符
\d				匹配数字
\n				匹配换行符
\t				匹配制表符

^					匹配字符串的开始
$					匹配字符串的结尾

\W				匹配非字母、数字、下划线
\D				匹配非数字
\S				匹配非空白符
a|b				匹配字符a或者字符b
()				匹配括号内的表达式，也表示一个组
[...]			匹配字符组中的字符
[^...]		不配皮除了字符组的所有字符
```

**量词：** 控制元字符出现的次数。

```python
*				重复零次或更多次
+				重复一次或更多次
?				重复零次或一次
{n}			重复n次
{n,}		重复n次或更多次
{n, m}	重复n到m次
```

**贪婪匹配和惰性匹配：**

```python
.*		贪婪匹配
.*?		惰性匹配
```

## 2.1 re 模块语法

**大多数用到的方法是：** findall、search、match、findite。

**search 和 match 区别于：** match 只匹配字符串的开始，如果字符串开始不符合正则表达式，则匹配失败，函数返回 None；而 search 匹配整个字符串，直到找到一个匹配，并且这两种方法只匹配一次。

**findall 和 findite 区别：** findall 匹配返回元组或列表，而 findite 返回一个迭代器。

### 2.1.1 正则表达式修饰符 - 可选标志

正则表达式可以包含一些可选标志修饰符来控制匹配的模式。修饰符被指定为一个可选的标志。多个标志可以通过按位 `OR(|)` 它们来指定。如 `re.I | re.M` 被设置成 I 和 M 标志：

| 修饰符 | 描述                                                                        |
| :----- | :-------------------------------------------------------------------------- |
| re.I   | 忽略大小写                                                                  |
| re.L   | 表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境                        |
| re.M   | 多行匹配，影响 ^ 和 $                                                       |
| re.S   | 即为 **.** 并且包括换行符在内的任意字符（**.** 不包括换行符）               |
| re.U   | 表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库 |
| re.X   | 为了增加可读性，忽略空格和 **#** 后面的注释                                 |

### 2.1.2 re.compile 方法

compile 函数用于编译正则表达式，生成一个正则表达式 Pattern 对象，供函数使用。

**语法格式为：** `re.compile(pattern[, flags])`

**参数：**

- **pattern** : 一个字符串形式的正则表达式.
- **flags** : 可选，表示匹配模式，比如忽略大小写，多行模式等，具体参数参考正则表达式修饰符 2.1.1.

```python
>>>import re
>>> c = re.compile(r'\d+')                    # 用于匹配至少一个数字
>>> m = pattern.match('one12twothree34four')        # 查找头部，没有匹配
>>> print (m)
None
>>> m = pattern.match('one12twothree34four', 2, 10) # 从'e'的位置开始匹配，没有匹配
>>> print (m)
None
>>> m = pattern.match('one12twothree34four', 3, 10) # 从'1'的位置开始匹配，正好匹配
>>> print (m)                                         # 返回一个 Match 对象
<_sre.SRE_Match object at 0x10a42aac0>
>>> m.group(0)   # 可省略 0
'12'
>>> m.start(0)   # 可省略 0
3
>>> m.end(0)     # 可省略 0
5
>>> m.span(0)    # 可省略 0
(3, 5)
```

在上面，当匹配成功时返回一个 Match 对象，其中：

- `group([group1, …])` 方法用于获得一个或多个分组匹配的字符串，当要获得整个匹配的子串时，可直接使用 `group()` 或 `group(0)`；
- `start([group])` 方法用于获取分组匹配的子串在整个字符串中的起始位置（子串第一个字符的索引），参数默认值为 0；
- `end([group])` 方法用于获取分组匹配的子串在整个字符串中的结束位置（子串最后一个字符的索引`+1`），参数默认值为 0；
- `span([group])` 方法返回 `(start(group), end(group))`。

### 2.1.3 re.match 方法

re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match() 就返回 none。

**语法：** `re.match(pattern, string, flags=0)`

函数参数说明：

| 参数    | 描述                                                                                                         |
| :------ | :----------------------------------------------------------------------------------------------------------- |
| pattern | 匹配的正则表达式                                                                                             |
| string  | 要匹配的字符串。                                                                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等，具体参数参考正则表达式修饰符 2.1.1。 |

匹配成功 re.match 方法返回一个匹配的对象，否则返回 None。

我们可以使用 group(num) 或 groups() 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述                                                                                                       |
| :----------- | :--------------------------------------------------------------------------------------------------------- |
| group(num=0) | 匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
| groups()     | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。                                                   |

```python
import re
print(re.match('www', 'www.runoob.com').span())  # 在起始位置匹配  (0, 3)
print(re.match('com', 'www.runoob.com'))         # 不在起始位置匹配 None

line = "Cats are smarter than dogs"
matchObj = re.match(r'(?P<name>.*) are (.*?) .*', line, re.M | re.I)
print(matchObj.groups())  # ('Cats', 'smarter') 元组格式输出代括号内匹配的内容
print(matchObj.group())   # 默认使用group输出第0个正则匹配的内容，0，1，2，也是对应的匹配结果
# 直接使用group()等价于group(0)
print(matchObj.group(1))  # Cats
print(matchObj.group(2))  # smarter

# 如果在括号内使用(?P<name>.*?)，此时使用group('name')可直接打印对应位置的匹配字符串
print(matchObj.group('name'))  # Cats
```

### 2.1.4 re.search 方法

re.search 扫描整个字符串并返回第一个成功的匹配。

**语法：** `re.search(pattern, string, flags=0)`

**函数参数说明：**

| 参数    | 描述                                                                                                         |
| :------ | :----------------------------------------------------------------------------------------------------------- |
| pattern | 匹配的正则表达式                                                                                             |
| string  | 要匹配的字符串。                                                                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等，具体参数参考正则表达式修饰符 2.1.1。 |

匹配成功 re.search 方法返回一个匹配的对象，否则返回 None。

我们可以使用 group(num) 或 groups() 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述                                                                                                       |
| :----------- | :--------------------------------------------------------------------------------------------------------- |
| group(num=0) | 匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
| groups()     | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。                                                   |

```python
import re
print(re.search('www', 'www.runoob.com').span())  # 在起始位置匹配  (0, 3)
print(re.search('com', 'www.runoob.com').span())  # 不在起始位置匹配 (11, 14)

line = "Cats are smarter than dogs"
searchObj = re.search(r'(?P<name>.*) are (.*?) .*', line, re.M | re.I)
print(searchObj.groups())  # ('Cats', 'smarter') 元组格式输出代括号内匹配的内容
print(searchObj.group())   # 默认使用group输出第0个正则匹配的内容，0，1，2，也是对应的匹配结果
# 直接使用group()等价于group(0)
print(searchObj.group(1))  # Cats
print(searchObj.group(2))  # smarter

# 如果在括号内使用(?P<name>.*?)，此时使用group('name')可直接打印对应位置的匹配字符串
print(searchObj.group('name'))  # Cats
```

### 2.1.5 re.findall 方法

**findall：** 在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果有多个匹配模式，则返回元组列表，如果没有找到匹配的，则返回空列表，多匹配模式只在一个匹配过程中，正则语句存在多个匹配项，该过程会返回元组。

**语法：** `findall(string[, pos[, endpos]])`

**参数：**

- **string** : 待匹配的字符串。
- **pos** : 可选参数，指定字符串的起始位置，默认为 0。
- **endpos** : 可选参数，指定字符串的结束位置，默认为字符串的长度。

```python
import re
# 一个匹配项
f  # 创建一个正则公式，匹配数字
result1 = pattern.findall('runoob 123 google 456')
result2 = pattern.findall('run88oob123google456', 0, 10)
print(result1)  # ['123', '456']
print(result2)  # ['88', '12']

# 多个匹配项，返回元组
result = re.findall(r'(\w+)=(\d+)', 'set width=20 and height=10')
print(result)  # [('width', '20'), ('height', '10')]
```

### 2.1.6 re.findite 方法

findite 和 findall 类似，在字符串中找到正则表达式所匹配的所有子串，并把它们作为一个迭代器返回。

**语法：** `re.finditer(pattern, string, flags=0)`

**参数：**

| 参数    | 描述                                                                                                         |
| :------ | :----------------------------------------------------------------------------------------------------------- |
| pattern | 匹配的正则表达式                                                                                             |
| string  | 要匹配的字符串。                                                                                             |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等，具体参数参考正则表达式修饰符 2.1.1。 |

```python
import re

it = re.finditer(r"\d+","12a32bc43jf3")
for match in it:
    print (match.group() )
# 12
# 32
# 43
# 3
```

### 2.1.7 检索和替换 re.sub 方法

Python 的 re 模块提供了`re.sub`用于替换字符串中的匹配项。

**语法：** `re.sub(pattern, repl, string, count=0, flags=0)`

**参数：**

- **pattern :**  正则中的模式字符串。
- **repl :** 替换的字符串，也可为一个函数。
- **string :** 要被查找替换的原始字符串。
- **count :** 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。

```python
import re

phone = "2004-959-559 # 这是一个国外电话号码"

# 删除字符串中的 Python注释
num = re.sub(r'#.*$', "", phone)
print("电话号码是: ", num)  # 电话号码是:  2004-959-559

# 删除非数字(-)的字符串
num = re.sub(r'\D', "", phone)
print("电话号码是 : ", num)  # 电话号码是 :  2004959559
```

repl 参数是一个函数。

```python
import re


# 将匹配的数字乘以 2
def double(matched):
    value = int(matched.group('value'))
    return str(value * 2)


s = 'A23G4HFD567'
print(re.sub('(?P<value>\d+)', double, s))  # A46G8HFD1134
```

### 2.1.8 re.split 方法

split 方法按照能够匹配的子串将字符串分割后返回列表。

**语法：** `re.split(pattern, string[, maxsplit=0, flags=0])`

**参数：**

| 参数     | 描述                                                                                                         |
| :------- | :----------------------------------------------------------------------------------------------------------- |
| pattern  | 匹配的正则表达式                                                                                             |
| string   | 要匹配的字符串。                                                                                             |
| maxsplit | 分隔次数，maxsplit=1 分隔一次，默认为 0，不限制次数。                                                        |
| flags    | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等，具体参数参考正则表达式修饰符 2.1.1。 |

```python
>>>import re
>>> re.split('\W+', 'runoob, runoob, runoob.')
['runoob', 'runoob', 'runoob', '']
>>> re.split('(\W+)', ' runoob, runoob, runoob.')
['', ' ', 'runoob', ', ', 'runoob', ', ', 'runoob', '.', '']
>>> re.split('\W+', ' runoob, runoob, runoob.', 1)
['', 'runoob, runoob, runoob.']

>>> re.split('a*', 'hello world')   # 对于一个找不到匹配的字符串而言，split 不会对其作出分割
['hello world']
```

## 2.2 正则表达式对象

### 2.1.1 re.RegexObject

`re.compile() ` 返回 RegexObject 对象。

### 2.1.2 re.MatchObject

`group() `返回被 RE 匹配的字符串。

- **start()** 返回匹配开始的位置
- **end()** 返回匹配结束的位置
- **span()** 返回一个元组包含匹配 (开始,结束) 的位置
