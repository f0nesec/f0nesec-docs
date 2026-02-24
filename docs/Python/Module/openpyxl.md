# openpyxl 模块

> OpenPyXl 是一个第三方的 Python 模块，用于读取和修改 `.xlsx` 格式的 `Excel `文件。
>

## 模块解析

### **打开 xlsx 文件**

```python
import openpyxl
wb_old = openpyxl.load_workbook("D:/old.xlsx")
wb_old = openpyxl.load_workbook("D:/old.xlsx", read_only=True) # 以只读模式打开
```

### **新建 xlsx 文件**

```python
import openpyxl

wb = openpyxl.Workbook()							# 新建工作薄默认新建一张sheet表

ws0 = wb.create_sheet()               # 创建一个新表，新表依次被命名为 Sheet, Sheet1, Sheet2, …
ws1 = wb.create_sheet("Newsheet")     # 创建一个名为 Newsheet 的新表，将新表插在最后
ws2 = wb.create_sheet("Newsheet", 0)  # 将新表插在第一的位置。工作表的 index 从 0 开始
ws3 = wb.create_sheet("Newsheet", 1)  # 将新表插在第二的位置
ws4 = wb.create_sheet("Newsheet", -1) # 将新表插在倒数第一的位置，即插入完成后的倒数第二个

wb.save("D:/new.xlsx")								# 保存工作薄
```

**注意：** 使用 `load_workbook() `打开的工作簿也可以使用`save()`方法保存。如果未设置只读，且保存时使用原文件名保存在原路径，则保存时会将修改写入到原文件。

### **编辑 xlsx 表格**

```python
ws = wb["Sheet"]  # 与字典获取值的方法相同，先获取工作薄对象默认为第一个sheet
ws = wb.active		# 获取活动工作表，用户下一步对工作表进行增删改查
wb.remove(ws)			# 删除工作表
name = ws.title   # 获取工作表的名字
ws.title = "New Title"   # 工作表重命名

# 工作表包含数据的最小行、最大行、最小列、最大列
ws.min_row    # 这四个都是整数类型
ws.max_row
ws.min_column
ws.max_column

wb.cell(row=1, column=1, value='索引') # 插入数据到单元格
```
