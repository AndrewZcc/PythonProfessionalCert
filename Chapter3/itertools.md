# 3.2 itertools 内建迭代工具模块

- https://www.liaoxuefeng.com/wiki/1016959663602400/1017783145987360
- https://blog.csdn.net/u013300049/article/details/79313979

#### 非常有用的几个 迭代器 工具

1. **chain(iter1, iter2)**: 可以把一组迭代对象串联起来，变成一个更大的迭代器：
```python
>>> for c in itertools.chain('ABC', 'XYZ'):
...     print(c)
# 迭代效果：'A' 'B' 'C' 'X' 'Y' 'Z'
```

2. **groupby(iter)**: 对迭代器中元素进行分组，相邻相同的元素 会被分为一组：
```python
>>> for key, group in itertools.groupby('AAABBBCCAAA'):
...     print(key, list(group))
...
A ['A', 'A', 'A']
B ['B', 'B', 'B']
C ['C', 'C']
A ['A', 'A', 'A']
```

3. **product**(p, q, ..., repeat=n): 笛卡尔积
```python
>>> list(product('ABC', repeat=2))
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
```

4. **permutations**(p[, r])：排列
```python
>>> list(itertools.permutations('ABC', 2))
[('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
```

5. **combinations**(p, r)：组合
```python
>>> list(itertools.combinations('ABC', 2))
[('A', 'B'), ('A', 'C'), ('B', 'C')]
```

6. **combinations_with_replacement**(p, r)：带重复元素的组合
```python
>>> list(itertools.combinations_with_replacement('ABC', 2))
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```
