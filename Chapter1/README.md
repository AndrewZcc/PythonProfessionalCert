# 一、Python 常考数据类型
### 一、基本操作

```python
输入输出
str = input('Please input a string:')
# 正常输出 (默认带换行)
print(str)
# 不换行输出: 指定结尾字符
print( x, end="")
```

### 二、数据类型

#### 1. 基本数据类型

注意：虽然Python有数据类型，但在实际使用过程中不需要显式声明！在 Python 中，变量就是变量，它没有类型，每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。
**Number** 类型：1. int，2. bool，3. float，4. complex

变量定义和赋值：

```python
a = 1
b = 2
c = "string"
a = float('inf') # 正无穷
b = float('-inf') # 负无穷

a = b = c = 1
a, b, c = 1, 2, "runoob"
```

变量删除

```python
del a
del a, b, c
```

#### 2. 六大标准数据类型

不可变：**Number**（数字），**String**（字符串），**Tuple**（元组）
可变：**List**（列表），**Set**（集合），**Dictionary**（字典）

查看/判断 一个变量是什么类型

```python
a = 20
type(a) ... ... <class 'int'>
isinstance(a, int) ... ... True
```

------

##### 1、Number (不可变)

https://m.runoob.com/python3/python3-number.html

```python
a, b, c, d = 20, 5.5, True, 4+3j
print(type(a), type(b), type(c), type(d))
输出： <class 'int'> <class 'float'> <class 'bool'> <class 'complex'>

运算
+ - * /
a // b 整除
a % b 取余
a ** b 乘方

abs(x) # 绝对值
ceil(x) # 向上取整
floor(x) # 向下取整
exp(x) # math.exp(1) 返回e，e的x次方, math.exp(2) e^2
fabs(x) # 绝对值浮点返回
log(x)
log10(x)
max(x1, x2, ...)
min(x1, x2, ...)
pow(x, y) #幂
sqrt(x) #平方根
round(x[, n]) # 四舍五入 保留n位小数点
modf(x)
```

##### 2、String (不可变)

```python
# 字符串 基本操作
str='Runoob'
print(str)                 # 输出字符串
print(str[0:-1])           # 输出第一个到倒数第二个的所有字符
print(str[0])              # 输出字符串第一个字符
print(str[2:5])            # 输出从第三个开始到第五个的字符
print(str[2:])             # 输出从第三个开始后的所有字符
print(str * 2)             # 输出字符串两次
print(str + '你好')        # 连接字符串

print('------------------------------')

print('hello\nrunoob')      # 使用反斜杠(\)+n转义特殊字符
print(r'hello\nrunoob')     # 在字符串前面添加一个 r，表示原始字符串，不会发生转义

# 运算
[] 字符串截取
+ 字符串连接
* 字符串复制
r'' 原生字符串 (转义符失效)
```

注意：python 字符串是不可变类型，所以 `str[0]='a'`这种尝试修改的操作 会报错！

##### 3、Tuple (不可变)

元组（tuple）与列表类似，不同之处在于元组的**元素不能修改**。元组写**在小括号 () 里**，元素之间用逗号隔开。

```python
tuple = ('abcd', 786 , 2.23, 'runoob', 70.2)
print (tuple)             # 输出完整元组
print (tuple[0])          # 输出元组的第一个元素
print (tuple[1:3])        # 输出从第二个元素开始到第三个元素
print (tuple[2:])         # 输出从第三个元素开始的所有元素
print (tinytuple * 2)     # 输出两次元组
print (tuple1 + tuple2)   # 连接元组

tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```

------

##### 4、List (可变)

列表可以完成大多数集合类的数据结构实现。列表是写在方括号 [] 之间、用逗号分隔开的元素列表。
和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。
**与 字符串/元组 不同的是：列表中的元素 可以改变**！

```python
list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
tinylist = [123, 'runoob']
# 列表基本操作
print (list)            # 输出完整列表
print (list[0])         # 输出列表第一个元素
print (list[1:3])       # 从第二个开始输出到第三个元素
print (list[2:])        # 输出从第三个元素开始的所有元素
print (tinylist * 2)    # 输出两次列表
print (list + tinylist) # 连接列表

# 改变列表元素
>>>a = [1, 2, 3, 4, 5, 6]
>>>a[0] = 9
>>>a[2:5] = [13, 14, 15] # 修改子列表中所有元素的值
a = [9, 2, 13, 14, 15, 6]
>>>a[2:5] = []   # 将对应的元素值设置为 [], 可以理解为删除列表中的元素！ remove()
a = [9, 2, 6]

list截取 可以有第三个参数 (代表每次截取的步长 默认步长为1)
如果步长为负数，则表示逆向读取，可用于 反转字符串
inputWords[-1::-1] 三个参数解释
# 第一个参数 -1 表示最后一个元素
# 第二个参数为空，表示移动到列表末尾
# 第三个参数为步长，-1 表示逆向
```

列表相关常用函数

```
list = str.split(' ')  // 字符串分割成 list
str = ' '.join(list)  // list 拼接为字符串
```

##### 5、Set (可变)

基本功能是 进行成员关系测试 和 删除重复元素。可以使用大括号 { } 或者 set() 函数创建集合。

```python
# 创建
parame = {value01,value02,...}
set(value)

# 去重
student = {'Tom', 'Jim', 'Mary', 'Tom', 'Jack', 'Rose'}
print(student)   # 输出集合，重复的元素被自动去掉
# 成员测试
if 'Rose' in student :
    print('Rose 在集合中')
else :
    print('Rose 不在集合中')

# 支持集合运算
a = set('abracadabra')
b = set('alacazam')
print(a)
print(a - b)     # a 和 b 的差集 (差)
print(a | b)     # a 和 b 的并集 (并)
print(a & b)     # a 和 b 的交集 (交)
print(a ^ b)     # a 和 b 中不同时存在的元素 (异或)
```

##### 6、Dictionary (可变)

字典当中的元素是通过键来存取的，而不像列表只能通过偏移进行存取。
字典是一种映射类型，字典用 { } 标识，它是一个无序的 **键(key) : 值(value)** 的集合。

```python
tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值

字典初始化
>> dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
{'Taobao': 3, 'Runoob': 1, 'Google': 2}
>> dict(Runoob=1, Google=2, Taobao=3)
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
```

#### 3. 数据类型转换

```python
int(x [, base])
str(x)
repr(x) // 将x转换成表达式字符串
eval(str) // 对字符串表达式 直接求值
```
