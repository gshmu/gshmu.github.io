title: AND & OR
date: 2014-08-08
categories: python
tags: [python, bool]
---
Python 的bool运算 and & or，但运算结果不是单纯的False或者True，无疑结果是对的。一句话总结：用最少的运算，保留更多的信息，保证正确的结果。

## Documentation
| Operation | Result | Notes |
| --- | --- | --- |
| x or y | if x is false, then y, else x | 运算是短路的 |
| x and y | if x is false, then x, else y | 运算是短路的 |

### 关于短路
`print None and None[0]`没有报错，正常打印出None。（`None[0]`会报`TypeError`错）

### `bool ? x : y`运算
由于python的bool运算保留了更多信息，所以可以实现上述三目运算。

##### 三目运算
*三目运算是这样的，可是存在一个误区！*
`bool and x or y`

##### 误区，当x为假时，永远返回y。
修正上述误区：`((test and [x]) or [y])[0]`采用了`x`为假时，`[x]`为真（避免上述误区），然后`[0]`索引求值。

还有种简洁的写法：`(y, x)[bool]` 其中x，y是反的，用`bool`索引求值。

上面涉及了两个值，网上还有三个或更多值的，我就不多少了，也不建议去搜。`ugly`！

### 技巧VS陷阱
我认为，这个既算不上技巧，也不能称为陷阱。

python实现三目运算还是用`x if bool else y`，从看着到结果都比较顺眼。当然适当的使用and & or保留值的特性也是可以的，主要是你要明白你写的是什么。

## 写代码，自己要明白，还要让看的人明白。
（看的人也要知道自己看的是python）


