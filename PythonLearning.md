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

## 实例方法、类方法、静态方法
        实例方法：默认方法，不需要修饰。只有实例可以调用。实例变量用self来调用。
        类方法：需要@classmethod修饰。只有类可以调用。类中变量用类名调用。
        静态方法：需要@staticmethod修饰。类和实例都可以调用。

## Map, filter , reduce
    
       - filter 函数：
    filter 函数用于根据指定的条件过滤集合中的元素，只保留满足条件的元素。

```python
# 示例：过滤出列表中的偶数
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # 输出 [2, 4, 6, 8, 10]
```

       - map 函数：
        map 函数用于对集合中的每个元素应用一个函数，并返回由函数处理后的结果组成的新集合。

```python
# 示例：将列表中的每个数平方
numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x**2, numbers))
print(squared_numbers)  # 输出 [1, 4, 9, 16, 25]
```
  
       - reduce 函数：
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

## 列表推导式与生成器表达式
        - 列表推导式
        首先形式为 [a for a in {gen}] ，gen为迭代器。返回值为列表。
```python
#简化前
num_str = "123"
codes = []
for num in num_str:
    codes.append(ord(num))
#简化后
num_str = "123"
codes = [ord(num) for num in num_str]
    笛卡尔积(二维数组)：
cartesian_str = [ (a+b) for a in a_str
                        for b in b_str]
```
        - 生成器表达式
        首先生成的是一个生成器，形式为(a for a in {gen}) 。返回值为迭代器，配合for 使用较好。
        tuple(ord(char) for char in strls)

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