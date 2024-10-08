# Python3

## 基础知识
### 注释
    # 单注释 ’’’ ””” 多注释
### 基本数据类型：（type查看）
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
### 数据转换
    隐式与显式  
    chr(),ord() 字符与ASCII码   
    hex(),oct() 进制
### 异常处理
    1. try/except 
        - except+错误代码，最后一个except作通配符，有异常执行 。
        - else，表示没有异常且try中没有return时执行。
        - finally，无论如何都执行。如果finally 有return, 则会覆盖try/except中的return。
    2. Raise 
        抛出异常raise [Exception [, args [, traceback]]]
    3. Exception类
        自定义异常
    4. 异常的抛出
        一般用于网络访问等情况（比如爬虫）
### with语句
        当执行with语句时，Python会调用上下文管理器对象的__enter__()方法来获取资源，然后执行with-block。当代码块执行完毕后，Python会自动调用上下文管理器对象的__exit__()方法来释放资源。简单来说，就是
        有了with可以不需要try/except，可以在类封装的__exit()__函数对其进行处理，包括错误判定等；如果要让程序继续执行，只需要return True即可。 
### 函数注解
        函数注解可以在函数声明时，对函数的参数和返回值进行注解。
        函数注解的语法格式为：def func(arg1: type, arg2:'string', arg3: int = 0) -> type:
        函数注解的作用是对函数的参数和返回值进行类型提示，它不会对函数的参数和返回值进行强制性的类型检查。
        函数注解的信息存储在函数的 __annotations__ 属性中，它是一个字典，键是参数名，值是注解的类型。
        函数注解的主要作用是对函数的参数和返回值进行类型提示，它不会对函数的参数和返回值进行强制性的类型检查。
### Python中的*args和**kwargs
        *args就是就是传递一个可变参数列表给函数实参，这个参数列表的数目未知，甚至长度可以为0。args类型是一个tuple。
        **kwargs则是将一个可变的关键字参数的字典传给函数实参，同样参数列表长度可以为0或为其他值。kwargs则是一个字典dict。
        args只能位于kwargs的前面。
        args和kwargs不仅可以在函数定义中使用，还可以在函数调用中使用。在调用时使用就相当于pack（打包）和unpack（解包），类似于元组的打包和解包。
```python
# 示例：函数中使用 *args 和 **kwargs
from functools import wraps
def trace(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f'TRACE: calling {func.__name__}() '
              f'with {args}, {kwargs}')
        original_result = func(*args, **kwargs)
        print(f'TRACE: {func.__name__}() '
              f'returned {original_result!r}')
        return original_result
    return wrapper
@trace
def say(name, line):
    return f'{name}: {line}'
say('Jane', 'Hello, World')
# 输出
# TRACE: calling say() with ('Jane', 'Hello, World'), {}
# TRACE: say() returned 'Jane: Hello, World'
```
### == 与 is
        == 比较的是值，is 比较的是对象的标识（内存地址）。 
        is 运算符比 == 速度快，因为它不能重载，而是直接比较两个整数 ID；而 a == b 是语法糖，等同于 a.__eq__(b)。
        一般而言，我们比较的是值，所以 == 的使用频率更高。
        但是在比较对象是否为 None 时，应该使用 is。

## 类与对象
### 实例方法、类方法、静态方法
        实例方法：默认方法，不需要修饰。只有实例可以调用。实例变量用self来调用。
        类方法：需要@classmethod修饰。只有类可以调用。类中变量用类名调用。
        静态方法：需要@staticmethod修饰。类和实例都可以调用。
### Cls 方法
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
### 类的简洁化创建
#### 具名元组
        具名元组，namedtuple，是一个工厂函数，用来创建一个带字段名的元组和一个有名字的类。
        nametuple 有两个参数，第一个是类名，第二个是类的各个字段的名字。后者可以是由数个字符串组成的可迭代对象，或者是由空格分隔开的字段名组成的字符串。
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p.y)  # 输出 1 2
```
#### dataclass
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
### 用户定义可调用类型
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
### 可散列类和只读化处理属性
        一般而言，Python 中只有不可变的对象才能作为字典的键，这种对象叫做可散列对象。
        可散列对象需要满足以下要求：
        - 支持 hash() 函数，并且通过 __hash__() 方法所得到的散列值是不变的。
        - 支持通过 __eq__() 方法来检测相等性。
        - 对象和hash有关的属性都不能变化，比如对象的实例变量。
        要使一个类可散列，要进行以下操作：
        - 实现一个 __hash__() 方法，使其返回一个散列值。
        - 实现一个 __eq__() 方法，使其返回 True。
        - 对hash有关的计算进行设置，使其不能变化。(比如只读化处理hash有关的属性)
```python
# 示例：实现一个可散列的二维向量类
from array import array
import math
class Vector2d:
    typecode = 'd'
    def __init__(self, x, y):
        # 用只读属性保护实例变量
        self.__x = float(x)
        self.__y = float(y)
    
    # 只读访问器构造函数
    @property
    def x(self):
        return self.__x
    @property
    def y(self):
        return self.__y
    def __eq__(self, other):
        return tuple(self) == tuple(other)
    def __hash__(self):
        return hash(self.__x) ^ hash(self.__y)
```
### __slots__ 类节省空间
        Python 中的对象会占用大量的内存，因为每个对象都会存储各种各样的信息，比如实例变量、类变量、方法等。
        为了减少内存的使用，可以使用 __slots__ 类属性来指定实例属性名的列表，从而减少实例所占的内存。
        __slots__ 属性只对当前类有效，对子类无效。
```python
# 示例：使用 __slots__ 类属性来减少实例所占的内存
class Vector2d:
    __slots__ = ('__x', '__y')
    typecode = 'd'
    def __init__(self, x, y):
        self.__x = float(x)
        self.__y = float(y)
```
### 鸭子类型和白鹅类型
        鸭子类型：鸭子类型是指，当我们看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。鸭子类型是一种动态类型，它关注的不是对象的类型本身，而是它是如何使用的。
        白鹅类型：白鹅类型是一种静态类型，它关注的是对象的类型本身。一般继承于同一个父类的对象，都可以被看作是白鹅类型。白鹅类型也可以不通过继承而实现，可以通过python的register方法来实现。register是虚拟子类，只是将类注册到父类中，注册的类不会从父类中继承任何方法。(我寻思似乎只有用到大量isinstace项目时会用到)
```python
# 示例：鸭子类型
class Duck:
    def quack(self):
        print('Quack, quack!')
    def fly(self):
        print('Flap, flap!')
class Person:
    def quack(self):
        print("I'm quacking like a duck!")
    def fly(self):
        print("I'm flapping my arms!")
def quack_and_fly(thing):
    thing.quack()
    thing.fly()
d = Duck()
quack_and_fly(d)  # 输出 Quack, quack! Flap, flap!
p = Person()
quack_and_fly(p)  # 输出 I'm quacking like a duck! I'm flapping my arms!

# 示例：白鹅类型, 继承实现
class Bird:
    def quack(self):
        print('Quack, quack! I am a bird.')
    def fly(self):
        print('Flap, flap! I am a bird.')
class Duck(Bird):
    def quack(self):
        print('Quack, quack! I am a duck.')
    def fly(self):
        print('Flap, flap! I am a duck.')
def quack_and_fly(thing):
    thing.quack()
    thing.fly()
b = Bird()
quack_and_fly(b)  # 输出 Quack, quack! I am a bird. Flap, flap! I am a bird.
d = Duck()
quack_and_fly(d)  # 输出 Quack, quack! I am a duck. Flap, flap! I am a duck.

# 示例：白鹅类型, register实现
class Bird:
    def quack(self):
        print('Quack, quack! I am a bird.')
    def fly(self):
        print('Flap, flap! I am a bird.')
@Bird.register
class Duck:
    def quack(self):
        print('Quack, quack! I am a duck.')
    def fly(self):
        print('Flap, flap! I am a duck.')
print(issubclass(Duck, Bird))  # 输出 True
```
### 多继承时的执行顺序
        python 支持多继承，但是多继承时，如果多个父类中有同名的方法，子类会优先调用排在前面的父类中的方法。
```python
# 示例：多继承时的执行顺序
class A:
    def func(self):
        print('A')
class B:
    def func(self):
        print('B')
class C(A, B):
    def func(self):
        super().func()
c = C()
c.func()  # 输出 A
B.func(c)  # 输出 B
```

## 装饰器
        装饰器本质上是一个Python函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对象。
### 工作原理
```python
    @decorator
    def func():
        pass
    #等同于
    fun = decorator(func)
```
### Python 启用装饰器的时间
        装饰器的关键特性是，它们在被装饰的函数定义之后立即运行。这通常是在导入时（即Python加载模块时）。因此，装饰器可以用于改进“策略模式”。
```python
# 装饰器选择最佳策略
registry = []
def register(func):
    print('running register(%s)' % func)
    registry.append(func)
    return func
@register
def f1(value):
    return value * 2 
@register
def f2(value):
    return value + 2
@register      
def f3(value):
    return value ** 2
def best_func(value):
    return max(f(value) for f in registry)
```
### 闭包和nonlocal声明
        闭包是一种函数，它会保留定义函数时存在的自由变量的绑定，这样调用函数时，虽然定义作用域不可用了，但是仍然能够使用那些绑定。
        闭包的典型用途是延伸函数的作用域。
        nonlocal 声明用于指示某个变量是外部作用域中的自由变量，而不是局部作用域中的变量。一般可变变量在闭包中不需要nonlocal声明，但是如果要修改不可变变量（如元组或数字）则需要nonlocal声明。
```python
# 闭包实现计算移动平均值
def make_averager():
    count = 0
    total = 0
    def averager(new_value):
        nonlocal count, total
        count += 1
        total += new_value
        return total / count
    return averager
avg = make_averager()
print(avg(10))  # 输出 10.0
print(avg(11))  # 输出 10.5
print(avg(12))  # 输出 11.0
```
### 标准库中的装饰器
        functools.lru_cache 装饰器实现了备忘（memoization）功能，它把耗时的函数的结果保存起来，避免传入相同的参数时重复计算。(牺牲空间换取时间)
```python
# 示例：使用 functools.lru_cache 装饰器实现备忘功能
from functools import lru_cache
@lru_cache()
def fib(n):
    if n < 2:
        return n
    return fib(n - 1) + fib(n - 2)
print(fib(80)) # 用lru_cache可以大幅度缩短递归运行时间
```
        functools.singledispatch 装饰器可以把整体方案拆分成多个模块，甚至可以为你无法修改的类提供专门的函数。
```python
# 示例：使用 functools.singledispatch 装饰器为不同类型的对象执行不同的操作
from functools import singledispatch
@singledispatch
def fun(arg, verbose=False):
    if verbose:
        print("Let me just say,", end=" ")
    print(arg)
@fun.register(int)
def _(arg, verbose=False):
    if verbose:
        print("Strength in numbers, eh?", end=" ")
    print(arg)
@fun.register(list)
def _(arg, verbose=False):
    if verbose:
        print("Enumerate this:")
    for i, elem in enumerate(arg):
        print(i, elem)
@fun.register(dict)
def _(arg, verbose=False):
    if verbose:
        print("We are dicty:")
    for key, value in arg.items():
        print(key, value)
fun("Hi", verbose=True)  # 输出 Let me just say, Hi
fun(42, verbose=True)  # 输出 Strength in numbers, eh? 42
fun(['spam', 'spam', 'eggs', 'spam'], verbose=True) # 输出 Enumerate this: 0 spam 1 spam 2 eggs 3 spam
fun({'a': 1, 'b': 2}, verbose=True)  # 输出 We are dicty: a 1 b 2
```
        functools.total_ordering 装饰器为类定义所有的比较运算符，这样只需定义一个 __eq__() 方法，就能使用装饰器提供的方法自动获得其他方法。
```python
# 示例：使用 functools.total_ordering 装饰器为类定义所有的比较运算符
from functools import total_ordering
@total_ordering
class Student:
    def __init__(self, name, grade, age):
        self.name = name
        self.grade = grade
        self.age = age
    def __eq__(self, other):
        return ((self.grade, self.age) == (other.grade, other.age))
    def __lt__(self, other):
        return ((self.grade, self.age) < (other.grade, other.age))
student1 = Student('John', 'A', 15)
student2 = Student('Jane', 'B', 12)
print(student1 > student2)  # 输出 True
```
### 参数化装饰器
        参数化装饰器是指接受参数的装饰器，它能让我们在应用装饰器时传入自定义的参数。
```python
# 示例：参数化的注册装饰器
registry = set()
def register(active=True):
    def decorate(func):
        print('running register(active=%s)->decorate(%s)' % (active, func))
        if active:
            registry.add(func)
        else:
            registry.discard(func)
        return func
    return decorate
@register(active=False)
def f1():
    print('running f1()')
@register()
def f2():
    print('running f2()')
```

## Python 中的函数参数传递
### 可变与不可变，浅复制与深复制
        Python中的变量类型可分为可变与不可变。Python中可变对象包括列表（list）、字典（dict）、集合（set）等；不可变对象包括数字（int, float等）、布尔值（bool）、字符串（str）等。
        可变对象传入函数后，相当于C语言中的引用，对象更改会使对象发生改变。不可变对象则不会改变。

        浅复制：复制对象，但不会复制对象中的可变元素，即复制对象中的可变元素的引用。
        深复制：复制对象，同时会复制对象中的可变元素，即复制对象中的可变元素的值。
        一般来说，python复制列表可以用list()。也可以用python标准库中copy和deepcopy实现浅复制和深复制。

        不要使用可变类型作为参数的默认值，因为默认值会成为函数对象的属性，导致new 类的时候会出问题。
        防御可变参数，尽量传参默认值改为None，然后在属性赋值改为判断：None则为空列表，非None则浅复制或深复制。
```python
# 防御可变参数,
def __init__(self, passengers=None):
    if passengers is None:
        self.passengers = []
    else:
        self.passengers = list(passengers)
```
### 赋值
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
        当此时print(data)的值就可以发现两者的不同。
### 关键字参数
        Python中存在仅限关键字参数，即在函数定义时，参数名前加*，表示该参数只能作为关键字参数传入。
        比如
        def fun(a, b, *, c):
            print(a, b, c)
        这里c就是仅限关键字参数，只能通过c=xxx的形式传入。


## 高阶函数
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
### functiontools.partial
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

## Python数据结构 
### 列表推导式，生成器表达式和字典推导式
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
### 元组拆包
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
### 序列用*易出现的错误
        用*来处理序列时，如果序列的元素为可变对象的引用，往往会出现错误。
        错误示范：my_list = [[]] * 3, 此时my_list中的三个元素都是对同一个列表的引用，所以当修改其中一个元素时，其他元素也会发生改变。
        正确示范：my_list = [[] for _ in range(3)]，此时my_list中的三个元素都是独立的列表，修改其中一个元素不会影响其他元素。
### 数组, 内存视图, 双向队列
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
### dict中字典的默认处理
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





## 生成器函数与协程
        生成器函数：包含yield关键字的函数，调用生成器函数时，会返回一个生成器对象。对于一个生成器对象，应该使用next函数或send方法来获取下一个值，直到抛出StopIteration异常。使用for, list, tuple等函数可以获取生成器对象的所有值而不会抛出异常。
        协程：协程是指一个过程，这个过程与调用方协作，产出由调用方提供的值。协程可以暂停执行并在暂停的地方继续执行。
### iter 函数
        iter函数用于生成迭代器，迭代器是一种特殊的对象，它可以在诸如for循环之类的语句中使用。iter函数接收两个参数，第一个参数是一个可调用对象，第二个参数是哨符，用于标记迭代的结束。可用于检测对象是否可迭代。
        iter函数的作用：检查对象是否实现了__iter__方法，如果实现了则调用它，获取一个迭代器；如果没有实现__iter__方法，则检查对象是否实现了__getitem__方法，如果实现了则创建一个迭代器，从序列的第一个元素开始遍历；如果两个方法都没有实现，则抛出TypeError异常。
        __iter__方法：如果一个对象实现了__iter__方法，那么它就是可迭代的，可以被iter函数识别。__iter__方法必须返回一个迭代器，比如自身实现了__next__方法后需要返回self。
        __next__方法：如果一个对象实现了__next__方法，那么它就是迭代器，可以被next函数识别。__next__方法必须返回下一个元素，如果没有元素了则需要抛出StopIteration异常。
        __getitem__方法：如果一个对象实现了__getitem__方法，那么它就是可迭代的，可以被iter函数识别。__getitem__方法必须返回下一个元素，如果没有元素了则需要抛出IndexError异常。
```python
# 只实现__iter__方法调用iter
class Foo:
    num_ls = []
    def __init__(self, num):
        self.num = num
        Foo.num_ls.append(self.num)
    def __next__(self):
        if self.num_ls:
            return self.num_ls.pop(0)
        else:
            raise StopIteration 
    def __iter__(self):
        return self
foo = Foo(1)
foo2 = Foo(2)
print(list(foo))  # 输出 [1, 2]
# 只实现__getitem__方法调用iter
class Foo:
    num_ls = []
    def __init__(self, num):
        self.num = num
        Foo.num_ls.append(self.num)
    def __getitem__(self, index):
        return Foo.num_ls[index]
foo = Foo(1)
foo2 = Foo(2)
print(list(foo))  # 输出 [1, 2]
```
### Yield
    1. 与return 一样是返回值，不同的是yield是生成器，类似断点可保存信息。
    2. 有yield关键字后调用函数返回的就是实例化的生成器对象。
    3. yield两种操作：next与send。Send可以让yield得到返回值。
### 生成器函数与iter
        生成器函数和类的__iter__都可以构建生成器，但是后者不如前者，因为__iter__方法每次都要创建一个新的迭代器对象，而生成器函数则不会。
```python
# 示例：使用生成器函数构建生成器
def gen_AB():
    print('start')
    yield 'A'
    print('continue')
    yield 'B'
    print('end.')
for c in gen_AB():
    print('-->', c)
# 示例：使用类的 __iter__ 方法构建生成器
class gen_AB:
    def __iter__(self):
        print('start')
        yield 'A'
        print('continue')
        yield 'B'
        print('end.')
for c in gen_AB():
    print('-->', c)
# 输出:
# start
# --> A
# continue
# --> B
# end.
```
### 惰性实现
        Iterator接口可以用于实现惰性计算，即只有在需要时才计算。惰性计算可以节省大量内存，提高程序的性能。如下的re.finditer函数就是惰性实现。
        re.finditer(pattern, string, flags=0) 函数用于在字符串中找到正则表达式所匹配的所有子串，并返回一个迭代器，迭代器中包含匹配的所有子串。运用该函数代替re.findall可以节省大量内存。
```python
import re
# 示例：使用 re.finditer 函数查找字符串中的所有数字
s = '12 drummers drumming, 11 pipers piping, 10 lords a-leaping'
RE_WORD = re.compile(r'\w+')
for match in RE_WORD.finditer(s):
    print(match.group(), end='|')
# 输出: 12|drummers|drumming|11|pipers|piping|10|lords|a|leaping|
```
### 标准库的生成器函数
1. compress(it, selector_it): 并行处理两个可迭代对象，如果selector_it中的元素为真，则输出it中对应的元素。
2. dropwhile(predicate, it): 跳过it中predicate为真的元素，然后输出剩下的元素。
3. takewhile(predicate, it): 输出it中predicate为真的元素，然后停止。
4. filter(predicate, it): 输出it中predicate为真的元素。为内置函数。
5. filterfalse(predicate, it): 输出it中predicate为假的元素。
6. map(func, it1, [it2, ..., itN]): 输出func(it1[i], it2[i], ..., itN[i])的结果。为内置函数。
7. starmap(func, it): 输出it中func(*it[i])的结果, it一般为元组或列表。
8. islice(it, stop)或islice(it, start, stop, step=1): 输出it中从start开始到stop结束的元素切片，步长为step。
9. accumulate(it, [func]): 输出it中的元素累加和，如果指定了func，则输出it中的元素经过func处理后的累加和。
10. enumerate(iterable, start=0): 输出iterable中的元素以及元素的索引，索引从start开始。为内置函数。
11. chain(it1, ..., itN): 依次输出it1, ..., itN中的元素。
12. product(it1, ..., itN, repeat=1): 输出it1, ..., itN中的元素的笛卡尔积，repeat表示重复次数。
13. zip(it1, ..., itN): 输出it1, ..., itN中的元素的元组。只要有一个可迭代对象到达结尾，就会停止。为内置函数。
14. zip_longest(it1, ..., itN, fillvalue=None): 输出it1, ..., itN中的元素的元组，如果某个可迭代对象到达结尾，则用fillvalue填充。fillvalue默认为None。
15. count(start=0, step=1): 从start开始，每次加step，输出一个无限序列。
16. repeat(object, [times]): 输出object，如果指定了times，则输出times次。
17. cycle(iterable): 无限重复iterable中的元素。
### yield from 语句
        yield from 语句可以用于简化 for 循环中的 yield 语句，它可以把一个可迭代对象中的所有元素都产出。
        yield from 语句的作用：
        1. yield from 语句可以把嵌套的可迭代对象中的所有元素都产出。
        2. yield from 语句可以把子生成器产出的值直接传给生成器的调用方。
        3. yield from 语句可以在生成器中处理子生成器产生的异常。
```python
# 示例：使用 yield from 语句简化 for 循环中的 yield 语句
def chain(*iterables):
    for it in iterables:
        yield from it
s = 'ABC'
t = tuple(range(3))
print(list(chain(s, t)))  # 输出 ['A', 'B', 'C', 0, 1, 2]
```
### @contextmanager 装饰器
        @contextmanager 装饰器可以把简单的生成器函数变成上下文管理器，从而减少重复代码。
        @contextmanager 装饰器的作用：
        1. @contextmanager 装饰器可以把简单的生成器函数变成上下文管理器。
        2. @contextmanager 装饰器可以减少重复代码。
        3. @contextmanager 装饰器可以把生成器函数中的 yield 语句移到 __exit__ 方法中。
        使用 @contextmanager 装饰器时，一定要定义一个生成器函数，它的作用是生成上下文管理器。yield 语句之前的代码相当于 __enter__ 方法，yield 语句之后的代码相当于 __exit__ 方法中的内容。yield 语句产出的值会绑定到 with 语句中 as 子句的目标变量上。
        注意使用try/finally语句时，yield一定要放在try中，因为yield之后的语句相当于finally中的语句。
```python
# 示例：使用 @contextmanager 装饰器把简单的生成器函数变成上下文管理器
from contextlib import contextmanager
@contextmanager
def looking_glass():
    import sys
    original_write = sys.stdout.write
    def reverse_write(text):
        original_write(text[::-1])
    sys.stdout.write = reverse_write
    yield 'JABBERWOCKY'
    sys.stdout.write = original_write
with looking_glass() as what:
    print('Alice, Kitty and Snowdrop')
    print(what)
# 输出:
# pordwonS dna yttiK ,ecilA
# YKCOWREBBAJ
```
### 协程(coroutine)
        协程是指一个过程，这个过程与调用方协作，产出由调用方提供的值。协程可以暂停执行并在暂停的地方继续执行。协程可以把控制权交给调用方，让调用方决定做什么。协程可以用于实现多任务协作式函数。
        协程的特点：
        1. 协程是指一个过程，这个过程与调用方协作，产出由调用方提供的值。
        2. 协程可以暂停执行并在暂停的地方继续执行。
        3. 协程可以把控制权交给调用方，让调用方决定做什么。
        4. 协程可以用于实现多任务协作式函数。
        协程的使用步骤：
        1. 调用方通过调用生成器的 next 方法预激生成器。
        2. 调用方通过 send 方法把数据发给生成器。
        3. 协程通过 yield 表达式把控制权让给调用方。
        4. 调用方处理数据，然后再把控制权交还给协程。
        P.S. 使用yield from 会自动预激子生成器；可以通过捕获StopIteration异常来判断协程是否结束。
```python
# 示例：使用协程的简单例子
def simple_coroutine():
    print('-> coroutine started')
    x = yield
    print('-> coroutine received:', x)
my_coro = simple_coroutine()
print(my_coro)  # 输出 <generator object simple_coroutine at 0x0000020E6F9F9C80>
next(my_coro)  # 输出 -> coroutine started
my_coro.send(42)  # 输出 -> coroutine received: 42
my_coro.send(43)  # 抛出 StopIteration 异常
```

## 期物(future)和asyncio
### 期物
        期物: 期物是一个对象，它表示异步执行的操作。期物是协程的结果，它可以用于判断协程是否结束，也可以用于获取协程的结果。  
        期物的状态: 期物有三种状态，分别是 pending、running 和 finished。
        常见期物的方法:
        1. done() 方法: 用于判断期物是否结束，如果结束则返回 True，否则返回 False。
        2. result() 方法: 用于获取期物的结果，如果期物没有结束，则会阻塞直到期物结束。
        3. exception() 方法: 用于获取期物的异常，如果期物没有异常，则返回 None。
```python
# 示例：使用 asyncio.Future 类表示异步操作
import asyncio
async def set_after(fut, delay, value):
    await asyncio.sleep(delay)
    fut.set_result(value)
async def main():
    loop = asyncio.get_running_loop()
    fut = loop.create_future()
    await asyncio.gather(
        set_after(fut, 2, 'hello'),
        set_after(fut, 1, 'world'),
    )
    print(fut.result())
asyncio.run(main())
```
        期物和协程的关系: 期物是协程的结果，它可以用于判断协程是否结束，也可以用于获取协程的结果。
### asyncio
        asyncio 是 Python 3.4 版本引入的标准库，它提供了一种协程的实现方式，可以用于编写高效的异步程序。asyncio 是基于事件循环的异步框架，它提供了一种协程的实现方式，可以用于编写高效的异步程序。
        asyncio 的特点：
        1. asyncio 是基于事件循环的异步框架，它提供了一种协程的实现方式，可以用于编写高效的异步程序。
        2. asyncio 提供了一种协程的实现方式，可以用于编写高效的异步程序。
        常见asyncio 库的方法:
        1. asyncio.run(coro) 函数: 用于运行一个协程。
        2. asyncio.create_task(coro) 函数: 用于创建一个任务。
        3. asyncio.ensure_future(coro/future) 函数: 用于创建一个任务。与 create_task 方法不同的是，ensure_future 方法可以接收一个 Future 对象。
        4. asyncio.gather(*tasks) 函数: 用于并发运行多个任务。
        5. asyncio.wait(tasks) 函数: 用于等待多个任务完成。
        6. asyncio.sleep(delay) 函数: 用于休眠 delay 秒。
        7. asyncio.get_running_loop() 函数: 用于获取当前运行的事件循环。
