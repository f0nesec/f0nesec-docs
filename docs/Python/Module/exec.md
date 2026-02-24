# exec 模块

> exec 用于执行一个字符串形式的 Python 语句或代码对象。
>

## 模块解析

如果 object 参数指定的是一个字符串，那么该字符串将被作为 Python 语句解析并执行（除非遇到语法错误）；如果该参数指定的是一个代码对象，那么将直接被执行。

globals 参数管理的是一个全局命名空间，如果只是提供了 globals 参数，但不包含以 **builtins** 为键的值，则会在解析表达式之前，将当前环境中的 **builtins** 添加到 globals 中。

locals 参数管理的是一个局部命名空间，和 globals 类似，但当它和 globals 参数中如果存在有重复或冲突时，locals 拥有更高的优先级。

如果 globals 参数和 locals 参数均没有指定，则使用 Python 的全局和局部命名空间。

注意：即使在传递给 exec() 函数的代码上下文中，也不能在函数定义之外使用 nonlocal、yield 和 return 语句。

## 语法

```python
exec(object, globals=None, locals=None, /)
```

**参数解析：**

| **参数** | **含义**                                                             |
| -------- | -------------------------------------------------------------------- |
| object   | 指定一个将被作为 Python 语句解析并执行的字符串；或者指定一个代码对象 |
| globals  | 可选参数，该参数必须是一个字典类型，管理一个全局的命名空间           |
| locals   | 可选参数，该参数可以是任何映射对象，管理一个局部的命名空间           |

**返回值：**

该函数的返回值为 None。

## 代码示例

```python
>>> # exec() 返回值总是 None；eval() 函数将返回表达式的计算结果
>>> exec("1 + 2")
>>> eval("1 + 2")
3
>>> # exec() 执行的是语句；eval() 执行的是表达式（如果给它一个语句就会报错）
>>> exec("a = 3")
>>> a
3
>>> eval("a = 3")
Traceback (most recent call last):
  File "<pyshell#53>", line 1, in <module>
    eval("a = 3")
  File "<string>", line 1
    a = 3
      ^
SyntaxError: invalid syntax
>>> # exec() 还支持多个语句（使用分号分隔）
>>> exec("a = 1; b = 2")
>>> a
1
>>> b
2
```
