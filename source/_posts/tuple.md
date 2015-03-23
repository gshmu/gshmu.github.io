title: tuple change?
date: 2014-10-8
categories: Python
tags: [python, tuple]
---
在python中元组tuple是不能改变的，列表和字典是可以改变的。

### `change`
```python
In [1]: l = [1, 2]
 
In [2]: d = {'a':'aaa', 'b':'bbb'}
 
In [4]: t = (l, d)
 
In [5]: t
Out[5]: ([1, 2], {'a': 'aaa', 'b': 'bbb'})
 
In [7]: l.pop()
Out[7]: 2
 
In [8]: t
Out[8]: ([1], {'a': 'aaa', 'b': 'bbb'})
 
In [9]: l.append(3)
 
In [10]: t
Out[10]: ([1, 3], {'a': 'aaa', 'b': 'bbb'})
```

## 总结
上述，元组的项目是列表，改变了列表。元组有没有改变，自己掂量吧...
