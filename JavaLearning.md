# JAVA
 
## 基础注意项
### 注意点
        大小写敏感：Java 是大小写敏感的，这就意味着标识符 Hello 与 hello 是不同的。
        主方法入口：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。
### 注释
        单行注释：//
        多行注释：/* */
        文档注释：/** */
#### 特殊注释规范样例
        类注释：
        /**
        * CopyRright (c), xxxx-yyyy, All Rights Reserved
        * FileNmae: 类名.java
        * 类的详细说明
        * 
        * @author 作者姓名
        * @date xxxx年x月x日
        * @version x.x
        */
        属性注释：
        /**
        * 属性注释
        */
        方法注释：
        /**
        * 方法注释
        * @param 参数名 参数说明
        * @return 返回值说明
        * @throws 异常类型 说明
        */
### 标识符
        比其他常规语言多了美元符号
### 常见命名规范
        包名：多单词组成时所有字母都小写：xxyyzz
        类名、接口名：多单词组成时，所有单词的首字母大写：XxYyZz
        变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写：xxYyZz
        常量名：所有字母都大写。多单词时每个单词用下划线连接：XX_YY_ZZ
### javac和java命令
        javac：编译命令，将java文件编译成class文件
        java：运行命令，运行class文件

## Java的对象和类
### 构造方法
        Java的构造方法名必须与类名相同，一个类可以有多个构造方法，构造方法可以有多个参数，构造方法没有返回值。
### 创建对象
        三步走：
        1. 声明：声明一个对象，包括对象名称和对象类型。
        2. 实例化：使用关键字 new 来创建一个对象。
        3. 初始化：使用 new 创建对象时，会调用构造方法初始化对象。
### Java包
        类似python, import 包名.类名
        当前目录已经有class的情况下，可以直接使用类名，不需要import

## Java变量类型
### 局部变量
        局部变量声明在方法、构造方法或者语句块中；
        局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
        访问修饰符不能用于局部变量；
        局部变量只在声明它的方法、构造方法或者语句块中可见；
        局部变量是在栈上分配的。
### 成员变量
        成员变量是定义在类中，方法体之外的变量，在整个类体内都可见；
        成员变量在对象创建的时候创建，在对象被销毁的时候销毁；
        访问修饰符可以修饰成员变量；
        成员变量可以被声明在使用前或者使用后；
        成员变量是在堆上分配的。
### 类变量（静态变量）
        类变量声明在类中，方法体之外，但必须声明为static类型；
        类变量在类加载的时候创建，在程序退出的时候销毁；
        访问修饰符可以修饰类变量；
        类变量被声明为public static final类型时，类变量名称必须使用大写字母；
        类变量是在静态区分配的。
#### 静态变量线程安全
        类变量是全局的，所有的对象都共享同一个变量。所以，当一个对象对类变量进行修改后，其他对象访问的类变量是修改后的值。这样会造成线程安全问题。为了解决这个问题，可以使用同步关键字 synchronized，原子类，或者volatile关键字。
### 参数变量
        参数变量是在方法调用时被传递进方法中的变量；
        方法中的参数变量在调用方法时被创建，当方法返回时，参数变量被销毁；
        参数变量只在方法内部可见；
        参数变量是在栈上分配的。

## Java修饰符
### 访问控制修饰符
        Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。
        default：
        默认的，即不加任何修饰符，通常称为“默认访问模式“。
        访问级别：同一包内可见;不同包子类可见，非子类不可见。
        private：
        私有的，只允许在本类中进行访问。不能修饰类（外部类）。
        访问级别：本类可见; 不同包都不可见。
        public：
        公共的，允许在任何地方进行访问。
        访问级别：对所有类可见。
        protected：
        受保护的，允许在当前类、同一包中以及子类中进行访问。不能修饰类（外部类）。
        访问级别：本类、同一包、子类可见; 不同包都不可见。
### 非访问修饰符
        Java中，提供了很多非访问修饰符来实现其他的功能。非访问修饰符一般位于访问修饰符之前。
        static：
        静态的，表明一个成员变量或者方法可以在没有创建类的实例的情况下使用。静态变量始终只有一个副本，无论类创建了多少个对象。静态方法只能访问静态变量。
        final：
        最终的，表明一个变量只能被赋值一次，常量。一个类不能被继承，方法不能被重写。通常和 static 一起使用来创建类常量。
        abstract：
        抽象的，表明一个类或者方法是抽象的，不能被实例化。抽象方法只需要声明，不需要实现。通常和接口一起使用。
        synchronized：
        同步的，表明一个方法只能被一个线程访问。同步方法必须要有一个锁，通常为当前对象。
        volatile：
        易变的，确保一个线程修改了一个变量之后，其他线程能够立即看到修改的值。通常用于多个线程访问的成员变量或者状态变量。
        transient：
        短暂的，表明一个变量不应该被序列化，通常用于socket或者文件传输中。


## Java基本运算符
        大都与python一致，此处讲讲特殊的几个运算符。
        1. 三目运算符
        三目运算符与c一致，也不赘述。
        2. instanceof 运算符
        判定对象是否为某个类的实例，返回boolean值。

## Java循环结构
        1. while循环
        2. do...while循环
        3. for循环
        以上3种循环与c一致，不赘述。
        4. 增强for循环
        增强for循环指的是foreach循环，用于遍历数组或者集合，类似于python的for(i in list)。
        结构：for(元素类型 元素变量 : 数组或者集合) {循环体}
        5. break关键字
        6. continue关键字
        以上两个关键字与普通编程一致，不赘述。

## Java条件语句
        1. if语句
        2. if...else语句
        3. if...else if...else语句
        4. switch语句
        以上4种语句与c一致，不赘述。

## Java Number & Math类
### Number类
        基础数据类型：byte, short, int, long, float, double, boolean, char
        包装器类型：Byte, Short, Integer, Long, Float, Double, Boolean, Character
        两者区别：
        1. 基础数据类型在内存中占用空间较小，包装器类型在内存中占用空间较大。
        2. 基础数据类型是直接存储在栈中的，包装器类型是存储在堆中的。
        3. 基础数据类型的值是不可变的，包装器类型的值是可变的。
        4. 基础数据类型的默认值不是null，包装器类型的默认值是null。

        5. Boolean 1位, true/false
        6. Byte 8位有符号整数，范围-128~127
        7.  Short 16位有符号整数，范围-32768~32767
        8.  Integer 32位有符号整数，范围-2147483648~2147483647
        9.  Long 64位有符号整数，范围-9223372036854775808~9223372036854775807
        10. Float 32位单精度浮点数
        11. Double 64位双精度浮点数
        12. Character 16位Unicode字符，范围\u0000~\uffff
#### 装箱和拆箱
        装箱：将基本数据类型转换为包装器类型，例如将int转换为Integer，将double转换为Double。
                例子 Integer x = 5;
        拆箱：将包装器类型转换为基本数据类型，例如将Integer转换为int，将Double转换为double。
                例子 int x = new Integer(5);
#### Number & Math 常用类方法
        Number & Math 类用于对基本数据类型进行包装和数学运算。 
        1. Number类
        xxxValue()：以xxx类型返回指定数值
        compareTo()：将number对象与参数比较
        equals()：判断number对象是否与参数相等
        valueOf()：返回一个Number对象指定的内置数据类型
        2. Math类
        abs(x)：返回x的绝对值
        ceil(x)：返回大于等于x的最小整数
        floor(x)：返回小于等于x的最大整数
        max(x, y)：返回x和y中的最大值
        min(x, y)：返回x和y中的最小值
        pow(x, y)：返回x的y次幂
        sqrt(x)：返回x的平方根
        random()：返回0.0~1.0之间的随机数
        3. 通用型
        toString()：返回一个字符串表示形式
        parseInt()：将字符串解析为int类型
        random()：返回0.0~1.0之间的随机数

### Character 类
        Character 类用于对单个字符进行操作。
#### 转义序列
        \t, \b, \n, \r, \', \", \\
        与c一致，不赘述。
        \ddd, 表示8进制数ddd所代表的字符
        \uxxxx， 表示16进制数xxxx所代表的字符
#### Character类常用方法
        isLetter()：判断字符是否为字母
        isDigit()：判断字符是否为数字
        isWhitespace()：判断字符是否为空白字符
        isUpperCase()：判断字符是否为大写字母
        isLowerCase()：判断字符是否为小写字母
        toUpperCase()：将字符转换为大写字母
        toLowerCase()：将字符转换为小写字母
        toString()：返回字符的字符串形式，字符串长度为1

## String 与 StringBuffer & StringBuilder
### String 类
        String 类代表字符串。Java中的字符串是不可变的，所以每次对字符串的操作都会生成一个新的字符串对象。
        String 类是不可变的，所以你一旦创建了 String 对象，那它的值就无法改变了。如果需要对字符串做很多修改，那么应该选择使用 StringBuffer & StringBuilder 类。
#### String类创建字符串
        1. 通过字面量创建字符串
        String str = "Hello World";
        2. 通过构造方法创建字符串
        String str = new String("Hello World");
        两者区别：
        通过字面量创建的字符串会被放入字符串常量池中，而通过构造方法创建的字符串不会放入字符串常量池中；
        通过字面量创建的字符串对象的引用会被放入栈中，而通过构造方法创建的字符串对象的引用不会被放入栈中。
![String类创建字符串](https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png "String类创建字符串")
#### String类常见构建方法
        1. String()：初始化一个新创建的String对象，使其表示一个空字符序列。
        2. String(byte[] bytes)：通过使用平台的默认字符集解码指定的字节数组来构造新的String。
        3. String(char[] value)：分配一个新的String，使其表示字符数组参数中当前包含的字符序列。
#### String类常用方法
        1. length()：返回字符串的长度。例子：int len = str.length();
        2. concat()：将指定字符串连接到此字符串的结尾。例子：String str2 = str1.concat("World");
        3. format()：使用指定的格式字符串和参数返回一个格式化字符串。例子：String str2 = String.format("Hi, %s", "World");
        4. charAt()：返回指定索引处的char值。例子：char ch = str.charAt(0);
        5. indexOf()：返回指定字符在此字符串中第一次出现处的索引。例子：int index = str.indexOf("Hello");
        6. compareTo()：按字典顺序比较两个字符串。例子：int result = str1.compareTo(str2);
        7. substring()：返回一个新的字符串，它是此字符串的一个子字符串。例子：String substr = str.substring(0, 5);
        8. replace()：返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。例子：String str2 = str1.replace('H', 'W');
        9. replaceAll()：使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。例子：String str2 = str1.replaceAll("He", "Ha");
        10. contains()：当且仅当此字符串包含指定的 char 值序列时，返回 true。例子：boolean result = str.contains("Hello");
        11. split()：根据匹配给定的正则表达式来拆分此字符串。例子：String[] substr = str.split(" ");

### StringBuffer & StringBuilder 类
        StringBuffer & StringBuilder 类是可变的，可用于字符串拼接。
        StringBuffer & StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。
        StringBuffer & StringBuilder 类的基本方法和 String 类的方法是一样的。
#### StringBuffer与StringBuilder的区别
        StringBuffer 是线程安全的，StringBuilder 是非线程安全的。
        StringBuilder 效率高于 StringBuffer，所以多数情况下建议使用 StringBuilder 类。
#### StringBuffer & StringBuilder 比String 特有的方法
        1. append()：将指定的字符串追加到此字符序列。例子：StringBuffer str = new StringBuffer("Hello"); str.append("World");
        2. reverse()：将此字符序列用其反转形式取代。例子：StringBuffer str = new StringBuffer("Hello"); str.reverse();
        3. insert()：将指定的字符串插入此字符序列中。例子：StringBuffer str = new StringBuffer("Hello"); str.insert(0, "World");
        4. delete()：移除此序列的子字符串中的字符。例子：StringBuffer str = new StringBuffer("Hello"); str.delete(0, 5);
        5. replace()：使用给定 String 中的字符替换此序列的子字符串中的字符。例子：StringBuffer str = new StringBuffer("Hello"); str.replace(0, 5, "World");




## Java数组
### 数组
        数组是一个容器，可以同时存放多个数据值。
        数组的特点：
        1. 数组是引用数据类型
        2. 数组当中的多个数据，类型必须统一
        3. 数组的长度在程序运行期间不可改变
        Java数组大多与c一致，此处不赘述。
### 数组的声明
        1. dataType[] arrayRefVar; // 首选的方法
        2. dataType arrayRefVar[]; // 效果相同，但不是首选方法
        3. dataType[] arrayRefVar = new dataType[arraySize];
        4. dataType[] arrayRefVar = {value0, value1, ..., valuek};

## Java方法
        Java方法是语句的集合，它们在一起执行一个功能。
        Java方法类似于c中的函数，大多不再赘述。
### 命令行参数
        Java 命令行参数是 main() 方法的一个字符串数组。主方法不返回任何值，所以必须声明为 void。
        main() 方法的声明如下所示：
        public static void main(String args[])
        以下是一个简单的例子，演示了如何使用命令行参数：
```java
public class CommandLine {
        public static void main(String args[]){
        for(int i = 0; i<args.length; i++){
                System.out.println("args[" + i + "]: " + args[i]);
        }
        }
}
```
        编译以上代码，运行结果如下所示：
        $ javac CommandLine.java
        $ java CommandLine this is a command line 200 -100
        args[0]: this
        args[1]: is
        args[2]: a
        args[3]: command
        args[4]: line
        args[5]: 200
        args[6]: -100
### 可变参数
        可变参数允许传递不同数量的参数给一个方法。它最终被转化为一个数组传递给方法，可以使用命令行参数的方法来编写可变参数的方法。
        以下实例演示了可变参数的使用方法：
```java
public class VarargsDemo {
        public static void main(String args[]){
                // 调用可变参数的方法
                printMax(34, 3, 3, 2, 56.5);
                printMax(new double[]{1, 2, 3});
        }
        public static void printMax( double... numbers) {
                if (numbers.length == 0) {
                        System.out.println("No argument passed");
                        return;
                }
                double result = numbers[0];
                for (int i = 1; i <  numbers.length; i++)
                        if (numbers[i] >  result)
                                result = numbers[i];
                System.out.println("The max value is " + result);
        }
}
```
        编译以上代码，运行结果如下所示：
        $ javac VarargsDemo.java
        $ java VarargsDemo
        The max value is 56.5
        The max value is 3.0


## Java Stream, File & IO
#### Java Stream
        Java 中的流是一种数据传输方式，用于处理与设备、文件或者网络连接等交互的数据。
        Java 中，流是按照操作数据单位划分的，可以划分为字节流和字符流。
        字节流：以字节为单位进行数据传输，通常用于处理二进制文件，如图片、视频等。
        字符流：以字符为单位进行数据传输，通常用于处理文本文件，如txt、doc等。
        Java 中，流的操作方式分为两种：节点流和处理流。
        节点流：直接与数据源相连，读取数据或者写入数据。
        处理流：对一个已经存在的流进行连接或者封装，通过封装后的流来实现数据读取或者写入。
#### 控制台输入输出
1. System.in
        System.in 是 InputStream 的对象，通常用于获取键盘输入。
        初始化:
                BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.in 常见搭配输入方法: 
                br.read() 读取一个字节
                br.readln() 读取一行
2. System.out
        System.out 是 PrintStream 的对象，通常用于输出结果。
        System.out 常见搭配输出方法: 
                System.out.print() 输出一个字符
                System.out.println() 输出一行
                System.out.printf() 格式化输出
                System.out.write() 输出一个字节
3. Scanner
        Scanner 是 Java5 中的新特征，通常用于获取键盘输入。
        初始化:
                Scanner sc = new Scanner(System.in);
        Scanner 常见搭配输入方法: 
                sc.next() 读取一个字符串
                sc.nextInt() 读取一个整数
                sc.nextDouble() 读取一个双精度浮点数
                sc.nextBoolean() 读取一个布尔值
                sc.nextLine() 读取一行
#### 文件输入输出
1. FileInputStream
        FileInputStream 是 InputStream 的子类，通常用于读取二进制文件，如图片、视频等。
        初始化:
                FileInputStream fis = new FileInputStream("文件路径");
        FileInputStream 常见搭配输入方法: 
                fis.read() 读取一个字节
                fis.read(byte[] b, int off, int len) 读取一个字节数组的一部分
2. FileOutputStream
        FileOutputStream 是 OutputStream 的子类，通常用于写入二进制文件，如图片、视频等。
        初始化:
                FileOutputStream fos = new FileOutputStream("文件路径");
        FileOutputStream 常见搭配输出方法: 
                fos.write(int b) 写入一个字节
                fos.write(byte[] b, int off, int len) 写入一个字节数组的一部分

## 异常处理
        异常是程序在执行过程中出现的错误。
        Java 中，异常是一个对象，表示程序在执行过程中出现的错误。
        异常的分类：
        1. 检查性异常：在编译时发生的异常，如文件不存在、网络中断等。
        2. 运行时异常：在运行时发生的异常，如数组越界、除数为0等。
        3. 错误：Java 虚拟机无法解决的严重问题，如 JVM 运行错误、内存溢出等。
        Java 中，异常处理的方式有两种：try...catch...finally 和 throw/throws。
### try...catch...finally
        try 用于指定一块预防异常的代码。
        catch 用于捕获异常并处理异常。
        finally 用于指定一块无论是否发生异常都会执行的代码。
        以下实例演示了 try...catch...finally 的使用方法：
```java
public class ExceptionDemo {
        public static void main(String args[]){
                try {
                        int a[] = new int[2];
                        System.out.println("Access element three :" + a[3]);
                } catch (ArrayIndexOutOfBoundsException e) {
                        System.out.println("Exception thrown  :" + e);
                } finally{
                        System.out.println("The finally statement is executed");
                }
        }
}
```
### throw 与 throws
        throw 用于抛出一个异常对象。
        throws 用于声明一个方法可能抛出的所有异常。
        以下实例演示了 throw 与 throws 的使用方法：
```java
// throw
public class ExceptionDemo {
        public static void main(String args[]){
                try {
                        throw new Exception("My Exception");
                } catch (Exception e) {
                        System.out.println(e);
                }
        }
}
```
```java
// throws
public class ExceptionDemo {
        public static void main(String args[]) throws Exception {
                throw new Exception("My Exception");
        }
}
```

## 继承
### 继承关键字
        继承类用extends关键字，实现接口用implements关键字。
### super 与 this
        super 与 this 关键字用于在子类中访问父类的成员变量和成员方法。
        super 用于访问父类的成员变量和成员方法, this 用于访问本类的成员变量和成员方法。
### final
        final 关键字用于声明属性、方法和类，分别表示属性不可变、方法不可覆盖、类不可继承。
        final 修饰的属性必须在声明时初始化，且不可再修改。
        final 修饰的方法不可被子类覆盖。
        final 修饰的类不可被继承。
### 构造器
        构造器用于初始化对象，与python的__init__类似。
        构造器的名称必须与类名相同，且没有返回值。
        构造器的访问修饰符只能是 public，且不能被 static、final、synchronized 和 abstract 修饰。
        子类构造器不继承父类的构造器，但是子类构造器默认调用父类的无参构造器，如果父类没有无参构造器，则必须在子类的构造器中用 super 显式调用父类的构造器。

## Overload & Override
### Overload 
        重载指的是在同一个类中，方法名相同，参数列表不同的多个方法。
        重载的方法必须满足以下条件：
        1. 方法名相同
        2. 参数列表不同
        3. 与方法的修饰符和异常无关
        4. 与方法的参数名无关
        以下实例演示了重载的使用方法：
```java
public class OverloadDemo {
        public static void main(String args[]){
                OverloadDemo demo = new OverloadDemo();
                demo.test();
                demo.test(1);
                demo.test(1, 2);
                demo.test("Hello");
        }
        public void test() {
                System.out.println("无参方法");
        }
        public void test(int a) {
                System.out.println("重载的方法，参数为：" + a);
        }
        public void test(int a, int b) {
                System.out.println("重载的方法，参数为：" + a + " 和 " + b);
        }
        public void test(String a) {
                System.out.println("重载的方法，参数为：" + a);
        }
}
```
### Override
        重写指的是在子类中，方法名相同，参数列表相同，返回值相同的方法。
        重写的方法必须满足以下条件：
        1. 方法名相同
        2. 参数列表相同
        3. 返回类型相同
        4. 可以减少异常抛出，但是不能抛出新的异常
        5. 与方法的修饰符和异常无关
        6. 与方法的参数名无关
        以下实例演示了重写的使用方法：
```java