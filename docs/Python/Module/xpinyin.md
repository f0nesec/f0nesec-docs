# xpinyin 模块

> 该模块用于将汉字转换成拼音。
>

```python
>>> from xpinyin import Pinyin
>>> p = Pinyin()
>>>
>>> # 获取中文字符串的对应拼音
>>> p.get_pinyin("小甲鱼")
'xiao-jia-yu'
>>>
>>> # 显示声调
>>> p.get_pinyin("小甲鱼", tone_marks="marks")
'xiǎo-jiǎ-yú'
>>>
>>> # 将声调用显示为数字1、2、3、4
>>> p.get_pinyin("小甲鱼", tone_marks="numbers")
'xiao3-jia3-yu2'
>>>
>>> # 移除分隔符
>>> p.get_pinyin("小甲鱼", "")
'xiaojiayu'
>>>
>>> # 指定分隔符
>>> p.get_pinyin("小甲鱼", "^")
'xiao^jia^yu'
>>>
>>> # 获取拼音第一个字母
>>> p.get_initial("小")
'X'
>>> p.get_initials("小甲鱼")
'X-J-Y'
>>> p.get_initials("小甲鱼", "")
'XJY'
>>> p.get_initials("小甲鱼", "^")
'X^J^Y'
>>>
>>> # 获取声母（包含翘舌音）
>>> p.get_initials("上海自来水来自海上", with_retroflex=True)
'SH-H-Z-L-SH-L-Z-H-SH'
>>>
>>> # 多音字组合
>>> p.get_pinyins("模型", tone_marks="marks")
['mó-xíng', 'mú-xíng']
>>> p.get_pinyins("模样", tone_marks="marks")
['mó-yáng', 'mó-yàng', 'mó-xiàng', 'mú-yáng', 'mú-yàng', 'mú-xiàng']
```
