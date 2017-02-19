title: django advanced
date: 2015-03-22 08:08:06
categories: Python
tags: [django, python, advanced]
---
本文记述我在使用Django时遇到的两个问题，两次被坑的过程，也是两次进步的过程。

## `qs[m:n].update()`
业务我就不多说了，给queryset（总数可能有十万之多）中的部分（以万记）更新某个字段（或者说分配到某个订单），由于要保证互斥，同时希望序列号连续（对应实体的东西，方便分取）所以使用`select_for_update()`，当然任何使用锁的地方应该确保尽可能少锁，同时尽快释放。

问题出来了，如此多的数据，如果循环更新，锁的时间将会比较长，可是Django不支持切片后更新。办法：
``` python qs[m:n].update()
qs = Models.objects.filter(...).select_for_update().order_by("id")
rows = qs.filter(id__lt=qs[count:count+1].get().id).update(...)
assert(rows == count)  # TODO: remove
```

## `qs.distinct().aggregate()`
相信熟悉SQL的同学对distinct一定不陌生，加上MySQL后端，就出了这个问题。由于冗余条件的存在，所以qs里面出现了重复数据，这里就不赘述了。（注：当时使用的是Django==1.5.8，django不支持distinct(field)） So：
``` python qs.distinct().aggregate()
qs = Models.objects.filter(...)
qs = Models.objects.filter(pk__in=qs)  # distinct
sum_dict = qs.aggregate(...)
```
没错，就是多操作了一步。解决方法就是这么简单，可是这个重复数据并不总是有，让我头疼了好一阵子，不过还是被我给揪出来了。

## 总结
第二个问题环境：MySQL数据库后端 + Diango<1.6。当然如今我们都升1.7了，不过我还是记录下。
