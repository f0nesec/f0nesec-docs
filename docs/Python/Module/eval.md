#  eval 模块

> eval 用于执行一个字符串形式的 Python 表达式。
>

## 模块解析

globals 参数管理的是一个全局命名空间，如果只是提供了 globals 参数，但不包含以 **builtins** 为键的值，则会在解析表达式之前，将当前环境中的 **builtins** 添加到 globals 中。

locals 参数管理的是一个局部命名空间，和 globals 类似，但当它和 globals 参数中如果存在有重复或冲突时，locals 拥有更高的优先级。

如果 globals 参数和 locals 参数均没有指定，则使用 Python 的全局和局部命名空间。

## 语法

```python
eval(expression, globals=None, locals=None, /)
```

**参数解释：**

| **参数**   | **含义**                                                   |
| ---------- | ---------------------------------------------------------- |
| expression | 指定一个将被作为 Python 表达式解析并执行的字符串           |
| globals    | 可选参数，该参数必须是一个字典类型，管理一个全局的命名空间 |
| locals     | 可选参数，该参数可以是任何映射对象，管理一个局部的命名空间 |

**返回值：**

返回执行的结果。

## 代码示例

```python
>>> # 将字符串作为 Python 表达式来执行
>>> eval("1 + 2")
>>> 3
>>> # 也被称为是 repr() 的反函数
>>> eval(repr("I love FishC"))
'I love FishC'
>>> eval(repr([1, 1, 2, 3, 5]))
[1, 1, 2, 3, 5]
>>> # 通过 globals 指定全局命名空间
>>> eval("F + C")
Traceback (most recent call last):
  File "<pyshell#17>", line 1, in <module>
    eval("F + C")
  File "<string>", line 1, in <module>
NameError: name 'F' is not defined
>>> eval("F + C", {'F':70, 'C':67})
137
>>> # 如果同时指定 globals 和 locals，则后者的优先级更高
>>> eval("F + C", {'F':70, 'C':67}, {'F':'f', 'C':'c'})
'fc'
>>> # 默认 __builtins__ 内置命名空间将被导入到 globals 中，除非将其设置为 None
>>> eval("sum([1, 2, 3])")
6
>>> eval("sum([1, 2, 3])", {'__builtins__':None})
Traceback (most recent call last):
  File "<pyshell#22>", line 1, in <module>
    eval("sum([1, 2, 3])", {'__builtins__':None})
  File "<string>", line 1, in <module>
TypeError: 'NoneType' object is not subscriptable
>>> # 还可以 “狸猫换太子”，但这种做法不可取
>>> eval("sum([1, 2, 3])", {'sum':print})
[1, 2, 3]
```
