# JAVA
## JAVA Basic
 
### 基础注意项
#### 注意点
        大小写敏感：Java 是大小写敏感的，这就意味着标识符 Hello 与 hello 是不同的。
        主方法入口：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。
#### 注释
        单行注释：//
        多行注释：/* */
        文档注释：/** */
##### 特殊注释规范样例
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
#### 标识符
        比其他常规语言多了美元符号
#### 常见命名规范
        包名：多单词组成时所有字母都小写：xxyyzz
        类名、接口名：多单词组成时，所有单词的首字母大写：XxYyZz
        变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写：xxYyZz
        常量名：所有字母都大写。多单词时每个单词用下划线连接：XX_YY_ZZ
#### javac和java命令
        javac：编译命令，将java文件编译成class文件
        如: (Linux 环境下) javac -d ./bin ./src/**/*.java, 将src目录下所有java文件编译成class文件，输出到bin目录下,-d表示输出目录
        java：运行命令，运行class文件
        如: java -cp ./bin com.example.HelloWorld, 运行bin目录下的com.example.HelloWorld类, -cp表示类路径
#### jar包
        jar包是java的打包文件，通过对class文件进行打包，可以将多个class文件打包成一个jar包，方便传输和使用。
        jar包的创建：(Windows) 直接右键打包成zip文件，然后修改后缀名为jar
                    (Maven) mvn package, 在target目录下生成jar包

### Java的对象和类
#### 构造方法
        Java的构造方法名必须与类名相同，一个类可以有多个构造方法，构造方法可以有多个参数，构造方法没有返回值。
#### 创建对象
        三步走：
        1. 声明：声明一个对象，包括对象名称和对象类型。
        2. 实例化：使用关键字 new 来创建一个对象。
        3. 初始化：使用 new 创建对象时，会调用构造方法初始化对象。
#### Java包
        类似python, import 包名.类名
        使用 package p_name; 导入包;
        或者使用 import p_name.c_name; 导入包中的类
        包的作用域: 包名相同的类，可以直接访问不需要import。不用public, protected, private修饰的类就是包作用域。
#### 内部类
        内部类是定义在另一个类中的类。
        内部类的访问修饰符可以是 public, protected, private 以及默认访问权限。
        外部类要访问内部类的成员，必须创建内部类的对象。
        内部类可以访问外部类的所有成员，而不需要外部类对象的引用。下为例子
```java
void Outer(){
    private int x = 10;

    class Inner{
        void print(){
            System.out.println(Outer.this.x);
        }
    }
}
```
        内部类还可以是Anonymous class，即匿名类。下为例子。
```java
void asyncHello(){
    Runnable r = new Runnable(){
        public void run(){
            System.out.println("Hello World");
        }
    };
    new Thread(r).start();
}
```
        内部类还可以是静态类，即static class。静态类只能访问外部类的静态成员，不能访问外部类的非静态成员, 即不能访问.this。下为例子。
```java
class Outer{
    private static int x = 10;

    static class Inner{
        void print(){
            System.out.println(Outer.x);
        }
    }
}
```
#### JavaBean

        JavaBean 是一种符合如下标准的 Java 类：
        1. 类是公共的
        2. 有一个无参的公共构造器
        3. 有属性，且有对应的 get、set 方法
        4. 实现了 Serializable 接口
        以下为例子。
```java
public class Person implements Serializable {
    private String name;

    // 读属性(getter)
    public String getName(){
        return name;
    }
    // 写属性(setter)
    public void setName(String name){
        this.name = name;
    }
}
```
#### 枚举类
        枚举类是一种特殊的类，用于定义常量。
        枚举类的每个值都是枚举类的实例，枚举类的构造方法必须为私有。
        枚举类写法: enum ClassName{value1, value2, value3}
        枚举类好处: 1. 本身带有类型信息，编译器会检查类型错误。2. 不可能引用到非枚举的值。
        枚举类的常用方法: 1. name()：返回枚举值的名称。 2. ordinal(),返回枚举值的序号。
        以下为例子。
```java
public enum Weekday{
    SUN(0), MON(1), TUE(2), WED(3), THU(4), FRI(5), SAT(6);
    public final int dayValue;
    private Weekday(int dayValue){
        this.dayValue = dayValue;
    }
}
```

### Java变量类型
#### 局部变量
        局部变量声明在方法、构造方法或者语句块中；
        局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
        访问修饰符不能用于局部变量；
        局部变量只在声明它的方法、构造方法或者语句块中可见；
        局部变量是在栈上分配的。
#### 成员变量
        成员变量是定义在类中，方法体之外的变量，在整个类体内都可见；
        成员变量在对象创建的时候创建，在对象被销毁的时候销毁；
        访问修饰符可以修饰成员变量；
        成员变量可以被声明在使用前或者使用后；
        成员变量是在堆上分配的。
#### 类变量（静态变量）
        类变量声明在类中，方法体之外，但必须声明为static类型, 即用static修饰；
        类变量在类加载的时候创建，在程序退出的时候销毁；
        访问修饰符可以修饰类变量；
        类变量是在静态区分配的。
##### 静态变量线程安全
        类变量是全局的，所有的对象都共享同一个变量。所以，当一个对象对类变量进行修改后，其他对象访问的类变量是修改后的值。这样会造成线程安全问题。为了解决这个问题，可以使用同步关键字 synchronized，原子类，或者volatile关键字。
#### 参数变量
        参数变量是在方法调用时被传递进方法中的变量；
        方法中的参数变量在调用方法时被创建，当方法返回时，参数变量被销毁；
        参数变量只在方法内部可见；
        参数变量是在栈上分配的。

### Java修饰符
#### 访问控制修饰符
        Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。
        default：
        默认的，即不加任何修饰符，通常称为“默认访问模式“。
        访问级别：同一包内可见;不同包子类可见，非子类不可见。
        private：
        私有的，只允许在本类中进行访问。不能修饰类（外部类）。
        访问级别：本类可见; 不同包都不可见。
        public：
        公共的，允许在任何地方进行访问。
        (一个.java文件中只能有一个public类，且public类的类名必须与文件名相同。)
        访问级别：对所有类可见。
        protected：
        受保护的，允许在当前类、同一包中以及子类中进行访问。不能修饰类（外部类）。
        访问级别：本类、同一包、子类可见; 不同包都不可见。
#### 非访问修饰符
        Java中，提供了很多非访问修饰符来实现其他的功能。非访问修饰符一般位于访问修饰符之前。
        static：
        静态的，表明一个成员变量或者方法可以在没有创建类的实例的情况下使用。静态变量始终只有一个副本，无论类创建了多少个对象。静态方法只能访问静态变量。
        final：
        最终的，表明一个变量只能被赋值一次，常量。类不能被继承，方法不能被重写。通常和 static 一起使用来创建类常量。
        abstract：
        抽象的，表明一个类或者方法是抽象的，不能被实例化。抽象方法只需要声明，不需要实现。通常和接口一起使用。
        synchronized：
        同步的，表明一个方法只能被一个线程访问。同步方法必须要有一个锁，通常为当前对象。
        volatile：
        易变的，确保一个线程修改了一个变量之后，其他线程能够立即看到修改的值。通常用于多个线程访问的成员变量或者状态变量。
        transient：
        短暂的，表明一个变量不应该被序列化，通常用于socket或者文件传输中。


### Java基本运算符
        大都与python一致，此处讲讲特殊的几个运算符。
        1. 三目运算符
        三目运算符与c一致，也不赘述。
        2. instanceof 运算符
        判定对象是否为某个类的实例，返回boolean值。

### Java循环结构
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

### Java条件语句
        1. if语句
        2. if...else语句
        3. if...else if...else语句
        4. switch语句
        以上4种语句与c一致，不赘述。


### Java 核心类
#### Number类
        基础数据类型：byte, short, int, long, float, double, boolean, char
        包装器类型：Byte, Short, Integer, Long, Float, Double, Boolean, Character
        两者区别：
        1. 基础数据类型在内存中占用空间较小，包装器类型在内存中占用空间较大。
        2. 基础数据类型是直接存储在栈中的，包装器类型是存储在堆中的。
        3. 基础数据类型的默认值不是null，包装器类型的默认值是null。
        4. 包装器类型不能用==比较，只能用equals()方法比较。
        创建Number类新对象时，优先使用静态工厂方法valueOf()，而不是new。
        所有的包装类型都是不变类。
##### 装箱和拆箱
        装箱：将基本数据类型转换为包装器类型，例如将int转换为Integer，将double转换为Double。
                例子 Integer x = 5;
        拆箱：将包装器类型转换为基本数据类型，例如将Integer转换为int，将Double转换为double。
                例子 int x = new Integer(5);
##### Number & Math 常用类方法
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
#### Character 类
        Character 类用于对单个字符进行操作。
##### 转义序列
        \t, \b, \n, \r, \', \", \\
        与c一致，不赘述。
        \ddd, 表示8进制数ddd所代表的字符
        \uxxxx， 表示16进制数xxxx所代表的字符
##### Character类常用方法
        isLetter()：判断字符是否为字母
        isDigit()：判断字符是否为数字
        isWhitespace()：判断字符是否为空白字符
        isUpperCase()：判断字符是否为大写字母
        isLowerCase()：判断字符是否为小写字母
        toUpperCase()：将字符转换为大写字母
        toLowerCase()：将字符转换为小写字母
        toString()：返回字符的字符串形式，字符串长度为1

### String 与 StringBuffer & StringBuilder
#### String 类
        String 类代表字符串。Java中的字符串是不可变的，所以每次对字符串的操作都会生成一个新的字符串对象。
        String 类是不可变的，所以你一旦创建了 String 对象，那它的值就无法改变了。如果需要对字符串做很多修改，那么应该选择使用 StringBuffer & StringBuilder 类。
##### String类创建字符串
        1. 通过字面量创建字符串
        String str = "Hello World";
        2. 通过构造方法创建字符串
        String str = new String("Hello World");
        两者区别：
        通过字面量创建的字符串会被放入字符串常量池中，而通过构造方法创建的字符串不会放入字符串常量池中；
        通过字面量创建的字符串对象的引用会被放入栈中，而通过构造方法创建的字符串对象的引用不会被放入栈中。
![String类创建字符串](https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png "String类创建字符串")
##### String类常见构建方法
        1. String()：初始化一个新创建的String对象，使其表示一个空字符序列。
        2. String(byte[] bytes)：通过使用平台的默认字符集解码指定的字节数组来构造新的String。
        3. String(char[] value)：分配一个新的String，使其表示字符数组参数中当前包含的字符序列。
##### String类常用方法
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

#### StringBuffer & StringBuilder 类
        StringBuffer & StringBuilder 类是可变的，可用于字符串拼接。
        StringBuffer & StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。
        StringBuffer & StringBuilder 类的基本方法和 String 类的方法是一样的。
##### StringBuffer与StringBuilder的区别
        StringBuffer 是线程安全的，StringBuilder 是非线程安全的。
        StringBuilder 效率高于 StringBuffer，所以多数情况下建议使用 StringBuilder 类。
##### StringBuffer & StringBuilder 比String 特有的方法
        1. append()：将指定的字符串追加到此字符序列。例子：StringBuffer str = new StringBuffer("Hello"); str.append("World");
        2. reverse()：将此字符序列用其反转形式取代。例子：StringBuffer str = new StringBuffer("Hello"); str.reverse();
        3. insert()：将指定的字符串插入此字符序列中。例子：StringBuffer str = new StringBuffer("Hello"); str.insert(0, "World");
        4. delete()：移除此序列的子字符串中的字符。例子：StringBuffer str = new StringBuffer("Hello"); str.delete(0, 5);
        5. replace()：使用给定 String 中的字符替换此序列的子字符串中的字符。例子：StringBuffer str = new StringBuffer("Hello"); str.replace(0, 5, "World");




### Java数组
#### 数组
        数组是一个容器，可以同时存放多个数据值。
        数组的特点：
        1. 数组是引用数据类型
        2. 数组当中的多个数据，类型必须统一
        3. 数组的长度在程序运行期间不可改变
        Java数组大多与c一致，此处不赘述。
#### 数组的声明
        1. dataType[] arrayRefVar; // 首选的方法
        2. dataType arrayRefVar[]; // 效果相同，但不是首选方法
        3. dataType[] arrayRefVar = new dataType[arraySize];
        4. dataType[] arrayRefVar = {value0, value1, ..., valuek};

### Java方法
        Java方法是语句的集合，它们在一起执行一个功能。
        Java方法类似于c中的函数，大多不再赘述。
#### 命令行参数
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
#### 可变参数
        可变参数允许传递不同数量的参数给一个方法。它最终被转化为一个数组传递给方法，可以使用命令行参数的方法来编写可变参数的方法。
        可变参数的写法为：type... parameterName，其中 type 是参数类型，parameterName 是参数的名称。
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


### Java Stream, File & IO
##### Java Stream
        Java 中的流是一种数据传输方式，用于处理与设备、文件或者网络连接等交互的数据。
        Java 中，流是按照操作数据单位划分的，可以划分为字节流和字符流。
        字节流：以字节为单位进行数据传输，通常用于处理二进制文件，如图片、视频等。
        字符流：以字符为单位进行数据传输，通常用于处理文本文件，如txt、doc等。
        Java 中，流的操作方式分为两种：节点流和处理流。
        节点流：直接与数据源相连，读取数据或者写入数据。
        处理流：对一个已经存在的流进行连接或者封装，通过封装后的流来实现数据读取或者写入。
##### 控制台输入输出
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
##### 文件输入输出
1. FileInputStream
        FileInputStream 是 InputStream 的子类，通常用于读取二进制文件，如图片、视频等。
        初始化:
                InputStream fis = new FileInputStream("文件路径");
        FileInputStream 常见搭配输入方法: 
                fis.read() 读取一个字节
                fis.read(byte[] b, int off, int len) 读取一个字节数组的一部分
        一般的读写采用try(resource)的方式，可以实现自动关闭流，如:0
                try (InputStream fis = new FileInputStream("文件路径")) {
                        // 读取文件
                } catch (IOException e) {
                        e.printStackTrace();
                }        
2. FileOutputStream
        FileOutputStream 是 OutputStream 的子类，通常用于写入二进制文件，如图片、视频等。
        初始化:
                FileOutputStream fos = new FileOutputStream("文件路径");
        FileOutputStream 常见搭配输出方法: 
                fos.write(int b) 写入一个字节
                fos.write(byte[] b, int off, int len) 写入一个字节数组的一部分
3. Filter 模式
        Filter 模式是一种常见的设计模式，它通过对已有的流进行封装，来实现特定的功能。
        Filter 模式一般是为了防止类的爆炸，即类的数量过多，导致代码难以维护。
        JDK 将 FilexxxStream 分为两大类，一个提供直接数据，一个提供附加功能，在使用时，可以从直接类开始，不断用附加功能类对直接类进行包装，直到得到想要的全部功能。
4. 读取 classpath 资源
        Java 中，大部分项目都需要在程序启动时读取配置文件。在 Java 中，可以通过 ClassLoader 类的 getResourceAsStream() 方法来读取 classpath 下的资源文件, 以此避免路径依赖。
        如果未读到，getResourceAsStream() 方法会返回 null。
##### 序列化
        序列化是将对象转换为字节序列的过程，反序列化是将字节序列恢复为对象的过程。
        序列化的主要用途是将对象保存到文件中，或者将对象通过网络传输到另一个地方。
        Java 中，可以通过实现 Serializable 接口来实现序列化，该接口没有任何方法或者字段，只是作为一个标识。
        序列化： 将Java对象转为byte[]数组, 需要用到ObjectOutputStream类。
        反序列化：将byte[]数组转为Java对象, 需要用到ObjectInputStream类，用readObject()方法读取对象。此时可能会有两种异常，ClassNotFoundException和InvalidClassException。反序列化不调用构造方法，所以可以设置serialVersionUID作为版本号。

### 异常处理
        异常是程序在执行过程中出现的错误。
        Java 中，异常是一个对象，表示程序在执行过程中出现的错误。
        异常的分类：
        1. 检查性异常：在编译时发生的异常，如文件不存在、网络中断等。
        2. 运行时异常：在运行时发生的异常，如数组越界、除数为0等。
        3. 错误：Java 虚拟机无法解决的严重问题，如 JVM 运行错误、内存溢出等。
        一般而言：
        如果异常最后可以统一丢给Exception处理，如catch(Exception e);
        可以用printStackTrace()方法打印异常信息;
        可以将异常传入给异常类的构造方法，这会使新的异常对象包含原始异常的信息，从而让定位错误更加准确，如throw new Exception(e);
#### try...catch...finally
        Java 中，异常处理的方式有两种：try...catch...finally 和 throw/throws。
        try 用于指定一块预防异常的代码。
        catch 用于捕获异常并处理异常。
        finally 用于指定一块无论是否发生异常都会执行的代码，即使是在catch里发生异常的情况下。
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
#### throw 与 throws
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
#### 空指针异常
        NullPointerException 是 Java 中最常见的异常之一，当引用类型变量为 null 时，调用该变量的方法或者获取该变量的属性时，会发生空指针异常。
        对于空指针异常，必须遵循"早暴露，早修复"的原则，严禁使用catch(Exception e)来捕获空指针异常。
        避免空指针异常的好习惯：
        1. 变量尽量初始化，避免使用null。
        2. 返回值尽量避免使用null。
#### Java的日志
##### JDK Logging
        JDK Logging 是 Java 自带的日志框架，位于 java.util.logging 包中。
        JDK Logging 的日志级别从高到低分别为：SEVERE、WARNING、INFO、CONFIG、FINE、FINER、FINEST。
        JDK Logging 的局限: 
        1. Logging 系统在 JVM 启动时读取配置文件并完成初始化，一旦开始运行，就无法修改配置。
        2. 配置不方便，需要在 JVM 启动时传递参数"-Djava.util.logging.config.file=<config-file-name>"。
##### Commons Logging
        Commons Logging 是 Apache 提供的日志框架，位于 org.apache.commons.logging 包中。
        Commons Logging 的日志级别从高到低分别为：FATAL、ERROR、WARNNING、INFO、DEBUG、TRACE。
        Commons Logging 的特色:
        1. 可以通过配置文件挂接不同的日志系统，如 JDK Logging、Log4J、Logback 等。
        2. 只需要和两个类打交道：LogFactory 获取 Log 对象，Log 记录日志。
        3. 重载方法，可以传入异常对象，使得日志信息更加丰富。
##### Log4j
        Log4j 是 非常流行的日志框架，位于 org.apache.log4j 包中。
        Log4j 是 组件化的日志框架，包含四个组件：Appender、Layout、Filter、Console/File/Socket/JDBC 等。
        Log4j 的特色：
        通过配置log4j2.xml文件，可以实现日志的输出到控制台、文件、数据库等。



### 继承和接口
#### 关键字
        继承类用extends关键字，实现接口用implements关键字。
        继承一般是继承抽象类，本质上是定义基本变量和方法，子类可以继承父类的字段和方法，也可以重写父类的方法。
        接口本质上是定义方法，子类必须实现接口的方法，接口没有变量(可以有常量)，所有的方法(除了default方法)都是抽象方法。
#### super 与 this
        super 与 this 关键字用于在子类中访问父类的成员变量和成员方法。
        super 用于访问父类的成员变量和成员方法, this 用于访问本类的成员变量和成员方法。
#### final
        final 关键字用于声明属性、方法和类，分别表示属性不可变、方法不可覆盖、类不可继承。
        final 修饰的属性必须在声明时初始化，且不可再修改。
        final 修饰的方法不可被子类覆盖。
        final 修饰的类不可被继承。
#### 构造器
        构造器用于初始化对象，与python的__init__类似。
        构造器的名称必须与类名相同，且没有返回值。
        构造器的访问修饰符只能是 public，且不能被 static、final、synchronized 和 abstract 修饰。
        子类构造器不继承父类的构造器，但是子类构造器默认调用父类的无参构造器，如果父类没有无参构造器，则必须在子类的构造器中用 super 显式调用父类的构造器。
#### default
        default 关键字用于声明接口的默认方法。
        default 修饰的方法必须有方法体，且不能被子类覆盖。
        default 修饰的方法可以被实现接口的类调用。

### Overload & Override
#### Overload 
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
#### Override
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
public class OverrideDemo {
        public static void main(String args[]){
                OverrideDemo demo = new OverrideDemo();
                demo.test();
        }
        public void test() {
                System.out.println("父类的方法");
        }
}
public class OverrideDemoChild extends OverrideDemo {
        public static void main(String args[]){
                OverrideDemoChild demo = new OverrideDemoChild();
                demo.test();
        }
        @Override
        public void test() {
                System.out.println("子类重写父类的方法");
        }
}
```

### Java 的反射
        反射，指的是在对传入的类进行操作时，可以获取类的信息，如类名、属性、方法等。
#### Class 类
        JVM为每个加载的类都创建了一个 Class 类的对象，用于保存类的信息。获取到一个类的 Class 类的对象后，就可以通过该对象获取类的信息。
        获得 Class 类的对象的方法有三种：
        1. 直接通过类名获取，如 String.class
        2. 通过对象的 getClass() 方法获取，如 str.getClass()
        3. 通过 Class 类的 forName() 静态方法获取，如 Class.forName("java.lang.String")
        动态加载： JVM执行程序时，不是一次性将所有的类都加载到内存中，而是第一次使用时才会加载。
#### 访问字段与调用方法
        Java Class类获取字段对象的方法:
        1. getField(Name): 获取指定名称的 public 字段(包括父类)
        2. getDeclaredField(Name): 获取指定名称的字段(不包括父类)
        3. getFields(): 获取所有 public 字段(包括父类)
        4. getDeclaredFields(): 获取所有字段(不包括父类)
        Java Field类操作字段信息的方法:
        1. getName(): 获取字段名称
        2. getType(): 获取字段类型
        3. get(Object): 获取指定对象的字段值
        4. set(Object, Value): 设置指定对象的字段值
        Java Class类获取方法对象的方法:
        1. getMethod(Name, Class...): 获取指定名称和参数类型的 public 方法(包括父类)
        2. getDeclaredMethod(Name, Class...): 获取指定名称和参数类型的方法(不包括父类)
        3. getMethods(): 获取所有 public 方法(包括父类)
        4. getDeclaredMethods(): 获取所有方法(不包括父类)
        多态调用准则：总是调用实际类型的覆写方法。
        Java Class类调用构造方法:
        1. newsInstance(): 调用无参构造方法
        2. getConstructor(Class...): 获取指定参数类型的 public 构造方法
        Java Class类获得父类与接口:
        1. getSuperclass(): 获取父类
        2. getInterfaces(): 获取接口
        Java Class类获得注解:
        1. getAnnotation(Class): 获取指定类型的注解
        2. getAnnotations(): 获取所有注解
#### 动态代理
        动态代理指的是在运行时动态生成代理类，代理类可以在运行时调用任意方法。
        动态代理创建过程如下:
        1. 定义一个 InvocationHandler 实现类，实现 invoke() 方法
        2. 通过 Proxy.newProxyInstance() 方法创建interface实例, 需要三个参数:
                ClassLoader loader: 指定当前目标对象使用的类加载器, 获取加载器的方法是固定的
                Class<?>[] interfaces: 目标对象实现的接口类型, 使用泛型方式确认类型
                InvocationHandler h: 事件处理, 执行目标对象的方法时, 会触发事件处理器的方法, 会把当前执行的目标对象方法作为参数传入
        3. 将返回的 Object 强制转换为目标对象的接口
        以下实例演示了动态代理的使用方法：
```java
// 基于接口的示例
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;
public class DynamicProxyDemo {
        public static void main(String args[]){
                // 创建被代理的对象
                Subject realSubject = new RealSubject();
                // 创建一个实现了 InvocationHandler 接口的类的对象
                InvocationHandler handler = new DynamicProxy(realSubject);
                // 创建一个代理对象
                Subject proxySubject = (Subject) Proxy.newProxyInstance(handler.getClass().getClassLoader(), realSubject.getClass().getInterfaces(), handler);
                // 调用代理对象的方法
                proxySubject.request();
        }
}
interface Subject {
        void request();
}
class RealSubject implements Subject {
        @Override
        public void request() {
                System.out.println("RealSubject");
        }
}
class DynamicProxy implements InvocationHandler {
        private Object subject;
        public DynamicProxy(Object subject) {
                this.subject = subject;
        }
        @Override
        public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("Before");
                Object result = method.invoke(subject, args);
                System.out.println("After");
                return result;
        }
}
```

### Java 的注解
        注解，指的是在代码中加入元数据，用于描述代码的特性。
        注解中的属性类型可以是基本类型、String、枚举、以上类型及Class类型的数组。
        注解定义规则:
        1. 使用 @interface 定义注解
        2. 可以定义多个参数和默认值， 核心参数名称用 value
        3. 必须设置@Target指定注解的应用场合
        4. 应当设置@Retention(RetentionPolicy.RUNTIME)便于运行期读取
        注解的作用：
        1. 编译器使用的注解，如
            @Override: 检查该方法是否是重写方法，如果发现其父类，或者接口中并没有该方法时，会报编译错误。
            @SuppressWarnings: 指示编译器去忽略注解中声明的警告。
        2. 工具处理.class文件使用的注解，被底层库使用，无需自己处理。
        3. 程序运行时的注解，一般用于在运行时动态生成代码（比如反射）。
           常见的此类注解有注解的注解，即元注解，总共有5种，分别是： @Retention(生命周期)、@Target(应用场合)、@Documented(文档)、@Inherited(继承)、@Repeatable(可重复)。
           样例如下：
```java
// 注解实现反射简单示例
import java.lang.annotation.*;
import java.lang.reflect.Method;
@Retention(RetentionPolicy.RUNTIME) // 用来修饰注解，指定注解的生命周期为运行时
@Target(ElementType.METHOD) // 用来修饰注解，指定注解的应用场合为方法
public @interface Range{
        int min() default 0;
        int max() default 255;
}
public class Person{
    @Range(min=1, max=20)
    public String name;

    @Range(max=10)
    public String city;
}

// 使用注解和反射实现简单的参数检查
void check(Person person) throws IllegalArgumentException, ReflectiveOperationException {
        // 遍历所有Field
        for (Field field : person.getClass().getFields()) {
                // 获取Field定义的@Range
                Range range = field.getAnnotation(Range.class);
                if (range != null) {
                        Object value = field.get(person);
                        if (value instanceof String) {
                                String s = (String) value;
                                // 判断值是否满足@Range的min/max
                                if (s.length() < range.min() || s.length() > range.max()) {
                                        throw new IllegalArgumentException("Invalid field: " + field.getName());
                                }
                        }
                }
        }
}
```

### Java 的泛型
        泛型，指的是在定义类、接口、方法时，使用类型参数，用于指定类、接口、方法中的类型。
        泛型的作用：
        1. 提高代码的重用性
        2. 避免类型转换
        3. 提高代码的可读性
#### 向上转型
        向上转型指的是将子类对象转换为父类对象，可以使用父类引用指向子类对象。
        比如ArraryList<T> 可以向上转型为 List<T>，这样可以使得代码更加通用。(T不能变)
        但是不要把ArrayList<Integer> 向上转型为 ArrayList<Number>，因为两者之间没有继承关系。(T不能为父类)
#### 泛型使用
        在赋值后省略泛型<T>编译器会自动判断class类型;
        不指定泛型参数类型，编译器会给出警告;
        可以在接口定义泛型类型，实现接口时指定具体类型，下为例子：
```java
// 以Compareble<T> 为例
/* 
Comparable 定义:
public interface Comparable<T> {
        public int compareTo(T o);
}
*/
from java.lang import Comparable;
public class Person implements Comparable<Person> {
        public String name;
        public int age;
        public Person(String name, int age) {
                this.name = name;
                this.age = age;
        }
        @Override
        public int compareTo(Person other) {
                return this.name.compareTo(other.name);
        }
}
```
#### 泛型定义
        静态方法不能引用泛型类型<T>, 必须定义其他类型(比如<K>);
        泛型可以同时定义多个类型参数，如Map<K, V>;
#### 擦拭法
        Java 的泛型是采用擦拭法实现的，即在编译期间，所有的泛型信息都会被擦除，只保留原始类型。
        因此Java泛型存在以下局限:
        1. <T> 不是基本类型
        2. 无法取得带泛型的Class(无法用getClass() 判断类型)
        3. 不能实例化T类型, 要实例化得借助Class<T>参数, 通过反射来实例化T类型。
        4. 不恰当的覆写方法会使编译器报错，比如在某个Class里定义了equals(T t)方法，会被认为是覆写了Object.equals(Object)方法。
        如果非泛型子类继承了泛型父类，那么子类可以获取到泛型父类的类型。
#### 泛型中的通配符
##### extends 通配符
        extends 通配符指的是泛型的上限，即泛型必须是指定类型或者指定类型的子类。
        上届通配符： <? extends T> 可以赋值给 T 类型和 T 类型的子类。
        此时，方法内部可以调用获取 T 的方法，但是不能调用修改 T 的方法，即只可读不可写，如：
            <? extends Number>作为通配符，
            可以调用获取 Number 引用的方法，比如 'Number n = obj.getFirst();'(因为obj肯定是Number的子类，所以必能用Number读)
            但是不能调用修改 Number 引用的方法，比如 'obj.setFirst(new Number(100));'(因为Number不一定能转成子类obj，所以不能写)
        唯一例外： set(NULL);
##### super 通配符
        super 通配符指的是泛型的下限，即泛型必须是指定类型或者指定类型的父类。
        下届通配符： <? super T> 可以赋值给 T 类型和 T 类型的父类。
        此时，方法内部可以调用修改 T 的方法，但是不能调用获取 T 的方法，即只可写不可读，如：
            <? super Integer>作为通配符，
            可以调用修改 Integer 引用的方法，比如 'obj.setFirst(new Integer(100));'(因为obj的类型肯定是Integer的父类，所以必能写)
            但是不能调用获取 Integer 引用的方法，比如 'Integer n = obj.getFirst();'(但是obd的类型不一定能用Integer读出来，所以不能读)
        唯一例外： Object obj = p.getFirst();
##### PECS 原则
        PECS 原则指的是 Producer-Extends, Consumer-Super。
        1. 如果需要返回 T 类型，那么使用 <? extends T>。
        2. 如果需要写入 T 类型，那么使用 <? super T>。
        3. 如果需要读写 T 类型，那么不使用通配符。
        以下实例演示了泛型中的通配符的使用方法：
```java
// 以copy示例
public class Collections {
        public static <T> void copy(List<? super T> dest, List<? extends T> src) {
                for (int i = 0; i < src.size(); i++) {
                    T t = src.get(i); // src是producer
                    dest.add(t); // dest是consumer
                }
        }
}
```
#### 泛型中的反射
        待补充




### Java 的集合
        Java的集合类Collection分为三种类型：List, Set, Map。
        Java的集合设计特点：
            1. 接口和实现分离
            2. 支持泛型
            3. 访问集合元素统一通过Iterator接口
#### List
        Java的List分为两种类型：ArrayList, LinkedList。
        前者是基于数组实现的，后者是基于链表实现的。
        List快速创建： List.of("A", "B", "C");
        List遍历： for (String s : list) { ... }
        List转Array: 
            List<String> list = List.of(1, 2, 3);
            1. Object[] array = list.toArray(); 容易丢失类型信息, 不常用
            2. Integer[] array = list.toArray(new Integer[3]); 一般用toArray(new Integer[list.size()])创建"恰好"大小的数组
            3. Integer[] array = list.toArray(Integer[]::new); Java8新特性,函数式写法，最简洁
        Array转List: List<Integer> list = Arrays.asList(array);
        List的contains和indexOf方法依赖元素的equals方法，若对象里没有重写equals方法，则比较的是对象的地址。所以一般自定义类要重写equals方法。
#### Map   
        Map类似python中的dict。
        Map常用的实现类有HashMap, TreeMap, EnumMap。
        Map的顺序是不可靠的，即遍历的顺序不一定是put的顺序。
        Map的读写: 读- get(key), 写- put(key, value)。(put会自动覆盖相同key的value)
        Map的遍历: 
            1. for (String key : map.keySet()) { ... } 遍历key
            2. for (String value : map.values()) { ... } 遍历value
            3. for (Map.Entry<String, Integer> entry : map.entrySet()) { ... } 遍历key-value, entry.getKey()和entry.getValue()分别获取key和value
        HashMap的使用必须正确的实现equals()和hashCode()方法，否则，作为key的class就无法正确地比较是否相等。(比如自定义类作为key)。hashCode常用Object.hashCode()方法计算。
        EnumMap是一种特殊的Map，它要求key必须是enum类型, 它不仅效率高，而且没有额外的空间浪费。
        TreeMap是一种能够保证key有序的Map，它通过红黑树实现，key必须实现Comparable接口或者传入Comparator, 如果没有实现或者传入，则必须在创建TreeMap时传入一个自定义排序算法。
#### Properties
        Properties是Java提供的一种基于key-value存储的简单结构，常用来保存配置文件。
        读取配置文件:
            1. 创建Properties实例: Properties props = new Properties();
            2. 调用load()方法读取文件: props.load(new FileInputStream("config.properties"));
            3. 调用getProperty()方法获取配置: props.getProperty("key");
        写入配置文件:
            4. 创建Properties实例: Properties props = new Properties();
            5. 调用setProperty()方法设置配置: props.setProperty("key", "value");
            6. 调用store()方法写入文件: props.store(new FileOutputStream("config.properties"), "This is a comment line");
#### Set
        Set 就像是没有 value 的 Map，它本身是一组 key 的集合，因此，Set 不保存重复的元素。
        Set 可以用来去除重复元素。
        Set 的常用实现类有HashSet, TreeSet。
#### Queue
        Queue 是一种先进先出的队列。
        Queue 常用的实现类有LinkedList, ArrayDeque。
        LinkedList既可以当List用，也可以当Queue用，具体看抽象类引用。
        Queue的常用方法:
            1. add(E): 添加元素到队尾，如果添加失败，抛出异常
            2. offer(E): 添加元素到队尾，如果添加失败，返回false
            3. remove(): 获取队首元素并删除，如果队列为空，抛出异常
            4. poll(): 获取队首元素并删除，如果队列为空，返回null
            5. element(): 获取队首元素但不删除，如果队列为空，抛出异常
            6. peek(): 获取队首元素但不删除，如果队列为空，返回null
#### PriorityQueue
        PriorityQueue 是一种优先队列，它的特点是能保证每次取出的元素都是队列中权值最小的。
        PriorityQueue 的作用是能保证每次取出的元素都是队列中权值最小的。
        PriorityQueue 的优先级通过构造方法传入的 Comparator 对象决定，也可以实现 Comparable 接口来定义排序规则。
        其它同 Queue。
#### Deque
        Deque 是一种两端都可以操作的队列。
        Deque 的常用实现类有 ArrayDeque 和 LinkedList。
        待补充。
#### Collections
        Collections 是 Java 集合类的工具类，提供了一系列静态方法实现对集合的搜索、排序、线程安全化等操作。
        Collections 的常用方法:
            1. 排序: sort(List<T> list, Comparator<? super T> c)
            2. 洗牌: shuffle(List<?> list)
            3. 查找: binarySearch(List<? extends Comparable<? super T>> list, T key)
            4. 复制: copy(List<? super T> dest, List<? extends T> src)
            5. 最大最小值: max(Collection<? extends T> coll), min(Collection<? extends T> coll)
            6. 反转: reverse(List<?> list)
   
            
### 函数式编程
        函数式编程是一种编程范式，它将计算机运算视为数学上的函数计算，并且避免使用程序状态以及易变对象。
        Java 8 引入了函数式接口，Lambda 表达式，方法引用等新特性，使得 Java 也可以进行函数式编程。
#### Lamada 表达式
        Lambda 表达式是 Java 8 的新特性，它允许我们将一个函数作为参数传递给一个方法。
        Lambda 表达式的语法:
        1. 无参数，无返回值: () -> System.out.println("Hello");
        2. 有参数，无返回值: (int x) -> System.out.println(x);
        3. 有参数，有返回值: (int x, int y) -> { return x + y; };
        4. 有参数，有返回值(类型推断): (x, y) -> x + y;
        Lambda 表达式的使用:
        1. 作为参数传递给方法
        2. 作为返回值返回
        3. 作为变量赋值
        4. 作为方法调用
#### 方法引用
        方法引用是指使用方法的名字来替代 Lambda 表达式。
        方法引用的语法:
        1. 静态方法引用: 类名::静态方法名
        2. 实例方法引用: 实例::实例方法名
        3. 对象方法引用: 类名::实例方法名
        4. 构造方法引用: 类名::new
        方法引用的使用:
        同上。
#### 使用Stream
        Stream 是 Java 8 中处理集合的关键抽象概念，它可以对集合进行各种操作，并且支持并行处理。
        Stream 的特点:
        1. 不是数据结构，不保存数据
        2. 不会改变原对象，相反，它会返回一个持有结果的新Stream
        3. 惰性执行，只有终结操作才会执行
        Stream 的操作:
        1. 初始操作: Stream.of, Arrays.stream, Stream.generate
        2. 中间操作: filter, map, distinct(去重), sorted, limit, skip, concat(合并), parallel(并行)
        3. 终结操作: forEach, toArray, collect, reduce, count, max, min, sum, average


## Spring 
### IoC
        Ioc 称为控制反转，又称为依赖注入（DI）, 是一种设计思想，它的核心思想是将对象的创建和对象之间的调用关系交给容器来管理。Ioc 容器是一个高度可扩展的无侵入容器， 即不需要在代码中引入容器的API，只需要在配置文件中配置好对象的创建和对象之间的调用关系，容器就可以自动完成对象的创建和对象之间的调用。
        Ioc 的优点:
        1. Service 不再关心 Dao 的实现，只需要关心接口
        2. 共享组件变得非常容易
        3. 测试更加容易，因为可以使用内存数据库
        Ioc 的实现:
        1. 属性注入: 通过 setter 方法注入
        2. 构造方法注入: 通过构造方法注入
#### JavaBean
        JavaBean 是一种符合命名规范的 Java 类，在 Spring的 Ioc 容器中，所有的组件都是 JavaBean。
        xml配置文件中的bean必要标签:
        1. id: bean 的唯一标识符
        2. class: bean 的全限定类名
        Java里从Ioc容器中获取bean的方法:
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        User user = (User) context.getBean("user");
        下面是使用xml配置文件创建bean的示例:
```xml
<!-- bean 创建示例 -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <bean id="user" class="com.example.User">
            <property name="name" value="Tom"/>
            <property name="age" value="18"/>
            <property name="area" ref="area"/>
    </bean>
    <bean id="area" class="com.example.Area">
            <property name="province" value="Shanghai"/>
            <property name="city" value="Shanghai"/>
    </bean>
</beans>
```
```java
// 创建Ioc容器实例，加载配置文件
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
// 从Ioc容器中获取bean实例并使用
User user = (User) context.getBean(User.class);
String userName = user.getName();
```
        

        Annotation配置bean的注解(最常用):
        依赖创建类:
            1. @Component: 用于标注一个类为 Spring 的组件
            2. @Service: 用于标注一个类为 Spring 的 Service
            3. @Repository: 用于标注一个类为 Spring 的 Dao
            4. @Controller: 用于标注一个类为 Spring 的 Controller
        对象注入类:
            1. @Autowired: 根据类型自动装配
            2. @Inject: JSR-330 标准的注解，功能与 @Autowired 相同
            3. @Resource: 根据名称自动装配
        配置类:
            1. @Configuration: 用于标注一个类为 Spring 的配置类
            2. @ComponentScan: 用于指定 Spring 扫描的包
        Bean创建类:
            @Bean: 用于标注一个方法为 Spring 的 Bean, 该方法的返回值将被注册为一个 Bean。@Bean 注解的方法可以有参数，参数可以通过 @Autowired 注入。@Bean 注解与xml配置文件中的 <bean> 标签功能类似。@Bean 可以把第三方库的类注册为 Bean。
```java
// 使用@Component和@Autowired注解创建bean
@Component
public class User {
        private String name;
        private int age;
        private Area area;
        @Autowired
        public void setArea(Area area) {
                this.area = area;
        }
        public void setName(String name) {
                this.name = name;
        }
        public void setAge(int age) {
                this.age = age;
        }
}
```
        定制bean:
        1. @Scope: 用于指定 Bean 的作用域, 可以取值为 "singleton"(单例,默认)、"prototype"(原型)、"request"(请求)、"session"(会话)、"application"(应用)等等
        2. 注入List: 使用 @Autowired 注入 List时，Spring 会自动查找所有类型匹配的 Bean，并注入到 List 中。并且可以通过 @Order 注解指定顺序。
        3. 初始化和销毁: 使用 @PostConstruct 和 @PreDestroy 注解指定初始化和销毁方法。
        4. 使用别名: 使用 @Bean 注解的 name 属性指定别名以防止Bean重名。即@Bean(name="user")或者下方加个@Qualifier("user")。
#### Resource 和 配置注入
        Resource 是 Spring 提供的一个用于加载资源的接口，它可以加载文件系统、类路径、URL、Servlet 上下文等资源。一般用于加载配置文件。
        Resource可以通过以下方式注入：
        1. @Value("classpath:/path/to/file.txt"): 从类路径加载资源
        2. @Value("file:/path/to/file.txt"): 从文件系统加载资源
        配置注入是指将配置文件中的属性注入到 Bean 中。
        配置注入的方式有两种：
        3. @PropertySource: 用于指定配置文件的位置。只需要在@Configuration注解的类上使用@PropertySource注解指定配置文件的位置，然后在@Bean注解的方法上使用@Value注解注入属性。
        4. @Value("${key}")和@Value("#{}): 前者表示注入配置文件中的属性，后者表示从JavaBean中获取属性。

### AOP
        AOP 是一种编程范式，它的核心思想是将程序的业务逻辑和系统服务分离，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。
        AOP 本质上就是一个动态代理模式，它可以在不修改源代码的情况下，对方法进行增强。
#### Spring里使用AOP的步骤
        1. 定义执行方法，并在方法上通过AspectJ注解定义切面告诉Spring何处调用该方法(比如@Before, @After, @Around等拦截器);
        2. 标记@Component 和 @Aspect注解;
        3. 在@Configuration注解的类上使用@EnableAspectJAutoProxy注解开启AOP支持
```java
// 使用AOP的示例
@Aspect
@Component
public class LogAspect {
        @Before("execution(* com.example.service.*.*(..))")
        public void before() {
                System.out.println("Before");
        }
        @After("execution(* com.example.service.*.*(..))")
        public void after() {
                System.out.println("After");
        }
}
// 启用AOP
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {
}
```
#### 注解装配AOP
        简单装配: excution(* com.example.service.*.*(..)) 表示匹配com.example.service包下的所有类的所有方法。
        注解装配: 
        首先使用@Transaction注解标记一个方法或者类，表示该方法或者类需要事务支持。
#### AOP注意事项
        Spring 通过CGLIB创建的代理类不会调用super()，不会初始化final方法，也不会初始化父类的属性，包括final属性。(如果要访问注入后的字段，改用方法访问)

### 数据库操作
        暂略

