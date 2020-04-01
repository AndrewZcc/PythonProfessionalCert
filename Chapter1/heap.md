# 1.8 堆

### python heapq 堆

这是一个相当实用的内置模块，但是很多人竟然不知道他的存在，尽管如此，还是改变不了这个模块好用的事实！它是一种优先队列。它能让你能够以任意顺序添加对象，并随时（可能是在两次添加对象之间）找出（并删除）最小的元素。

Heap queue algorithm (a.k.a. priority queue).
<br>Heaps are arrays for which a[k] <= a[2*k+1] and a[k] <= a[2*k+2] for
all k, counting elements from 0.  

#### 一、主要函数
```python
heapify(heap)		# 将列表 堆化
heappush(heap, x)	# x 压入堆
heappop(heap)		# 从堆中 pop出 最小元素
heapreplace(heap, x) # 弹出最小元素，并将x压入堆 ==> 相当于 pop + push(x)
heappushpop(heap, x)

merge(*iters, key=None, reverse=False) # merge multiple sorted inputs
nlargest(n, list)  # 直接返回 list 中最大的n个元素
nsmallest(n, list) # 直接返回 list 中最小的n个元素
```
备注：
1. **heapq** 擅长求前n最大/小的元素，因为这就是堆的性质（heap……q）
2. python 中的 heapq **默认是 小根堆**
3. **大根堆** 怎么实现？一个巧妙的实现：我们还是用小根堆来进行逻辑操作，在做push的时候，我们把最大数的相反数(取负) 存进去，那么它的 **相反数(负值)** 就是最小数，仍然是堆顶元素，在访问堆顶的时候，再对它取反，就获取到了最大数。

4. nlargest **Equivalent to:  sorted(iterable, key=key, reverse=True)[:n]**
5. nsmallest **Equivalent to:  sorted(iterable, key=key)[:n]**

相关链接
- https://www.cnblogs.com/sunlong88/articles/10252957.html
- https://blog.csdn.net/abc_12366/article/details/80423249
- https://blog.csdn.net/jamfiy/article/details/88185512

#### 二、使用示例与注意

```python
import heapq

heap = [8,10,21,2,5,14,9,7]

def large_small():
    print(heap)
    print("Sorted:", sorted(heap))
    print("NLarge:", heapq.nlargest(4, heap))
    print("NSmall:", heapq.nsmallest(3, heap))
    print(heap)

def heapify():
    print(heap)
    heapq.heapify(heap) # heapify 之后，原先的list会具备堆的特性
    print(heap)
    heap.sort() # heap 等价于就是一个 list
    print(heap)

def merge():
    a, b = [3,10,2,12,9], [1,6,9,4,8]
    print(list(heapq.merge(a, b))) # Error
    print(list(heapq.merge(sorted(a), sorted(b)))) # Right: merge two sorted list.

def push_pop():
    heapq.heapify(heap)
    print(heap)
    heapq.heappush(heap, 3) # 注意：如果heap中原先已经有元素了，必须先对齐进行 堆化，然后 push/pop 操作才能正确
    print(heap)
    print("pop:", heapq.heappop(heap)) # 如果不先堆化，push/pop 操作的结果就是 不满足堆性质 的 list.push/list.pop
    print(heap)
```

#### 典型例题

* https://leetcode-cn.com/problems/k-th-smallest-prime-fraction/
* https://leetcode-cn.com/problems/top-k-frequent-elements/
