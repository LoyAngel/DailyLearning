# Python3

## 注释
    # 单注释 ’’’ ””” 多注释

## 基本数据类型：（type查看）
    1. String : 
        - 不能改变
        - +连，*重复
        - 从右往左以 -1 开始
        - \转义，加r原字符
        - 截取的语法格式：变量[头下标:尾下标:步长]
    2. Number: int bool float complex（复数）
    3. List:
        - 可改变
        - [],list()创建
        - 下标访问
    4. Tuple:
        - 不可改变（可连接）
        - (),tuple()创建
    5. Set:
        - {},set()创建（空集合不可用{}创建）
        - 防重复
        - 可以用中缀运算符 |（并集）, &（交集）, -（差集）来计算集合之间的运算。
    6. Dictionary:
        - 映射，哈希
        - {},dict()创建
        - Keys()、Values()

## 数据转换
    隐式与显式  
    chr(),ord() 字符与ASCII码   
    hex(),oct() 进制

## Yield
    1. 与return 一样是返回值，不同的是yield是生成器，类似断点可保存信息。
    2. 有yield关键字后调用函数返回的就是实例化的生成器对象。
    3. yield两种操作：next与send。Send可以让yield得到返回值。

## 异常处理：
    1. try/except 
        - except+错误代码，最后一个except作通配符，有异常执行 。
        - else，表示没有异常时执行。
        - finally，无论如何都执行。
    2. Raise 
        抛出异常raise [Exception [, args [, traceback]]]

## Exception类
        自定义异常

## 异常的抛出
    一般用于网络访问等情况（比如爬虫）

## with语句
        当执行with语句时，Python会调用上下文管理器对象的__enter__()方法来获取资源，然后执行with-block。当代码块执行完毕后，Python会自动调用上下文管理器对象的__exit__()方法来释放资源。简单来说，就是
        有了with可以不需要try/except，可以在类封装的__exit()__函数对其进行处理，包括错误判定等；如果要让程序继续执行，只需要return True即可。 

## Python中的*args和**kwargs
        *args就是就是传递一个可变参数列表给函数实参，这个参数列表的数目未知，甚至长度可以为0。args类型是一个tuple。
        **kwargs则是将一个可变的关键字参数的字典传给函数实参，同样参数列表长度可以为0或为其他值。kwargs则是一个字典dict。
        args只能位于kwargs的前面。
        args和kwargs不仅可以在函数定义中使用，还可以在函数调用中使用。在调用时使用就相当于pack（打包）和unpack（解包），类似于元组的打包和解包。

## 装饰器
        我的理解：在要重复使用的函数下加上Wrapper（*args,**kwargs）函数，写明需要重复调用的操作，再在需要使用这个重复函数的前面加上@(Name of Function) ，即可实现重复调用。      

## Python 中的函数参数传递
        Python中的变量类型可分为可变与不可变。Python中可变对象包括列表（list）、字典（dict）、集合（set）等；不可变对象包括数字（int, float等）、布尔值（bool）、字符串（str）等。
        可变对象传入函数后，相当于C语言中的引用，对象更改会使对象发生改变。不可变对象则不会改变。

## Python 中的函数参数传递2
        Python中的赋值实际上赋值的是地址，这里和C语言很大不同。
        例：
        b = a
        a = 7 ,a = “str” ，都是赋值常量地址，所以改变b不会影响啥，但，
        a = [ 1 ,2 ,3 ] ,a = [‘a’:1, ‘b’:2]时，右边为可变变量时，改变b就会对a产生影响。
        
        这里非常容易犯的错误，比如：
        data = ['1', '2', '3' ]时，
        head = data
        head += ['domain_url','domain_name']
        和
        head = data + ['domain_url','domain_name']
        两者是不一样的，前者引用了地址然后改变值，后者可以理解为常量的相加（？）。

## Python 中的函数参数传递3
        Python中存在仅限关键字参数，即在函数定义时，参数名前加*，表示该参数只能作为关键字参数传入。
        比如
        def fun(a, b, *, c):
            print(a, b, c)
        这里c就是仅限关键字参数，只能通过c=xxx的形式传入。

## 函数注解
        函数注解可以在函数声明时，对函数的参数和返回值进行注解。
        函数注解的语法格式为：def func(arg1: type, arg2:'string', arg3: int = 0) -> type:
        函数注解的作用是对函数的参数和返回值进行类型提示，它不会对函数的参数和返回值进行强制性的类型检查。
        函数注解的信息存储在函数的 __annotations__ 属性中，它是一个字典，键是参数名，值是注解的类型。
        函数注解的主要作用是对函数的参数和返回值进行类型提示，它不会对函数的参数和返回值进行强制性的类型检查。

## 实例方法、类方法、静态方法
        实例方法：默认方法，不需要修饰。只有实例可以调用。实例变量用self来调用。
        类方法：需要@classmethod修饰。只有类可以调用。类中变量用类名调用。
        静态方法：需要@staticmethod修饰。类和实例都可以调用。

## filter ,map, reduce
        filter, map, reduce 是 Python 中的三个内置高阶函数，它们都是对集合进行操作的函数，都接收一个函数作为参数，然后返回一个新的集合。
### filter 函数：
        filter 函数用于根据指定的条件过滤集合中的元素，只保留满足条件的元素。
```python
# 示例：过滤出列表中的偶数
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # 输出 [2, 4, 6, 8, 10]
```
### map 函数：
        map 函数用于对集合中的每个元素应用一个函数，并返回由函数处理后的结果组成的新集合。
```python
# 示例：将列表中的每个数平方
numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x**2, numbers))
print(squared_numbers)  # 输出 [1, 4, 9, 16, 25]
```
### reduce 函数：
        reduce 函数在 Python 3 中被移到 functools 模块中。它用于对集合中的元素进行累积操作，将集合中的元素逐个应用到一个二元函数上，从而得到一个单一的累积结果。
```python
from functools import reduce

# 示例：计算列表中所有数的乘积
numbers = [2, 3, 4, 5]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 输出 120 (2 * 3 * 4 * 5)
```
  
        在总结上述三个函数的区别时：
        - filter 用于过滤出满足条件的元素。
        - map 用于对每个元素应用一个函数，返回处理后的结果组成的新集合。
        - reduce 用于对集合中的元素进行累积操作，将二元函数逐个应用到元素上，得到一个单一的累积结果。
        注意：
        - filter 和 map 函数都可以用列表推导式来替代。

## functiontools.partial
        functools.partial 函数用于部分应用一个函数，即固定函数的某些参数，返回一个新的函数。
```python
from functools import partial
from operator import mul
from random import shuffle
# partial的运用简化函数
double = partial(mul, 2)
rand_ls = shuffle(list(range(10)))
double_ls = list(map(double, rand_ls))
print(double_ls)
```

## 列表推导式，生成器表达式和字典推导式
        - 列表推导式
        首先形式为 [a for a in {gen}] ，gen为迭代器。返回值为列表。
```python
# 简化前
num_str = "123"
codes = []
for num in num_str:
    codes.append(ord(num))
# 简化后
num_str = "123"
codes = [ord(num) for num in num_str]


# 笛卡尔积(二维数组)：
cartesian_str = [ (a+b) for a in a_str
                        for b in b_str]
```
        - 生成器表达式
        首先生成的是一个生成器，形式为(a for a in {gen}) 。返回值为迭代器，配合for 使用较好。
        tuple(ord(char) for char in strls)
```python
#简化前
num_str = "123"
codes = []
for num in num_str:
    codes.append(ord(num))
#简化后
num_str = "123"
codes = (ord(num) for num in num_str)
```
        - 字典推导式
        首先形式为 {a:b for a,b in {gen}} ，gen为迭代器。返回值为字典。
```python
# 简化前
num_str = "123"
codes = {}
for num in num_str:
    codes[num] = ord(num)
# 简化后
num_str = "123"
codes = {num: ord(num) for num in num_str}
```

## 元组拆包
        可以用  a, b, c, d = (a1, b1, c1 ,d1) 
        一般可以用于函数返回值赋值中：
```python
def fun1(k1, k2, ...):
    ...
    return (res1, res2, ...)
res1, res2, ...= fun1(k1, k2, ...)
用*可以处理剩下的元素
  res1, res2, *rest = fun1(k1, k2, ...)
```

## Cls 方法
        cls方法指在类中调用本身，往往跟修饰器@classmethod 绑定。
```python
class Apple:
    def __init__(self, color, name):
        self.color = color
        self.name = name
    
    @classmethod
    def be_touched(cls, fruit):
        apple = cls(fruit.color, fruit.name)
        return apple
```

## 类的简洁化创建
### 具名元组
        具名元组，namedtuple，是一个工厂函数，用来创建一个带字段名的元组和一个有名字的类。
        nametuple 有两个参数，第一个是类名，第二个是类的各个字段的名字。后者可以是由数个字符串组成的可迭代对象，或者是由空格分隔开的字段名组成的字符串。
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p.y)  # 输出 1 2
```
### dataclass
        dataclass 是 Python 3.7 新增的一个装饰器，用于自动为数据类生成一些特殊方法，如 __init__、__repr__、__eq__ 等。
```python
from dataclasses import dataclass
@dataclass
class Point:
    x: int
    y: int
p = Point(1, 2)
print(p.x, p.y)  # 输出 1 2
```

## 序列用*易出现的错误
        用*来处理序列时，如果序列的元素为可变对象的引用，往往会出现错误。
        错误示范：my_list = [[]] * 3, 此时my_list中的三个元素都是对同一个列表的引用，所以当修改其中一个元素时，其他元素也会发生改变。
        正确示范：my_list = [[] for _ in range(3)]，此时my_list中的三个元素都是独立的列表，修改其中一个元素不会影响其他元素。

## bisect 搜索
        bisect 模块包含两个主要函数，bisect 和 insort，两个函数都利用二分查找算法来在有序序列中查找或插入元素。
        bisect 函数用于查找元素应该插入的位置，insort 函数用于将元素插入到相应的位置。
```python
import bisect
my_list = [1, 2, 3, 7, 9, 11, 33]
print(bisect.bisect(my_list, 3))  # 输出 3
print(bisect.bisect(my_list, 8))  # 输出 4
bisect.insort(my_list, 4)
print(my_list)  # 输出 [1, 2, 3, 4, 7, 9, 11, 33]
```

## 数组, 内存视图, 双向队列
### 数组
        Python 中的数组是指由同一类型的元素组成的集合，与列表不同，数组中的元素类型必须一致。
        Python 中的数组效率比列表高，因此在需要存储大量数字的时候，应该使用数组而不是列表。
```python
from array import array
my_array = array('i', [1, 2, 3, 4])
print(my_array[0])  # 输出 1
```
### 内存视图
        内存视图是一个内置类，它能让用户在不复制内容的情况下操作同一个数组的不同切片。
        内存视图一般用于处理大型数据集合，可以显著提升程序的性能。
        常见用法：利用 memoryview.cast 将数组中的内容转换成不同类型，这样就可以在不复制内容的情况下，将内容转换成不同类型。
```python
numbers = array('h', [-2, -1, 0, 1, 2]) # 有符号短整数
memv = memoryview(numbers)
print(len(memv))  # 输出 5
memv_oct = memv.cast('B') # 转换成无符号字符
print(memv_oct.tolist())  # 输出 [254, 255, 255, 255, 0, 0, 1, 0, 2, 0]
```
### 双向队列
        双向队列是一个由队列构成的队列，可以在队列的两端添加或删除元素。
        双向队列可以用于实现先进先出的栈（LIFO），工程里常用于多线程的日志记录。
```python
from collections import deque
import time
def search(lines, pattern, history=5):
    previous_lines = deque(maxlen=history)
    for line in lines:
        if pattern in line:
            yield line, previous_lines
        previous_lines.append(line)
```

## dict中字典的默认处理
        setdefault() 方法: 为dict类的实例添加一个新的键值对，如果该键已经存在于dict中，则不做任何操作。
        defaultdict() 方法: 为collections模块中的defaultdict类, 是一个工厂函数，用于创建一个类似于dict的对象，其中所有的键都有默认值。
```python
data = [("p", 1), ("p", 2), ("p", 3),
        ("h", 1), ("h", 2), ("h", 3)]
# 正常情况
result = {}
for (key, value) in data:
    if key not in result:
        result[key] = []
    result[key].append(value)
# setdefault 方法
result = {}
for (key, value) in data:
    result.setdefault(key, []).append(value)
# defaultdict 方法
from collections import defaultdict
result = defaultdict(list)
for (key, value) in data:
    result[key].append(value)
```

## Unicode 中 EncodeError 和 DecodeError 处理
        多数非UTF-8编码的文本文件中，都会包含一些无法解码的字节序列，这些字节序列会导致异常。
        处理 EncodeError 异常的方法是使用 errors 参数，它可以指定如何处理不能编码的字符。
        errors 参数可以是一个字符串，也可以是一个编码错误处理方案。
        如果 errors 参数是一个字符串，它的值可以是 'strict'、'ignore'、'replace'、'xmlcharrefreplace' 或者 'backslashreplace'。
        如果 errors 参数是一个编码错误处理方案，它的值可以是 codecs.register_error() 方法的返回值。
```python
### EncodeError 处理
# 示例：使用 errors 参数处理 EncodeError 异常
city = 'São Paulo'
print(city.encode('utf-8'))  # 输出 b'S\xc3\xa3o Paulo'
print(city.encode('utf-16'))  # 输出 b'\xff\xfeS\x00\xe3\x00o\x00 \x00P\x00a\x00u\x00l\x00o\x00'
print(city.encode('iso8859_1', errors='ignore'))  # 输出 b'So Paulo'
print(city.encode('cp437', errors='replace'))  # 输出 b'S?o Paulo'
print(city.encode('cp437', errors='xmlcharrefreplace'))  # 输出 b'S&#227;o Paulo'
print(city.encode('cp437', errors='backslashreplace'))  # 输出 b'S\xe3o Paulo'

### DecodeError 处理
# 示例：使用 errors 参数处理 DecodeError 异常
octets = b'Montr\xe9al'
print(octets.decode('cp1252'))  # 输出 Montréal
print(octets.decode('iso8859_7'))  # 输出 Montrιal
print(octets.decode('koi8_r'))  # 输出 MontrИal
print(octets.decode('utf-8', errors='replace'))  # 输出 Montr�al
print(octets.decode('utf-8'))  # 抛出 UnicodeDecodeError 异常
```

## 用户定义可调用类型
        除了使用 def 语句或 lambda 表达式来创建函数之外，Python 还可以使用 class 语句来定义可调用类型。
        如果一个类实现了 __call__ 方法，那么它的实例可以作为函数调用。
```python
class Adder:
    def __init__(self, n):
        self.n = n

    def __call__(self, m):
        return self.n + m
adder = Adder(5)
print(adder(3))  # 输出 8
```


