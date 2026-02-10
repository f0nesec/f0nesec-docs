# pathlib 模块

> pathlib 是 Python3.4 之后新添加的模块，它可以让文件和路径操作变得快捷方便，完美代替 ` os.path` 模块。
>
> 该模块提供了用于表示文件系统路径的类，适用于不同的操作系统。路径类被分为提供纯计算操作而不涉及` I/O` 的 `PurePath`，以及从纯路径继承而来但提供 `I/O `操作的` Path`。

## 模块解析

### 路径查询

```python
# 导入模块
from pathlib import Path

# 获取当前路径的绝对路径
Path.cwd()

# 路径对象，用于对路径进行操作
# 生成路径对象，直接传入Path中
p = Path("/Users/luckyx/Desktop/code/1_idea_code")
# 可以使用拼接创建新的路径对象
q = p / "1.txt"

# 判断路径是否为一个文件夹
p.is_dir()  # --> True
q.is_dir()  # --> False

# 判断路径是否为一个文件
p.is_file()  # --> False
q.is_file()  # --> True

# 判断路径是否存在
p.exists()  # --> True

# 获取路径的最后一个部分
p.name  # --> 1_idea_code
q.name  # --> 1.txt

# 获取文件的文件名，如果是路径则返回路径名，文件则返回文件名
p.stem  # --> 1_idea_code
q.stem  # --> 1

# 获取文件后缀，如果是目录则返回空，如果是文件则返回文件后缀
p.suffix  # -->
q.suffix  # --> .txt

# 获取其父级目录，是绝对路径
p.parent  # --> /Users/luckyx/Desktop/code
q.parent  # --> /Users/luckyx/Desktop/code/1_idea_code
  # 使用parents可以获取父目录的所有目录的可迭代对象
  for i in p.parents:
    print(i)
  # /Users/luckyx/Desktop/code
  # /Users/luckyx/Desktop
  # /Users/luckyx
  # /Users
  # /
  # 当然也支持索引功能，超过索引范围会抛出异常
  p.parents[0]  # --> /Users/luckyx/Desktop/code
  p.parents[1]  # --> /Users/luckyx/Desktop
  p.parents[2]  # --> /Users/luckyx

# 将路径的各个组间拆分成元组
p.parts  # --> ('/', 'Users', 'luckyx', 'Desktop', 'code', '1_idea_code')

# 查询文件或者文件夹的状态信息
# 1>访问时间（access time 简写为atime）
# 2>修改时间（modify time 简写为mtime）
# 3>状态修改时间(change time 简写为ctime)
p.stat()  # --> os.stat_result(st_mode=16877, st_ino=48375226, st_dev=16777230, st_nlink=10, st_uid=501, st_gid=20, st_size=320, st_atime=1683783723, st_mtime=1683783723, st_ctime=1683783723)
	# 可以通过下表获取对应的值
  p.stat().st_size  # 获取文件或文件夹大小 --> 320

# 相对路径
test = Path("./doc")  # 当前路径的doc目录
test1 = Path("../doc")  # 当前路径的上一级doc目录
	# 将相对路径转换成绝对路径
  test.resolve()  # --> /Users/luckyx/Desktop/code/1_idea_code/doc
	# 获取当前路径下的子文件和子文件夹，只能获取当前路径下的，获取不到全部的子文件夹和子文件
  test.iterdir()  # 是一个生成器，如果没有子文件和子文件夹则为空
  # 将当前路径下所有文件整理成一个列表，使用推导式
  [i for i in test.iterdir() if i.is_file()]
```

### 路径修改

```python
from pathlib import Path

# 创建路径对象
p = Path("/Users/luckyx/Desktop/code/1_idea_code/test")

# 创建文件夹，需要提前创建路径对象
p.mkdir()  # 创建test文件夹
	# 如果创建的文件夹已经存在，那么再次创建就会抛出异常，使用关键字参数可以避免该异常
  p.mkdir(exist_ok=True)
  # 如果路径有存在多个不存在的路径，直接创建同样会抛出异常，使用关键字也可以避免该异常
  p.mkdir(parents=True)

# Path内部打包了open函数可以直接对文件进行打开关闭写入操作
q = p / "1.txt"
f = q.open("w")  # 此时可以对1.txt进行文件操作

# 对文件或文件夹修改名字，注意此时修改的名字需要添加相对路径或绝对路径，不然程序运行后会将文件保存到项目目录
q.rename("/Users/luckyx/Desktop/code/1_idea_code/test/2.txt")

# 替换指定的文件或文件夹，同样需要指定路径，不然会保留到项目目录
q.replace("/Users/luckyx/Desktop/code/1_idea_code/test/a/b/33.txt")

# 删除操作
# 删除文件夹，如果文件夹有文件，直接删除会报错
q.parent.rmdir()  # --> 目录存在文件，无法进行删除，此时需要先使用文件删除在进行目录删除
q.unlik()					# --> 先对目录下的文件进行删除
q.parent.rmdir()  # --> 删除父目录
```

### 查找功能

```python
from pathlib import Path

# 创建路径对象
p = Path(".")  # --> 当前路径

# 查找当前路径的所有txt文件，返回的是一个迭代器，可以存入列表中，也可以迭代输出
p.glob("*.txt")

# 查找当前路径的下一级路径的所有txt文件
p.glob("*/*.txt")

# 查找当前目录以及向下的所有子目录txt文件
p.glob("**/*.txt")
```

## 示例

```python
# 在 pathlib 模块中，Path 对象有一个 glob() 方法，它提供了向下递归搜索的能力（如下），请自己编写一个递归函数，实现相同的搜索功能

from pathlib import Path

p = Path.cwd()
file = []


def test(pat, list_data, a):
    for i in pat.iterdir():
        if i.is_file() and i.suffix == a:
            list_data.append(i)
        if i.is_dir():
            test(i, list_data, a)
    return list_data


s = test(p, file, '.py')
print(s)
```
