# decimal 模块

> decimal 库提供了对十进制小数的精确支持，特别适用于财务、科学和其他需要精确小数计算的领域。

- **导入库：** `import decimal` 。
- **创建十进制对象：** `decimal.Decimal(value)`，参数为字符串或数字 `value` 。
- **进行十进制运算：** `+、-、*、/、//、%、** ` 。
- **设置十进制上下限：** `decimal.getcontext().prec `和 `decimal.getcontext().rounding` 。

## 代码示例

```python
import decimal

# 创建十进制对象
a = decimal.Decimal('0.1')
b = decimal.Decimal('0.2')

# 进行十进制运算
result = a + b
print(result) # 0.3

# 设置十进制精度
decimal.getcontext().prec = 4

# 设置十进制四舍五入方式
decimal.getcontext().rounding = decimal.ROUND_HALF_UP

# 进行十进制运算
result = a / b
print(result) # 0.5
```