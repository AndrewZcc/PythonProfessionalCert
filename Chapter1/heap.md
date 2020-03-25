# 1.8 堆

### python heapq 堆

这是一个相当实用的内置模块，但是很多人竟然不知道他的存在，尽管如此，还是改变不了这个模块好用的事实！它是一种优先队列。它能让你能够以任意顺序添加对象，并随时（可能是在两次添加对象之间）找出（并删除）最小的元素。

#### 主要函数
```python
heappush(heap, x)	# x 压入堆
heappop(heap)		# 从堆中 pop出 最小元素
heapify(heap)		# 将列表 堆化
heapreplace(heap, x) # 弹出最小元素，并将x压入堆 ==> 相当于 pop + push(x)

nlargest(n, list)  # 直接返回 list 中最大的n个元素
nsmallest(n, list) # 直接返回 list 中最小的n个元素
```
备注：
1. **heapq** 擅长求前n最大/小的元素，因为这就是堆的性质（heap……q）
2. python 中的 heapq **默认是 小根堆**
3. **大根堆** 怎么实现？一个巧妙的实现：我们还是用小根堆来进行逻辑操作，在做push的时候，我们把最大数的相反数(取负) 存进去，那么它的 **相反数(负值)** 就是最小数，仍然是堆顶元素，在访问堆顶的时候，再对它取反，就获取到了最大数。

相关链接
- https://www.cnblogs.com/sunlong88/articles/10252957.html
- https://blog.csdn.net/abc_12366/article/details/80423249
- https://blog.csdn.net/jamfiy/article/details/88185512

#### 典型例题

https://leetcode-cn.com/problems/k-th-smallest-prime-fraction/
