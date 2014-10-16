title: slice
date: 2014-10-14 10:46:19
categories: python
tags: [python, slice, pythonic]
---
“不会slice，绝不能说会python”，slice的重要性不言而喻。

## Basis
* index start with 0
* support negtive index
* [included:excluded:step] eg: **`[:]`**, **`[::-1]`**
* work with list, tuple and string

## step
```python Ipython 中的示例
In [1]: e = range(6)
  
In [2]: e
Out[2]: [0, 1, 2, 3, 4, 5]
  
In [3]: e[:]
Out[3]: [0, 1, 2, 3, 4, 5]
  
In [4]: e[6]
IndexError
  
In [5]: e[5]
Out[5]: 5
  
In [6]: e[:5]
Out[6]: [0, 1, 2, 3, 4]
  
In [7]: e[:6]
Out[7]: [0, 1, 2, 3, 4, 5]
  
In [8]: e[::-1]
Out[8]: [5, 4, 3, 2, 1, 0]
  
In [9]: e[6:0]
Out[9]: []
  
In [10]: e[6:0:-1]
Out[10]: [5, 4, 3, 2, 1]
  
In [11]: 0 in e[6:0:-1]
Out[11]: False
  
In [12]: e[5:0:-1]
Out[12]: [5, 4, 3, 2, 1]
  
In [13]: e[5:0:-1] == e[6:0:-1]
Out[13]: True
  
In [14]: e[-1:-7:-1]
Out[14]: [5, 4, 3, 2, 1, 0]
  
In [15]: e[-1:-7:-1] == e[::-1]
Out[15]: True
  
In [16]: e[-1:-9:-1]
Out[16]: [5, 4, 3, 2, 1, 0]
  
In [17]: e[::-2] == e[-1:-7:-2]
Out[17]: True
  
In [18]: e[::-2] == e[-1:-8:-2]
Out[18]: 'Just do IT'
```
* **e[::-1] == e[-1:-7:-1]**
* slice切片中索引可以超出实际范围
* 带有步长的切片，索引顺序和步长方向一致
* 切片总是新产生一个对象，而不是改变原有对象

## 总结
`Just do IT`

