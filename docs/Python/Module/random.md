# random 模块

> 计算机伪随机数是由梅森旋转算法生成的伪随机序列中的元素。
>

```python
import random

random.seed(10)  # 设置种子，使得后面的随机是可以再现的
random.random()  # 不给种子的话（不加random.seed()语句），默认使用系统时间作为种子
random.randint(10,100)  # 生成一个[a,b]之间的整数
random.randrange(10,100,10)  # 生成一个[m,n]之间以k为步长的随机整数
random.getrandbits(16)  # 生成一个k比特长的随机整数
random.uniform(10,100)  # 生成一个[a,b]之间的随机小数
random.choice([1,2,3,5,6,7]) # 从序列seq中随机选择一个元素
s=[1,2,3,5,6,7]
random.shuffle(s)  # 将序列seq中的元素随机排列，返回打乱后的序列
```

| 函数                                 | 描述                                              |
| ------------------------------------ | ------------------------------------------------- |
| random.seed(a=None)                  | 初始化随机种子，默认值为当前系统时间              |
| random.random()                      | 生成一个[0.0, 1.0)之间的随机小数                  |
| random.randint(a, b)                 | 生成一个[a, b]之间的随机整数                      |
| random.getrandbits(k)                | 生成一个 k 比特长度的随机整数                     |
| random.randange(start, stop[, step]) | 生成一个[start, stop)之间以 step 为步数的随机整数 |
| random.uniform(a, b)                 | 生成一个[a, b]之间的随机小数                      |
| random.choice(seq)                   | 从序列类型随机返回一个元素，比如列表              |
| random.shuffle(seq)                  | 将序列类型中的元素随机排列，返回打乱后的序列      |
| random.sample(pop, k)                | 从 pop 类型中随机选取 k 个元素，以列表的类型返回  |
