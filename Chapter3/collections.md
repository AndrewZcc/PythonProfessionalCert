# 3.1 高性能容器数据结构 collections

* https://docs.python.org/zh-cn/3/library/collections.html
* https://www.liaoxuefeng.com/wiki/1016959663602400/1017681679479008

**简介**
collections在python官方文档中的解释是 **High-performance container datatypes**，高性能 **容器数据类型**。
它总共包含五种数据类型：
- 【字典的变种】Counter：高性能**计数器**
- 【字典的变种】defaultdict：带缺省值的字典 (append/appendleft, pop/popleft)
- 【字典的变种】orderdDict：字典的子类，保存了他们被添加的顺序
- 【列表的变种】deque：高性能**双向列表**
- namedtuple()：创建命名元组子类的工厂函数

#### 1、Counter
提供了对可哈希对象的计数功能。

```python
# collections.Counter
from collections import Counter
colors = ['red', 'blue', 'red', 'green', 'blue', 'blue']
c = Counter(colors)
print (dict(c)) // {'red': 2, 'blue': 3, 'green': 1}
【备注: 不需要再遍历所有colors去进行计数了，直接 Counter(colors) 即可】

# Counter这种数据结构支持的 操作
c = Counter(a=3, b=1)
d = Counter(a=1, b=2)
c + d                       # 相加
#Counter({'a': 4, 'b': 3})
c - d                       # 相减，如果小于等于0，删去
#Counter({'a': 2})
c & d                       # 求最小
#Counter({'a': 1, 'b': 1})
c | d                       # 求最大
#Counter({'a': 3, 'b': 2})
```

#### 2、DefaultDict
defaultdict的作用是在于，当字典里的key不存在但被查找时，返回的不是keyError而是一个默认值。

defaultdict接受一个工厂函数作为参数，factory_function可以是list、set、str等等，作用是当key不存在时，返回的是工厂函数的默认值，比如list对应[ ]，str对应的是空字符串，set对应set( )，int对应0

```python
dict = defaultdict(factory_function)
# 设置默认值为 -1，工厂函数可以简的用一个 lambda 匿名函数 即可
dict = defaultdict(lambda: -1)

from collections import defaultdict

dict1 = defaultdict(int)
dict2 = defaultdict(set)
dict3 = defaultdict(str)
dict4 = defaultdict(list)
dict1[2] ='two'

print(dict1[1])  # 0
print(dict2[1])  # set()
print(dict3[1])  # “”
print(dict4[1])  # []
```
https://www.jianshu.com/p/bbd258f99fd3

#### 3、Deque (stack / queue)
deque 是Python中stack和queue的通用形式，也就是 **既能当栈用，又能当做双向队列**，list是单向队列。
```python
# 一、只要list里有的方法，deque 都可以用.
list.append(obj)
list.count (obj) #统计某个元素在列表中出现的次数
list.extend(seq)
list.index(obj) # 从列表中找出某个值第一个匹配项的索引位置
list.insert(index, obj) #将对象插入列表
list.pop([index=-1]) # 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
list.remove(obj) # 移除列表中某个值的第一个匹配项
list.reverse() # 反向列表中元素
list.sort(cmp=None, key=None, reverse=False) # 对原列表进行排序

# 二、但是 deque 的方法list是不能用的例如：
deque.appendleft(x)  头部添加元素
deque.extendleft(iterable) 头部添加多个元素
deque.popleft() 头部返回并删除
deque.rotate(n=1) 旋转
deque.maxlen 最大空间，如果是无边界的，返回None
```

https://blog.csdn.net/qq_34979346/article/details/83540389
