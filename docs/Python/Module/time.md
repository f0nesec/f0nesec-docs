# time 模块

> 时间的访问和转换，每个时间戳都以自从 1970 年 1 月 1 日午夜（历元）经过了多长时间来表示。
>

```python
import time

# 添加时间延时10s
time.sleep(10)

# 获取时间戳
localtime = time.time()
print(localtime)
## 1684065138.333071

# 时间戳转换成秒
print(int(localtime))

#毫秒级时间戳
print (int(round(t * 1000)))
```

```python
import time

# 获取当前时间返回为元组
localtime = time.localtime(time.time())
print(localtime)
## time.struct_time(tm_year=2023, tm_mon=5, tm_mday=14, tm_hour=19, tm_min=52, tm_sec=18, tm_wday=6, tm_yday=134, tm_isdst=0)
```

![](https://relay-img.f0nesec.top/python/time.png)

```python
import time

# 获取格式化时间
localtime = time.asctime( time.localtime(time.time()) )
print(localtime)
## Sun May 14 19:57:22 2023

# 获取格式化日期
import time

# 格式化成2016-03-20 11:45:39形式 这种很常用
localtime = time.time()
print(time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(localtime)))

# 格式化成Sat Mar 28 22:24:24 2016形式
print(time.strftime("%a %b %d %H:%M:%S %Y", time.localtime(localtime)))

# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print(time.mktime(time.strptime(a, "%a %b %d %H:%M:%S %Y")))
```

```python
# 获取某月日历使用 calendar模块
import calendar

cal = calendar.month(2016, 1)
print("以下输出2016年1月份的日历:")
print(cal)
```
