# 2.5 python 排序

### 一、bisect 二分快速插入排序

`bisect`用于在 有序/已排过序的序列中，**快速** 向其中插入值、或 判断值的插入位置 的模块。

```python
# 使用范例
import bisect
class Solution:
    def countSmaller(self, nums):
        sorted_list, res = list(), list()
        for num in nums[::-1]:
            loc = bisect.bisect_left(sorted_list, num)
            res.append(loc)
            sorted_list.insert(loc, num)
        return res[::-1]
```

### 二、sorted vs. list.sort()

##### 1、key 参数/函数

list.sort()和 sorted()函数增加了key参数来 **指定一个函数**，**此函数将在每个元素比较前被调用**。

```python
# key参数 接收一个函数，此函数只有一个参数且返回一个值用来进行 定制化比较。
sorted(list(enumerate(nums)), key=lambda x:x[1])
```

#### 更多参考
https://www.jb51.net/article/57678.htm