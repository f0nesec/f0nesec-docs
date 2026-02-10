# hashlib

## 模块介绍

> 1. 这个模块针对许多不同的安全哈希和消息摘要算法实现了一个通用接口。
> 2. 什么是哈希(Hash)? 哈希，是把任意长度的输入通过散列算法变换成固定长度的输出，简单的说就是通过
>    函数，将明文数据通过变成密文数据达到加密的作用。
> 3. 每种类型的 hash 都有一个构造器方法，它们都返回一个具有相同的简单接口的 hash 对象。 例如，使
>    用 sha256() 创建一个 SHA-256 hash 对象。
> 4. 然后使用 update() 方法向这个对象输入' 字节类对象 (通常是 bytes) '。在任何时候你都可以使用
>    digest() 或 hexdigest() 方法获得到目前为止输入这个对象的拼接数据的 digest。

## hashilib 构造器

> 1. 此模块中常见 hash 算法构造器
>    sha1(), sha224(), sha256(), sha384(), sha512(), blake2b()，blake2s()，md5()。
>
> 2. 在大部分平台上可用的还有
>    sha3_224(), sha3_256(), sha3_384(), sha3_512(), shake_128(), shake_256() 等等。

```python
"""如果需要获取构造器对象，我们可以直接引入模块 hashilib 后用点的方式生成，如下实例:

代码示例
		import hashlib

		h = hashlib.md5()
		print(h)
打印结果
		<md5 _hashlib.HASH object @ 0x00000233D317EAD0>

示例以 md5 为例，在模块名后用点的方式找到需要的算法构造器名称即可生成算法构造器对象。
"""

import hashlib

# 什么都不传递通过hexdigest()获取对应的值，此时值为空对应的hash MD5值
test = hashlib.md5().hexdigest()
print(test)  # d41d8cd98f00b204e9800998ecf8427e
```

## hashlib.new() 创建对象

```python
import hashlib

# 通过new()方法创建对象,在 new() 括号中输入哈希构造器算法构造器的名称字符串相当于调用了构造器创建了一个对象。
# 语法：语法格式 hashlib.new(name, [data, ]*, usedforsecurity=True)
test = hashlib.new("md5").hexdigest()
print(test)  # d41d8cd98f00b204e9800998ecf8427e
```

## 传入参数以及获取值

```python
import hashlib

# hash.digest_size 以字节表示的结果哈希对象的大小。
test = hashlib.md5().digest_size
print(test)  # 16

# hash.block_size 以字节表示的哈希算法的内部块大小。
test = hashlib.md5().block_size
print(test)  # 64

# hash.digest() 返回字节串对象
test = hashlib.md5()
test.update(b"123")
test.update(b"456")
print(test.digest())  # b'\xe1\n\xdc9I\xbaY\xab\xbeV\xe0W\xf2\x0f\x88>'

# hash.update() 传入加密对象
test = hashlib.new("md5")
test.update(b"123456")
print(test.hexdigest())  # e10adc3949ba59abbe56e057f20f883e
# 可以分开进行传递，使用md5和new等价
test = hashlib.md5()
test.update(b"123")
test.update(b"456")
print(test.hexdigest())  # e10adc3949ba59abbe56e057f20f883e
```

## 加盐，升级加密

数据被加密后是不能被直接解密的，网站上的解密一般都是暴力解密，不断地在猜在试有可能得出结果，我们还可以通过加盐操作来提高破解数据的难度，加盐其实就是在真正要被加密的数据中添加其他数据。

```python
import hashlib

# 使用md5加密
test = hashlib.new("md5")
# 实际需要加密的数据
test.update("123456".encode('utf-8'))
print(test.hexdigest())  # e10adc3949ba59abbe56e057f20f883e
# 在后面添加一个1，最终加密的字符为1234561
test.update(b"1")
print(test.hexdigest())  # aaa42296669b958c3cee6c0475c8093e

# 当然可以将盐设置为动态的比如时间只需要修改第二个update
# aa可以设置动态的
aa = "1234"
test = hashlib.new("md5")
test.update("123456".encode('utf-8'))
test.update(aa.encode('utf-8'))
print(test.hexdigest())
```
