# json 模块

> 同通过 Python 实现 json 编码和解码。

## 模块解析

**json：** 是一种轻量级的数据交换格式，易于人阅读和编写。

- **json.dumps()：** 用于将 Python 对象编码成 json 字符串，不加 s 表示对文件进行操作。
- **json.loads()：** 用于解码 json 数据，该函数返回 python 字段的数据类型，不加 s 表示对文件进行操作。

**注意：** 将 json 字符串转成 python 数据类型字段会发生改变。

| JSON          | Python    |
| :------------ | :-------- |
| object        | dict      |
| array         | list      |
| string        | unicode   |
| number (int)  | int, long |
| number (real) | float     |
| true          | True      |
| false         | False     |
| null          | None      |

## 示例

```python
import json


# load/loads
# load
with open("test.txt", "r") as f:
    print(json.load(f))
a = {"a": "b", "c": "3"}
print(json.loads(a))

# dump.dumps
with open("test.txt", "r") as f:
    print(json.dump(f))
a = {"a": "b", "c": "3"}
print(json.dump(a))
```
