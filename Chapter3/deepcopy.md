# 3.2 deepcopy 深拷贝

**简介：**
在 Python 中, 我们有两种拷贝对象的方式：**浅拷贝**和**深拷贝**。浅拷贝和深拷贝都可以在 copy 模块中找到, 其中 copy.copy() 进行浅拷贝操作, copy.deepcopy() 进行深拷贝操作。浅拷贝是在另一块地址中创建一个新的对象，但是新对象内的子对象引用指向源对象的子对象。如果这时候我们修改源对象的子对象的属性, 新对象中子对象的属性也会改变。为了获取一个和源对象没有任何关系的全新对象，我们需要深拷贝。**深拷贝**是在另一块地址中创建一个新的对象，同时对象内的子对象也是新开辟的，和源对象对比仅仅是值相同。

#### 为什么 Python 深拷贝这么慢

python3 深拷贝实现源码：
```python
def deepcopy(x, memo=None, _nil=[]):
    """Deep copy operation on arbitrary Python objects.
    See the module's __doc__ string for more info.
    """
    if memo is None:
        memo = {}

    d = id(x)
    y = memo.get(d, _nil)
    if y is not _nil:
        return y

    cls = type(x)

    copier = _deepcopy_dispatch.get(cls)
    if copier:
        y = copier(x, memo)
    else:
        try:
            issc = issubclass(cls, type)
        except TypeError: # cls is not a class (old Boost; see SF #502085)
            issc = 0
        if issc:
            y = _deepcopy_atomic(x, memo)
        else:
            copier = getattr(x, "__deepcopy__", None)
            if copier:
                y = copier(memo)
            else:
                reductor = dispatch_table.get(cls)
                if reductor:
                    rv = reductor(x)
                else:
                    reductor = getattr(x, "__reduce_ex__", None)
                    if reductor:
                        rv = reductor(4)
                    else:
                        reductor = getattr(x, "__reduce__", None)
                        if reductor:
                            rv = reductor()
                        else:
                            raise Error(
                                "un(deep)copyable object of type %s" % cls)
                if isinstance(rv, str):
                    y = x
                else:
                    y = _reconstruct(x, memo, *rv)

    # If is its own copy, don't memoize.
    if y is not x:
        memo[d] = y
        _keep_alive(x, memo) # Make sure x lives at least as long as d
    return y
```

备注：其中 `memo` 保存着所有拷贝过的对象。深拷贝需要维护一个 memo 用于记录已经拷贝的对象，这是它比较慢的原因。而维护这个 memo 的原因是为了避免相互引用造成的死循环。绝大多数情况下，程序中不存在相互引用。但作为通用模块，Python 深拷贝必须为了这 1% 情形，牺牲 99% 情形下的性能。真是无奈呀。我们可以通过自己实现 \_\_deepcopy\_\_ 函数来改进其效率。

#### 结论
尽量少用 deepcopy()，对性能影响还是比较大了！

但在保证正确且**不超时的情况下**，该用还是得用！