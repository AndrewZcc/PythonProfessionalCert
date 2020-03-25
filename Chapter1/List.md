# 1.2 List / collections.deque

### List 列表

序列中最常见的就是：列表 和 元组。所有序列都支持：**索引、切片、加、乘、成员检查** 这些基本操作。

##### 列表常用操作
```python
# 更新 或 添加元素
list = ['Google', 'Runoob', 1997, 2000]
list[2] = 2001
list1.append('zhchuch') //在列表末尾添加新的对象
list.insert(index, obj) //在指定位置添加新元素

# 删除元素
del list[2]
list1.remove(obj) //移除列表中某个值的第一个匹配项
list.pop([index=-1]) //移除指定位置的 列表元素 (默认移除最后一个)

# 列表元素个数
len(list)
# 返回最大值
max(list)
# 返回最小值
min(list)

# 统计某个元素在列表中出现的次数
list.count(obj)
# 列表 扩充另一个列表
list.extend(seq)
# 反转
list.reverse()
# 排序
list.sort( key=None, reverse=False)
# 清空
list.clear()
# 复制
list.copy()

# 列表 深拷贝 (只有深拷贝 才是真正互不影响/完全相互独立 的拷贝)
pre = list()
pre.append(copy.deepcopy([""] * 4))

# 从列表中找出某个值第一个匹配项的索引位置，找不到则抛出异常
list.index(obj)
```

### 用 list 实现堆栈 stack
**STACK**
```python
stack = [3, 4, 5]
stack.append(6)
stack.append(7)
stack.pop()  # 7
stack.pop()  # 6
```

### 用 list 实现队列 deque [collections.deque](/Chapter3/collections.md)
**Deque, Queue**
```python
from collections import deque
queue = deque(["Eric", "John", "Michael"])
queue.append("Terry")
queue.append("Graham")
queue.popleft()  # 'Eric'
queue.popleft()  # 'John'
```

### 用 list 实现二维数组
```python
# 二维数组定义与初始化
// 1.直接赋值
matrix = [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

// 2. 正确的 初始化定义
matrix = [[0]*15 for i in range(15)] // √
// 2. 错误的 初始化定义
matrix = [[0]*15]*15  // ×
```
备注：**切记：**不可直接用 `[[0]*15]*15` 这种方式来定义一个初始化的 15\*15 大小的数组！

因为 python中列表是可变的，直接用`*`进行复制，其实复制的只是个引用，这样定义后大家指向的后台说白了都是同一个对象！会相互影响 一变俱变！

https://www.cnblogs.com/bellz/p/10590707.html
