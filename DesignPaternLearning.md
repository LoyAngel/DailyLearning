# 设计模式(Design Patern)
### 基本概念  
#### 方法重载 (Method Overloading)  
        方法重载是指在一个类中，当有多个方法的名称相同但参数（数量或类型）不同的情况下，可以使用相同的方法名称来调用不同的方法。
##### 例子
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

// 调用示例
Calculator calculator = new Calculator();
int result1 = calculator.add(2, 3); // 输出结果：5
double result2 = calculator.add(2.5, 3.7); // 输出结果：6.2
```
#### 方法覆写(Method Overriding)
        方法覆写（重写）是指在子类中重新定义（重写）与父类中拥有相同名称和参数的方法。
##### 例子
```java
public class Animal {
    public void eat() {
        System.out.println("Animal is eating");
    }
}

public class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("Dog is eating");
    }
}

Animal animal = new Animal();
animal.eat(); // 输出结果：Animal is eating

Dog dog = new Dog();
dog.eat(); // 输出结果：Dog is eating
```
#### 接口和抽象类(Interface vs Abstract Class)  
##### 区别： 
    1. 定义方式：接口定义了一些方法的规范，而抽象类可以包含方法的实现。 
    2. 实现方式：一个类可以同时实现多个接口，但只能继承一个抽象类。 
    3. 构造函数：接口不能有构造函数，而抽象类可以有构造函数。 
    4. 成员变量：接口中的变量都是public static final类型的，而抽象类可以有各种类型的变量。
##### 接口例子：
```java
public interface Animal {
void sound();
void eat();
}

public class Cat implements Animal {
private String name;
private int age;

public Cat(String name, int age) {
    this.name = name;
    this.age = age;
}

public void sound() {
    System.out.println(name + " is meowing");
}

public void eat() {
    System.out.println(name + " is eating");
}
}

public class Dog implements Animal {
private String name;
private int age;

public Dog(String name, int age) {
    this.name = name;
    this.age = age;
}

public void sound() {
    System.out.println(name + " is barking");
}

public void eat() {
    System.out.println(name + " is eating");
}
}

// 使用接口的场景示例
Animal cat = new Cat("Kitty", 3);
cat.sound(); // 输出结果：Kitty is meowing
cat.eat(); // 输出结果：Kitty is eating
```
##### 抽象类例子：
```java
public abstract class Animal {
protected String name;
protected int age;

public Animal(String name, int age) {
    this.name = name;
    this.age = age;
}

public abstract void sound();

public void eat() {
    System.out.println(name + " is eating");
}
}

public class Cat extends Animal {
public Cat(String name, int age) {
    super(name, age);
}

@Override
public void sound() {
    System.out.println(name + " is meowing");
}
}

public class Dog extends Animal {
public Dog(String name, int age) {
    super(name, age);
}

@Override
public void sound() {
    System.out.println(name + " is barking");
}
}

// 使用抽象类的场景示例
Animal cat = new Cat("Kitty", 3);
cat.sound(); // 输出结果：Kitty is meowing
cat.eat(); // 输出结果：Kitty is eating
```
#### 泛型(Generics)
        泛型（Generics）是Java中的一个特性，它允许我们编写能够处理多种类型的代码，而不是固定于特定类型。
##### 例子
        假设我们有一个名为Box的类，用于存储某种物体。在过去，我们可能会定义Box类可以存储任何类型的对象，但在使用时，我们必须进行类型转换。而使用泛型，我们可以定义一个更通用的Box类：
```java
public class Box<T> {
private T item;

public Box(T item) {
    this.item = item;
}

public T getItem() {
    return item;
}
}
```
        在这个泛型Box类中，我们使用了一个类型参数T，在创建Box对象时，可以指定具体的类型。在使用Box对象时，无需进行类型转换，因为编译器会自动进行类型检查和类型推断。
##### 例子
```java
Box<String> stringBox = new Box<>("Hello");
String str = stringBox.getItem(); // 无需类型转换

Box<Integer> integerBox = new Box<>(123);
int num = integerBox.getItem(); // 无需类型转换
```
#### 委托和事件(Delegate vs Event)  
        委托（Delegate）是一种引用方法的类型，可以将方法视为参数传递、存储和调用。它允许我们将方法作为委托对象传递给其他方法，从而实现方法的回调和扩展。  
        事件（Event）是基于委托的机制，用于实现观察者模式。它允许对象通过定义和引发事件来通知其他对象发生了某种情况或状态的改变。
##### 例子：
```java
// 定义委托
    public delegate void OnClickDelegate();
// 委托
public class Button {
    public event OnClickDelegate OnClick;

    public void Click() {
        Console.WriteLine("Button is clicked");
        // 触发事件
        OnClick?.Invoke();
    }
}

// 定义一个响应按钮点击事件的方法
public static void HandleButtonClick() {
    Console.WriteLine("Button click event handled");
}

// 使用委托和事件的场景示例
Button button = new Button();
// 订阅按钮点击事件
button.OnClick += HandleButtonClick;

// 点击按钮
button.Click();
    事件
public class Button {
    public event EventHandler Click;

    public void OnClick() {
        Console.WriteLine("Button is clicked");
        // 触发事件
        Click?.Invoke(this, EventArgs.Empty);
    }
}

public static void HandleButtonClick(object sender, EventArgs e) {
    Console.WriteLine("Button click event handled");
}

Button button = new Button();
button.Click += HandleButtonClick;
button.OnClick();
```
### UML类图
        1. 类（Class）：用矩形框表示，框内写上类的名称。分为三部分，上面类名，中间特性（字段或属性），最后操作（方法或行为）。
        2. 属性（Attributes）：表示类的特征或状态，用名称和类型表示。属性通常写在类的顶部。例如，一个名为"age"的属性可以表示为：-age:int （"-"表示私有属性，"int"表示属性的类型）。
        3. 方法（Methods）：表示类的行为或操作，用名称和参数列表表示。方法通常写在类的底部。例如，一个名为"getName"的方法可以表示为：+getName():String （"+"表示公有方法，"String"表示方法的返回类型）。
        4. 关联关系（Association）：表示类之间的关联，通常使用实线箭头来表示。箭头指向关联的目标类。例如，如果类A和类B之间存在关联关系，可以用以下形式来表示：[A]-->[B]。
        5. 继承关系（Inheritance）：表示类之间的继承关系，通常使用空心箭头来表示。箭头指向父类。例如，如果类B继承自类A，可以用以下形式来表示：[A]<|--[B]。
        6. 实现关系（Interface）：表示类实现接口的关系，通常使用空心三角形箭头来表示。箭头指向接口。例如，如果类A实现了接口B，可以用以下形式来表示：[A]..▷[B]。
        7. 聚合关系（Aggregation）：表示整体与部分之间的关系，通常使用空心菱形箭头来表示。箭头指向整体。例如，如果类A包含一个类B的对象，可以用以下形式来表示：[B]◇-->[A]。
        8. 组合关系（Composition）：表示整体与部分之间的强关系，通常使用实心菱形箭头来表示。箭头指向整体。例如，如果类A包含一个类B的对象，并且类B的生命周期依赖于类A，可以用以下形式来表示：[B]◆-->[A]。
### 基本原则
#### 开发-封闭原则(Open-Closed Principle)
        开发-封闭是面向对象设计中的一种原则，它强调软件实体（类、模块、函数等）应该是可扩展的，而不是修改原有代码。即在程序的开发阶段，应该尽量保持对修改是封闭的，同时对扩展是开放的。
##### 例子
    ```java
    // 定义图形抽象类
    abstract class Shape {
        // ...
    }

    // 定义圆类
    class Circle extends Shape {
        private double radius;

        // ...

        public double getRadius() {
            return radius;
        }
    }

    // 定义矩形类
    class Rectangle extends Shape {
        private double width;
        private double height;

        // ...

        public double getWidth() {
            return width;
        }

        public double getHeight() {
            return height;
        }
    }

    // 定义计算面积接口
    interface AreaCalculator {
        double calculateArea();
    }

    // 圆实现计算面积接口
    class CircleAreaCalculator implements AreaCalculator {
        private Circle circle;

        public CircleAreaCalculator(Circle circle) {
            this.circle = circle;
        }

        @Override
        public double calculateArea() {
            return Math.PI * circle.getRadius() * circle.getRadius();
        }
    }

    // 矩形实现计算面积接口
    class RectangleAreaCalculator implements AreaCalculator {
        private Rectangle rectangle;

        public RectangleAreaCalculator(Rectangle rectangle) {
            this.rectangle = rectangle;
        }

        @Override
        public double calculateArea() {
            return rectangle.getWidth() * rectangle.getHeight();
        }
    }

    // 使用示例
    public class Main {
        public static void main(String[] args) {
            Circle circle = new Circle();
            circle.setRadius(3.0);
            AreaCalculator circleAreaCalculator = new CircleAreaCalculator(circle);
            double circleArea = circleAreaCalculator.calculateArea();
            System.out.println("Circle area: " + circleArea);

            Rectangle rectangle = new Rectangle();
            rectangle.setWidth(4.0);
            rectangle.setHeight(5.0);
            AreaCalculator rectangleAreaCalculator = new RectangleAreaCalculator(rectangle);
            double rectangleArea = rectangleAreaCalculator.calculateArea();
            System.out.println("Rectangle area: " + rectangleArea);
        }
    }
    ```
以上例子，体现了开发-封闭原则，我们可以通过实现AreaCalculator接口来扩展计算面积的功能，而不需要修改原有代码。
#### 单一职责原则(Single Responsibility Principle)
    单一职责是面向对象设计原则之一，它要求一个类应该只有一个引起它变化的原因，即一个类应该只有一个职责。
##### 例子
```java
public class FileHandler {
    public void readFile(String filepath) {
        // 读取文件的逻辑
    }

    public void writeFile(String filepath, String content) {
        // 写入文件的逻辑
    }

    public void deleteFile(String filepath) {
        // 删除文件的逻辑
    }
}

public class FileValidator {
    public boolean validateFile(String filepath) {
        // 验证文件的逻辑
        // 返回true或false
    }
}

public class FileProcessor {
    private FileHandler fileHandler;
    private FileValidator fileValidator;

    // 构造函数

    public void processFile(String filepath) {
        if (fileValidator.validateFile(filepath)) {
            fileHandler.readFile(filepath);
            // 处理文件的逻辑
            fileHandler.writeFile(filepath, "Processed content");
        } else {
                // 文件验证失败的处理逻辑
        }
    }
}
```
以上例子，体现了单一职责原则，我们将文件处理的逻辑拆分到了不同的类中，使得每个类只负责一个职责。
#### 依赖倒转原则(Dependency Inversion Principle)
        依赖倒转（Dependency Inversion Principle）是面向对象设计中的一条原则，它指导我们如何组织和设计代码，以便实现代码的可扩展性和灵活性。该原则的核心思想是高层模块不应该依赖于低层模块的具体实现，而是依赖于抽象。  
        简单来说，依赖倒转模式要求我们通过抽象来解耦高层模块与低层模块之间的关系，而不是直接依赖于具体的实现类。这样做的好处是，当需要修改低层模块的实现时，高层模块不会受到影响，只需要修改抽象接口的实现即可。
#####     例子
```java
// 抽象接口
interface Switchable {
    void on();
    void off();
}

// 电视类（低层模块）
class Television implements Switchable {
    public void on() {
        System.out.println("电视已打开");
    }

    public void off() {
        System.out.println("电视已关闭");
    }
}

// 遥控器类（高层模块）
class RemoteControl {
    private Switchable switchable;

    public RemoteControl(Switchable switchable) {
        this.switchable = switchable;
    }

    public void turnOn() {
        switchable.on();
    }

    public void turnOff() {
        switchable.off();
    }
}

// 测试类
public class Main {
    public static void main(String[] args) {
        // 创建一个电视对象
        Television television = new Television();

        // 创建一个遥控器对象，并将电视对象注入遥控器中
        RemoteControl remoteControl = new RemoteControl(television);

        // 通过遥控器打开电视
        remoteControl.turnOn();
        // 通过遥控器关闭电视
        remoteControl.turnOff();
    }
}
```
以上例子，体现了依赖倒转原则，我们通过抽象接口Switchable来解耦高层模块RemoteControl与低层模块Television之间的关系，使得高层模块不依赖于低层模块的具体实现。
#### 迪米特原则(Law of Demeter)  
        迪米特模式也被称为最少知识原则，它是一种设计模式，旨在减少耦合度，提高系统的可维护性和可扩展性。  
        简单来说，迪米特模式的核心思想是尽量降低类与类之间的依赖关系。一个对象应当尽可能不了解其他对象的内部细节，只和自己的朋友打交道。
#####     例子：
```java
// 以一个购物场景为例，假设有三个类：购物车（ShoppingCart）、商品（Product）和用户（User）。
// 首先，我们创建一个购物车类 ShoppingCart
public class ShoppingCart {
    private List<Product> products;

    public ShoppingCart() {
        products = new ArrayList<>();
    }

    public void addProduct(Product product) {
        products.add(product);
    }

    public int getProductCount() {
        return products.size();
    }
}
// 然后，我们创建一个商品类 Product
public class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getProductInfo() {
        return name + ": $" + price;
    }
}
// 最后，我们创建一个用户类 User
public class User {
    private ShoppingCart shoppingCart;

    public User() {
        shoppingCart = new ShoppingCart();
    }

    public void buyProduct(Product product) {
        shoppingCart.addProduct(product);
    }
}
```
以上例子中，购物车（ShoppingCart）只与商品（Product）和用户（User）类直接交互，并不知道具体商品或用户的内部实现细节。这样，购物车只需要和自己的朋友打交道，降低了系统的耦合度。
#### 里氏代换原则(Liskov Substitution Principle)
        里氏代换原则是面向对象设计中的一条原则，它是对开发-封闭原则的一个补充。里氏代换原则要求，子类必须能够替换掉它们的父类型。也就是说，在使用继承时，只要父类出现的地方，子类就可以出现，而且替换为子类也不会产生任何错误或异常，使用者可能根本就不需要知道是父类还是子类。
##### 例子：
```java
// 定义一个图形抽象类
abstract class Shape {
    public abstract double getArea();
}
// 定义圆类
class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
// 定义矩形类
class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double getArea() {
        return width * height;
    }
}
// 定义计算面积的工具类
class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.getArea();
    }
}
// 测试类
public class Main {
    public static void main(String[] args) {
        AreaCalculator areaCalculator = new AreaCalculator();

        Circle circle = new Circle(3.0);
        double circleArea = areaCalculator.calculateArea(circle);
        System.out.println("Circle area: " + circleArea);

        Rectangle rectangle = new Rectangle(4.0, 5.0);
        double rectangleArea = areaCalculator.calculateArea(rectangle);
        System.out.println("Rectangle area: " + rectangleArea);
    }
}
```
以上例子，体现了里氏代换原则，我们可以将Shape类型的变量替换为其子类Circle或Rectangle，而不会影响计算面积的逻辑。
#### 接口隔离原则(Interface Segregation Principle)
        接口隔离原则是面向对象设计中的一条原则，它要求接口的设计要尽量小而专，不要让接口承担过多的职责。如果一个接口承担了过多的职责，那么就应该将它拆分成多个更小的接口，以此来降低系统的耦合度，提高系统的可维护性和可扩展性。
##### 例子：
```java
// 定义一个图形接口
interface Shape {
    double getArea();
}
// 定义一个三维图形接口
interface SolidShape {
    double getVolume();
}
// 定义一个可旋转图形接口
interface Rotatable {
    void rotate(float degree);
}
// 定义一个可放大缩小的图形接口
interface Resizable {
    void resize(int percent);
}
// 定义一个圆类
class Circle implements Shape, Rotatable {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public void rotate(float degree) {
        // 旋转圆形
    }
}
// 定义一个球类
class Sphere implements Shape, SolidShape, Rotatable {
    private double radius;

    public Sphere(double radius) {
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return 4 * Math.PI * radius * radius;
    }

    @Override
    public double getVolume() {
        return 4 / 3 * Math.PI * radius * radius * radius;
    }

    @Override
    public void rotate(float degree) {
        // 旋转球体
    }
}
// 定义一个长方形类
class Rectangle implements Shape, Rotatable, Resizable {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double getArea() {
        return width * height;
    }

    @Override
    public void rotate(float degree) {
        // 旋转长方形
    }

    @Override
    public void resize(int percent) {
        // 放大或缩小长方形
    }
}
// 定义一个正方形类
class Square implements Shape, Rotatable, Resizable {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    public double getArea() {
        return side * side;
    }

    @Override
    public void rotate(float degree) {
        // 旋转正方形
    }

    @Override
    public void resize(int percent) {
        // 放大或缩小正方形
    }
}
// 测试类
public class Main {
    public static void main(String[] args) {
        Shape circle = new Circle(3.0);
        System.out.println("Circle area: " + circle.getArea());

        Shape sphere = new Sphere(3.0);
        System.out.println("Sphere area: " + sphere.getArea());
        System.out.println("Sphere volume: " + ((Sphere) sphere).getVolume());

        Shape rectangle = new Rectangle(4.0, 5.0);
        System.out.println("Rectangle area: " + rectangle.getArea());

        Shape square = new Square(3.0);
        System.out.println("Square area: " + square.getArea());
    }
}
```
以上例子，体现了接口隔离原则，我们将Shape接口拆分成了Shape、SolidShape、Rotatable和Resizable四个接口，每个接口都只包含一个职责，这样做的好处是，当我们需要实现某个接口时，只需要实现该接口的一个或多个方法即可，而不需要像之前那样实现所有的方法。
#### 合成复用原则(Composite Reuse Principle)
        合成复用原则是面向对象设计中的一条原则，它要求尽量使用合成/聚合的方式，而不是使用继承。
##### 例子：
```java
// 定义一个水果类
class Fruit {
    private String name;
    private double price;

    public Fruit(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getFruitInfo() {
        return name + ": $" + price;
    }
}
// 定义一个水果盘类
class FruitPlate {
    private List<Fruit> fruits;

    public FruitPlate() {
        fruits = new ArrayList<>();
    }

    public void addFruit(Fruit fruit) {
        fruits.add(fruit);
    }

    public void removeFruit(Fruit fruit) {
        fruits.remove(fruit);
    }

    public void showFruitPlate() {
        for (Fruit fruit : fruits) {
            System.out.println(fruit.getFruitInfo());
        }
    }
}
// 测试类
public class Main {
    public static void main(String[] args) {
        FruitPlate fruitPlate = new FruitPlate();
        fruitPlate.addFruit(new Fruit("Apple", 2.0));
        fruitPlate.addFruit(new Fruit("Banana", 3.0));
        fruitPlate.addFruit(new Fruit("Orange", 4.0));
        fruitPlate.showFruitPlate();
    }
}
```
以上例子，体现了合成复用原则，我们将水果盘（FruitPlate）类中的水果（Fruit）类作为其成员变量，而不是将水果盘类继承自水果类。

### 23种模式
#### 简单工厂模式  
        它提供一个统一的接口来创建不同类型的对象，客户端通过这个接口来获取具体的对象，而无需直接关心对象的创建细节。
##### 例子：
```java
// 抽象类
public interface Coffee {
    void prepare();
}
// 具体类
public class Latte implements Coffee {
    @Override
    public void prepare() {
        System.out.println("Preparing Latte...");
    }
}
public class Americano implements Coffee {
    @Override
    public void prepare() {
        System.out.println("Preparing Americano...");
    }
}

public class Cappuccino implements Coffee {
    @Override
    public void prepare() {
        System.out.println("Preparing Cappuccino...");
    }
}
// 简单工厂模式
public class CoffeeFactory {
    public Coffee createCoffee(String type) {
        Coffee coffee = null;

        switch (type) {
            case "Latte":
                coffee = new Latte();
                break;
            case "Americano":
                coffee = new Americano();
                break;
            case "Cappuccino":
                coffee = new Cappuccino();
                break;
            default:
                throw new IllegalArgumentException("Invalid coffee type: " + type);
        }

        return coffee;
    }
}
```
#### 策略模式  
        策略模式是一种行为设计模式，用于在运行时选择算法的方法。它允许你在多个算法之间进行切换或选择，而不需要更改类的实现。换句话说，它将算法与其使用者分离。
##### 例子：
```java
// 定义战斗策略接口
interface FightStrategy {
    void fight();
}

// 不同敌人的战斗策略实现类
class DragonStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用火焰攻击，对龙造成伤害");
    }
}

class GoblinStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用长剑攻击，对哥布林造成伤害");
    }
}

class SkeletonStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用弓箭攻击，对骷髅造成伤害");
    }
}

// 游戏角色类
class Warrior {
    private FightStrategy fightStrategy;

    // 设置战斗策略
    public void setFightStrategy(FightStrategy strategy) {
        this.fightStrategy = strategy;
    }

    // 战斗方法调用战斗策略
    public void fight() {
        if (fightStrategy != null) {
            fightStrategy.fight();
        }
    }
}

// 测试
public class Main {
    public static void main(String[] args) {
        Warrior warrior = new Warrior();

        // 设置不同的敌人策略
        warrior.setFightStrategy(new DragonStrategy());
        warrior.fight();

        warrior.setFightStrategy(new GoblinStrategy());
        warrior.fight();

        warrior.setFightStrategy(new SkeletonStrategy());
        warrior.fight();
    }
}
    
```
        策略模式一般与简单工厂相结合，让客户端和算法彻底分离。
##### 例子：
```java
// 定义战斗策略接口
interface FightStrategy {
    void fight();
}

// 不同敌人的战斗策略实现类
class DragonStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用火焰攻击，对龙造成伤害");
    }
}

class GoblinStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用长剑攻击，对哥布林造成伤害");
    }
}

class SkeletonStrategy implements FightStrategy {
    @Override
    public void fight() {
        System.out.println("使用弓箭攻击，对骷髅造成伤害");
    }
}

// 策略工厂类
class StrategyFactory {
    // 根据敌人类型创建战斗策略
    public static FightStrategy createStrategy(String enemyType) {
        switch (enemyType) {
            case "dragon":
                return new DragonStrategy();
            case "goblin":
                return new GoblinStrategy();
            case "skeleton":
                return new SkeletonStrategy();
            default:
                throw new IllegalArgumentException("无效的敌人类型");
        }
    }
}

// 游戏角色类
class Warrior {
    private FightStrategy fightStrategy;

    // 设置战斗策略
    public void setFightStrategy(FightStrategy strategy) {
        this.fightStrategy = strategy;
    }

    // 战斗方法调用战斗策略
    public void fight() {
        if (fightStrategy != null) {
            fightStrategy.fight();
        }
    }
}

// 测试
public class Main {
    public static void main(String[] args) {
        Warrior warrior = new Warrior();

        // 使用策略工厂创建不同敌人的策略
        FightStrategy dragonStrategy = StrategyFactory.createStrategy("dragon");
        warrior.setFightStrategy(dragonStrategy);
        warrior.fight();

        FightStrategy goblinStrategy = StrategyFactory.createStrategy("goblin");
        warrior.setFightStrategy(goblinStrategy);
        warrior.fight();

        FightStrategy skeletonStrategy = StrategyFactory.createStrategy("skeleton");
        warrior.setFightStrategy(skeletonStrategy);
        warrior.fight();
    }
}
```
#### 装饰模式  
        装饰模式是一种设计模式，它允许你在不修改已有对象的基础上，动态地给对象添加额外的功能。它采用了一种包装的方式，将对象放入一个装饰器对象中，然后用装饰器对象来扩展该对象的功能。
##### 例子：
```java
// 定义一个手机接口，里面包含基本的手机功能
public interface Phone {
    void makeCall(String number);
    void sendText(String message);
}
// 创建一个智能手机类，实现手机接口
public class SmartPhone implements Phone {
    @Override
    public void makeCall(String number) {
        System.out.println("打电话给：" + number);
    }
    @Override
    public void sendText(String message) {
        System.out.println("发送信息：" + message);
    }
}
//接下来，创建一个手机装饰器类，用于扩展手机的功能
public abstract class PhoneDecorator implements Phone {
    protected Phone decoratedPhone;

    public PhoneDecorator(Phone phone) {
        this.decoratedPhone = phone;
    }

    @Override
    public void makeCall(String number) {
        decoratedPhone.makeCall(number);
    }

    @Override
    public void sendText(String message) {
        decoratedPhone.sendText(message);
    }
}
// 创建具体的装饰器类，例如防水装饰器和快速充电装饰器
public class WaterproofPhoneDecorator extends PhoneDecorator {
    public WaterproofPhoneDecorator(Phone phone) {
        super(phone);
    }

    @Override
    public void makeCall(String number) {
        System.out.println("正在打电话之前，启用防水功能");
        decoratedPhone.makeCall(number);
    }

    @Override
    public void sendText(String message) {
        System.out.println("正在发送信息之前，启用防水功能");
        decoratedPhone.sendText(message);
    }
}

public class FastChargingPhoneDecorator extends PhoneDecorator {
    public FastChargingPhoneDecorator(Phone phone) {
        super(phone);
    }

    @Override
    public void makeCall(String number) {
        System.out.println("正在打电话之前，启用快速充电功能");
        decoratedPhone.makeCall(number);
    }

    @Override
    public void sendText(String message) {
        System.out.println("正在发送信息之前，启用快速充电功能");
        decoratedPhone.sendText(message);
    }
}
// 通过组合装饰器来给智能手机添加额外的功能
Phone smartPhone = new SmartPhone();
smartPhone = new WaterproofPhoneDecorator(smartPhone);
smartPhone = new FastChargingPhoneDecorator(smartPhone);

smartPhone.makeCall("123456789");
smartPhone.sendText("Hello!");

// 通过装饰模式，你可以在不修改现有智能手机类的情况下，动态地给手机添加防水和快速充电功能。      
```
#### 代理模式  
        代理模式是一种结构型设计模式，用于提供一个代理对象来控制对另一个对象的访问。
        通俗地说，我们可以把代理理解为一个中间人，它可以帮助我们进行一些操作，而不需要直接与目标对象进行交互。代理模式在实际应用中常用于隐藏真实对象的复杂性、实现权限控制、延迟加载等。
##### 例子：
```java
// 创建真实的音乐播放器类 MusicPlayer，实现音乐接口，并实现播放音乐的具体逻辑。
public class MusicPlayer implements Music {
    private String song;

    public void setSong(String song) {
        this.song = song;
    }

    @Override
    public void play() {
        System.out.println("正在播放音乐：" + song);
    }
}
// 接下来创建一个代理类 MusicPlayerProxy，它也实现音乐接口，并持有一个真实的音乐播放器对象。
public class MusicPlayerProxy implements Music {
    private MusicPlayer musicPlayer;

    public MusicPlayerProxy(String song) {
        musicPlayer = new MusicPlayer();
        musicPlayer.setSong(song);
    }

    @Override
    public void play() {
        // 在调用真实播放器前，可以做一些额外的操作，比如权限验证、日志记录等
        System.out.println("正在验证用户权限...");

        // 调用真实播放器的播放方法
        musicPlayer.play();
    }
}
// 最后，可以通过代理类创建一个音乐播放器对象，并调用播放音乐的方法。
public class Main {
    public static void main(String[] args) {
        Music musicPlayerProxy = new MusicPlayerProxy("《Let It Go》");
        musicPlayerProxy.play();
    }
}
// 在上述例子中，MusicPlayerProxy 作为代理类，帮助控制了用户对音乐播放器对象的访问。
// 它在调用真实播放器对象的播放方法之前，可以执行一些额外的操作:
// 比如权限验证。这样可以确保用户具有播放音乐的权限，并且将一些额外的处理与核心功能分离开来。
```
#### 工厂方法模式  
        工厂方法模式是一种创建型设计模式，用于创建对象的方法不是在对象自身的类中定义，而是通过一个工厂类来创建对象。
        通俗地说，工厂方法模式就像是一个工厂，能够根据客户端的需求动态地生产出不同的产品。客户端只需要告诉工厂需要什么产品，而无需关心具体的产品创建细节。
##### 例子：
```java
// 假设我们要开发一个电商网站，其中有多种商品需要销售
// 首先定义一个商品接口 Product，它包含一个展示商品的方法 display()
public interface Product {
    void display();
}
// 然后，创建多个具体的商品类，实现商品接口，并实现展示商品的具体逻辑。
public class Laptop implements Product {
    @Override
    public void display() {
        System.out.println("这是一台笔记本电脑");
    }
}

public class Phone implements Product {
    @Override
    public void display() {
        System.out.println("这是一部手机");
    }
}

// 接下来，创建一个工厂接口 ProductFactory，定义一个创建商品的方法 createProduct()
public interface ProductFactory {
    Product createProduct();
}
// 然后创建多个具体的工厂类，实现工厂接口，并实现创建商品的具体逻辑。
public class LaptopFactory implements ProductFactory {
    @Override
    public Product createProduct() {
        return new Laptop();
    }
}

public class PhoneFactory implements ProductFactory {
    @Override
    public Product createProduct() {
        return new Phone();
    }
}
// 最后，可以通过具体的工厂类创建商品对象，并调用展示商品的方法。
public class Main {
    public static void main(String[] args) {
        ProductFactory productFactory = new LaptopFactory();
        Product product = productFactory.createProduct();
        product.display();
    }
}

// 在上述例子中，根据客户端的需求，通过具体的工厂类 LaptopFactory 
// 创建了一个笔记本电脑商品对象并调用了展示商品的方法。
// 客户端只需要告诉工厂需要什么商品，而无需了解商品的创建细节。
// 这样可以将客户端与具体商品的创建过程解耦，使得系统更加灵活和可扩展。
```      
##### 简单工厂和工厂方法的区别
        简单工厂模式是由一个工厂类根据传入的参数决定创建哪种类型的对象。它适合只有少量对象类型需要创建的情况，但是随着对象类型增多，工厂类的责任会变得越来越重，代码的维护和扩展性会变差。
        工厂方法模式是将对象的创建交给具体的子类去实现，每个子类负责创建一种具体的对象。它可以更灵活地扩展和替换对象的创建逻辑。工厂方法模式适用于创建产品族或者有多个产品维度的情况。
##### 例子：
        例如，假设有一个汽车制造工厂，根据用户的选择，可以制造不同种类的汽车，比如小汽车和卡车。
```java
public interface Car {
    void drive();
}
```
##### 简单工厂模式
```java
public class CarFactory {
    public static Car createCar(String type) {
        if (type.equals("sedan")) {
            return new SedanCar();
        } else if (type.equals("truck")) {
            return new TruckCar();
        } else {
            throw new IllegalArgumentException("Invalid car type");
        }
    }
}

public class SedanCar implements Car {
    @Override
    public void drive() {
        System.out.println("Driving a sedan car");
    }
}

public class TruckCar implements Car {
    @Override
    public void drive() {
        System.out.println("Driving a truck car");
    }
}

public class Main {
    public static void main(String[] args) {
        Car sedan = CarFactory.createCar("sedan");
        sedan.drive();

        Car truck = CarFactory.createCar("truck");
        truck.drive();
    }
}
```
##### 工厂方法模式
```java
public interface CarFactory {
    Car createCar();
}

public class SedanCarFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new SedanCar();
    }
}

public class TruckCarFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new TruckCar();
    }
}

public class SUVCarFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new SUVCar();
    }
}

public class SportsCarFactory implements CarFactory {
    @Override
    public Car createCar() {
        return new SportsCar();
    }
}

// 具体车型的定义和实现同上

public class Main {
    public static void main(String[] args) {
        CarFactory sedanFactory = new SedanCarFactory();
        Car sedan = sedanFactory.createCar();
        sedan.drive();

        CarFactory truckFactory = new TruckCarFactory();
        Car truck = truckFactory.createCar();
        truck.drive();

        CarFactory suvFactory = new SUVCarFactory();
        Car suv = suvFactory.createCar();
        suv.drive();

        CarFactory sportsCarFactory = new SportsCarFactory();
        Car sportsCar = sportsCarFactory.createCar();
        sportsCar.drive();
    }
}
```
##### 抽象工厂和工厂方法的区别
        抽象工厂模式是一种创建一族相关或相互依赖的对象的设计模式。在抽象工厂模式中，有一个抽象工厂类定义了一系列相关的产品的创建方法，具体的产品创建则由其子类工厂来实现。每个子类工厂可以创建不同种类的产品，但这些产品之间有着相互的关联或依赖关系。
        工厂方法模式是一种创建单一对象的设计模式。在工厂方法模式中，有一个抽象工厂类定义了一个创建产品的方法，具体的产品创建则由其子类工厂来实现。每个子类工厂只能创建一种类型的产品。
##### 抽象工厂模式
```java
// 抽象工厂模式
// 定义抽象工厂类
abstract class AbstractFactory {
    // 创建产品A的方法
    public abstract ProductA createProductA();
    // 创建产品B的方法
    public abstract ProductB createProductB();
}

// 具体的产品A
class ProductA {
    // 产品A的具体实现
}

// 具体的产品B
class ProductB {
    // 产品B的具体实现
}

// 子类工厂1实现抽象工厂
class ConcreteFactory1 extends AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ProductA();
    }

    @Override
    public ProductB createProductB() {
        return new ProductB();
    }
}

// 子类工厂2实现抽象工厂
class ConcreteFactory2 extends AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ProductA();
    }

    @Override
    public ProductB createProductB() {
        return new ProductB();
    }
}
```
##### 工厂方法模式
```java
// 工厂方法模式
// 定义抽象工厂类
abstract class Factory {
    // 创建产品的方法
    public abstract Product createProduct();
}

// 具体的产品
class Product {
    // 产品的具体实现
}

// 子类工厂1实现工厂
class ConcreteFactory1 extends Factory {
    @Override
    public Product createProduct() {
        return new Product();
    }
}

// 子类工厂2实现工厂
class ConcreteFactory2 extends Factory {
    @Override
    public Product createProduct() {
        return new Product();
    }
}
```
#### 原型模式  
        原型模式 (Prototype Pattern) 是一种创建对象的设计模式，它允许我们通过复制现有对象来创建新对象，而不需要通过调用构造函数。通俗地说，原型模式就像是制作复制品的工厂，它通过复制一个现有对象来创建新对象。
##### 例子：
```java
class Person implements Cloneable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    protected Person clone() throws CloneNotSupportedException {
        return (Person) super.clone();
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Person prototype = new Person("John", 25);
        Person newInstance = prototype.clone();

        System.out.println("Prototype: " + prototype.getName() + ", " + prototype.getAge());
        System.out.println("New Instance: " + newInstance.getName() + ", " + newInstance.getAge());
    }
}
```
#### 模版方法模式  
        模板方法模式 (Template Method Pattern) 是一种行为型设计模式，它定义了一个算法框架，并将一些步骤推迟到子类中实现。通俗地说，模板方法模式就像是一个制定了步骤的流程模板，其中一些步骤可以由子类来自定义。
##### 例子：
```java
abstract class Beverage {
    final void prepareBeverage() {
        boilWater();
        brew();
        pourInCup();
        addCondiments();
    }

    private void boilWater() {
        System.out.println("Boiling water...");
    }

    abstract void brew();

    private void pourInCup() {
        System.out.println("Pouring into cup...");
    }

    abstract void addCondiments();
}

class Coffee extends Beverage {
    @Override
    void brew() {
        System.out.println("Brewing coffee...");
    }

    @Override
    void addCondiments() {
        System.out.println("Adding milk and sugar...");
    }
}

class Tea extends Beverage {
    @Override
    void brew() {
        System.out.println("Steeping tea...");
    }

    @Override
    void addCondiments() {
        System.out.println("Adding lemon...");
    }
}

public class Main {
    public static void main(String[] args) {
        Beverage coffee = new Coffee();
        coffee.prepareBeverage();

        System.out.println("----------------------");

        Beverage tea = new Tea();
        tea.prepareBeverage();
    }
}
```
#### 外观模式  
        外观模式是一种结构型设计模式，它提供了一个统一简化的接口，以隐藏复杂的子系统，并使客户端能够更方便地使用子系统。外观模式通过创建一个高层接口，将子系统的相关功能进行封装，使得客户端只需要调用这个高层接口就可以完成操作。
##### 例子：
```java
// 子系统类A
class SubSystemA {
    public void operationA() {
        System.out.println("操作A");
    }
}

// 子系统类B
class SubSystemB {
    public void operationB() {
        System.out.println("操作B");
    }
}

// 子系统类C
class SubSystemC {
    public void operationC() {
        System.out.println("操作C");
    }
}

// 外观类
class Facade {
    private SubSystemA subsystemA;
    private SubSystemB subsystemB;
    private SubSystemC subsystemC;

    public Facade() {
        subsystemA = new SubSystemA();
        subsystemB = new SubSystemB();
        subsystemC = new SubSystemC();
    }

    public void operation() {
        subsystemA.operationA();
        subsystemB.operationB();
        subsystemC.operationC();
    }
}

// 客户端类
public class Main {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.operation();
    }
}
```
#### 建造者模式  
        建造者模式是一种创建型设计模式，它用于将对象的构建与表示分离，并通过一个统一的接口逐步构建复杂对象。它允许使用相同的构建过程来创建不同的表示。
##### 例子：  
        客户端通过创建指挥者对象，使用指挥者对象调用相应的建造者方法来构建特定类型的汽车对象，并通过调用汽车对象的getter方法获取属性值。这样，我们可以根据需要创建不同属性的汽车对象，而不需要直接操作构建过程中的细节。
```java
// 汽车类
class Car {
    private String color;
    private String engineType;
    private String tireType;

    public void setColor(String color) {
        this.color = color;
    }

    public void setEngineType(String engineType) {
        this.engineType = engineType;
    }

    public void setTireType(String tireType) {
        this.tireType = tireType;
    }

    public String getColor() {
        return color;
    }

    public String getEngineType() {
        return engineType;
    }

    public String getTireType() {
        return tireType;
    }
}

// 建造者接口
interface CarBuilder {
    void setColor(String color);
    void setEngineType(String engineType);
    void setTireType(String tireType);
    Car build();
}

// 具体建造者类
class SedanCarBuilder implements CarBuilder {
    private Car car;

    public SedanCarBuilder() {
        this.car = new Car();
    }

    public void setColor(String color) {
        car.setColor(color);
    }

    public void setEngineType(String engineType) {
        car.setEngineType(engineType);
    }

    public void setTireType(String tireType) {
        car.setTireType(tireType);
    }

    public Car build() {
        return car;
    }
}

// 指挥者类
class CarDirector {
    public Car constructSedanCar() {
        CarBuilder builder = new SedanCarBuilder();

        builder.setColor("Red");
        builder.setEngineType("V6");
        builder.setTireType("Sport");

        return builder.build();
    }
}

// 客户端类
public class Main {
    public static void main(String[] args) {
        CarDirector director = new CarDirector();
        Car sedanCar = director.constructSedanCar();

        System.out.println("汽车颜色：" + sedanCar.getColor());
        System.out.println("汽车引擎：" + sedanCar.getEngineType());
        System.out.println("汽车轮胎：" + sedanCar.getTireType());
    }
}
```
#### 观察者模式  
        观察者模式是一种行为型设计模式，用于对象之间的一对多依赖关系。当一个对象的状态发生变化时，它会自动通知所有依赖它的对象，使得这些对象能够自动更新自己的状态。
##### 例子：
```java
// 观察者接口，定义观察者需要实现的方法
interface Observer {
    void update(String message);
}

// 购物平台类，主题类
class ShoppingPlatform {
    private List<Observer> observers = new ArrayList<>();

    // 注册观察者
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    // 取消观察者
    public void unregisterObserver(Observer observer) {
        observers.remove(observer);
    }

    // 通知观察者
    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }

    // 生成新订单
    public void generateOrder() {
        // 生成订单的逻辑

        // 通知管理员有新订单
        notifyObservers("New order generated");
    }
}

// 管理员类，观察者类
class Admin implements Observer {
    private String name;

    public Admin(String name) {
        this.name = name;
    }

    // 当有通知时更新消息
    public void update(String message) {
        System.out.println("Admin " + name + " received notification: " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        // 创建购物平台
        ShoppingPlatform platform = new ShoppingPlatform();

        // 创建管理员
        Admin admin1 = new Admin("Alice");
        Admin admin2 = new Admin("Bob");

        // 注册管理员为观察者
        platform.registerObserver(admin1);
        platform.registerObserver(admin2);

        // 生成订单
        platform.generateOrder();

        // 输出：
        // Admin Alice received notification: New order generated
        // Admin Bob received notification: New order generated
    }
}
```
#### 状态模式  
        状态模式是一种设计模式，它允许对象在不同的状态下表现出不同的行为。通俗地说，就好像一个人可以根据自己的心情和状态做不同的事情一样。
##### 例子：
```java 
// 定义一个抽象的状态接口
interface State {
    void doAction(Context context);
}

// 创建具体的状态类1
class ConcreteState1 implements State {
    @Override
    public void doAction(Context context) {
        System.out.println("当前状态是状态1");
        // 根据状态1的逻辑处理相应的行为
        context.setState(new ConcreteState2()); // 在状态1的逻辑处理完成后，切换到状态2
    }
}

// 创建具体的状态类2
class ConcreteState2 implements State {
    @Override
    public void doAction(Context context) {
        System.out.println("当前状态是状态2");
        // 根据状态2的逻辑处理相应的行为
        context.setState(new ConcreteState1()); // 在状态2的逻辑处理完成后，切换到状态1
    }
}

// 创建一个上下文类
class Context {
    private State state; // 当前状态

    public Context() {
        this.state = new ConcreteState1(); // 初始化状态为状态1
    }

    public void setState(State state) {
        this.state = state;
    }

    public void doAction() {
        state.doAction(this);
    }
}

// 测试
public class Main {
    public static void main(String[] args) {
        Context context = new Context();
        context.doAction(); // 执行状态1的行为，并切换到状态2
        context.doAction(); // 执行状态2的行为，并切换到状态1
    }
}
```
##### 状态模式与策略模式的异同
        相似点：状态模式和策略模式都是通过将不同的行为封装到不同的类中，然后通过组合的方式将行为委托给其他对象来实现不同的行为。
        不同点：
        1. 状态模式和策略模式的目的不同。状态模式的目的是允许对象在内部状态发生改变时改变它的行为，而策略模式的目的是允许对象在运行时选择算法。
        2.  状态类的状态切换是由上下文类来控制的，而策略类的算法切换是由客户端来控制的。（最主要）
#### 适配器模式  
        适配器模式是一种设计模式，它用于使不兼容的接口能够一起工作。正常项目开发中，我们应该减少使用适配器模式，因为它会导致系统变得更加复杂。但是在某些情况下，比如接手老项目等，它可以帮助我们解决兼容性问题。
##### 例子：
        假设你有一台笔记本电脑，但它只有一个USB接口，而你需要连接一个键盘和一个鼠标，它们都是使用PS/2接口的。这时候，你可以使用一个USB到PS/2适配器来解决兼容性问题。适配器连接到USB接口上，然后你可以将鼠标和键盘连接到适配器的PS/2接口上。
```java
// 目标接口
interface USB {
    void connectUSB();
}

// 需要适配的类
class PS2 {
    void connectPS2() {
        System.out.println("连接PS/2设备");
    }
}

// 适配器类
class PS2ToUSBAdapter implements USB {
    private PS2 ps2;

    public PS2ToUSBAdapter(PS2 ps2) {
        this.ps2 = ps2;
    }

    public void connectUSB() {
        ps2.connectPS2();
    }
}

// 客户端代码
public class Main {
    public static void main(String[] args) {
        PS2 ps2Device = new PS2();

        USB usbDevice = new PS2ToUSBAdapter(ps2Device);
        usbDevice.connectUSB(); // 输出: 连接PS/2设备
    }
}
```
#### 备忘录模式  
        备忘录模式是一种行为型设计模式，它用于在不破坏封装性的前提下捕获一个对象的内部状态，并且能够在稍后的时间点将该对象恢复到此状态。它通常用于需要保存和恢复对象状态的场景，例如撤销操作、历史记录等。
        在备忘录模式中，有三个主要角色： 
        1. 源发器（Originator）：它是需要被保存和恢复状态的对象。它知道如何创建和恢复备忘录对象，并且能够将自身的状态保存到备忘录对象中。 
        2. 备忘录（Memento）：它是用于存储源发器对象内部状态的对象。它可以包含源发器对象的部分或全部状态信息。 
        3. 管理者（Caretaker）：它负责保存备忘录对象，并且可以决定何时以及如何恢复源发器的状态。它不知道备忘录对象的具体内容，只负责存储和管理备忘录。
##### 例子
```java
// 源发器类
class Originator {
    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void restoreFromMemento(Memento memento) {
        state = memento.getState();
    }
}

// 备忘录类
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// 管理者类
class Caretaker {
    private Memento memento;

    public void saveMemento(Memento memento) {
        this.memento = memento;
    }

    public Memento retrieveMemento() {
        return memento;
    }
}

// 示例代码
public class Main {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State 1");
        System.out.println("Current state: " + originator.getState());

        caretaker.saveMemento(originator.createMemento());

        originator.setState("State 2");
        System.out.println("Current state: " + originator.getState());

        originator.restoreFromMemento(caretaker.retrieveMemento());
        System.out.println("Restored state: " + originator.getState());
    }
}
```
#### 组合模式
        组合模式是一种结构型设计模式，它允许将对象组合成树状的层次结构，以表示“部分-整体”的关系。这使得客户端可以将单个对象和组合对象一视同仁地处理，无需区分它们之间的差异。
        在组合模式中，有三个主要角色： 
        1. 组件（Component）：它是组合模式的基本对象。它可以是叶子节点（没有子节点）或者是容器节点（有子节点），定义了统一的接口供客户端使用。 
        2. 叶子（Leaf）：它是组合模式中的叶子节点，它没有子节点。 
        3. 容器（Composite）：它是组合模式中的容器节点，可以包含其他组件对象作为子节点。它提供了管理子节点的方法，并且可以将操作委托给子节点。
##### 例子
```java
// 组件接口
interface Component {
    void operation();
}

// 叶子节点类
class Leaf implements Component {
    private String name;

    public Leaf(String name) {
        this.name = name;
    }

    @Override
    public void operation() {
        System.out.println("Leaf " + name + " operation");
    }
}

// 容器节点类
class Composite implements Component {
    private List<Component> components = new ArrayList<>();

    @Override
    public void operation() {
        System.out.println("Composite operation");

        for (Component component : components) {
            component.operation();
        }
    }

    public void addComponent(Component component) {
        components.add(component);
    }

    public void removeComponent(Component component) {
        components.remove(component);
    }
}

// 示例代码
public class Main {
    public static void main(String[] args) {
        Component leaf1 = new Leaf("Leaf 1");
        Component leaf2 = new Leaf("Leaf 2");
        Component leaf3 = new Leaf("Leaf 3");

        Component composite = new Composite();
        composite.addComponent(leaf1);
        composite.addComponent(leaf2);

        Component root = new Composite();
        root.addComponent(composite);
        root.addComponent(leaf3);

        root.operation();
    }
}
```
#### 迭代器模式
        迭代器模式是一种行为型设计模式，用于提供一种统一的方式来遍历集合对象中的元素，而无需暴露集合的内部表示。它将集合和遍历分离，使得可以独立地修改集合和遍历算法。
        在迭代器模式中，有两个主要角色： 
        1. 迭代器接口（Iterator）：它定义了遍历集合对象的方法，包括获取下一个元素、判断是否还有元素等。 
        2. 集合接口（Aggregate）：它定义了创建迭代器对象的方法，通常包含返回迭代器对象的方法。
##### 例子
```java
// 迭代器接口
interface Iterator {
    boolean hasNext();
    Object next();
}

// 集合接口
interface Aggregate {
    Iterator createIterator();
}

// 具体迭代器类
class ConcreteIterator implements Iterator {
    private String[] elements;
    private int position = 0;

    public ConcreteIterator(String[] elements) {
        this.elements = elements;
    }

    @Override
    public boolean hasNext() {
        return position < elements.length;
    }

    @Override
    public Object next() {
        return elements[position++];
    }
}

// 具体集合类
class ConcreteAggregate implements Aggregate {
    private String[] elements;

    public ConcreteAggregate(String[] elements) {
        this.elements = elements;
    }

    @Override
    public Iterator createIterator() {
        return new ConcreteIterator(elements);
    }
}

// 示例代码
public class Main {
    public static void main(String[] args) {
        String[] elements = {"Element 1", "Element 2", "Element 3"};

        Aggregate aggregate = new ConcreteAggregate(elements);
        Iterator iterator = aggregate.createIterator();

        while (iterator.hasNext()) {
            Object element = iterator.next();
            System.out.println(element);
        }
    }
}
```
#### 单例模式
        单例模式是一种创建型设计模式，它能够保证一个类只有一个实例，并提供一个访问该实例的全局节点。
        在单例模式中，有两个主要角色： 
        1. 单例类（Singleton）：它包含了一个实例且能自行创建这个实例。 
        2. 客户端（Client）：它需要通过单例类的全局节点来获取单例类的实例。
##### 懒汉模式与饿汉模式
        懒汉模式是指单例实例在第一次被使用时才进行初始化的模式，而饿汉模式是指单例实例在类被加载时就进行初始化的模式。
        懒汉模式的优点是单例只有在使用时才会被实例化，可以节省资源，缺点是第一次加载时需要及时进行实例化，反应稍慢一些，且在多线程环境下需要使用同步锁 synchronized 进行同步，可能会造成资源的浪费。
        饿汉模式的优点是单例在类被加载时就被实例化，避免了线程同步问题，缺点是单例在还没有使用到的时候就被实例化，可能会造成资源的浪费。
##### 例子
```java
// 懒汉模式
public class LazySingleton {
    private static LazySingleton instance;

    private LazySingleton() {}

    public static LazySingleton getInstance() {
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
// 饿汉模式
public class EagerSingleton {
    private static EagerSingleton instance = new EagerSingleton();

    private EagerSingleton() {}

    public static EagerSingleton getInstance() {
        return instance;
    }
}
```
#### 桥接模式
        桥接模式是一种结构型设计模式，它可以将抽象部分与实现部分分离，使它们都可以独立地变化。通俗地说，桥接模式就是将事物与其具体实现分开，使它们可以各自独立地变化。
        在桥接模式中，有四个主要角色： 
        1. 抽象类（Abstraction）：它定义了抽象部分的接口。它一般是抽象类而不是接口，因为接口不能包含实现代码。 
        2. 扩充抽象类（Refined Abstraction）：它是抽象类的子类，可以扩充抽象类中定义的方法。 
        3. 实现类接口（Implementor）：它定义了实现类的接口，这个接口不一定要与抽象类的接口完全一致，事实上这两个接口可以完全不同。一般来说，Implementor接口仅提供基本操作，而Abstraction定义的接口可能会做更多更复杂的操作。 
        4. 具体实现类（Concrete Implementor）：它是实现类接口的具体实现，含有实现类的具体操作。
##### 例子
```java
// 定义抽象类 Shape
public abstract class Shape {
    protected DrawAPI drawAPI;

    protected Shape(DrawAPI drawAPI) {
        this.drawAPI = drawAPI;
    }

    public abstract void draw();
}

// 定义实现接口 DrawAPI
public interface DrawAPI {
    void drawCircle(int radius, int x, int y);
}

// 创建具体实现类 RedCircle
public class RedCircle implements DrawAPI {
    @Override
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Drawing red circle with radius " + radius + " at (" + x + ", " + y + ")");
    }
}

// 创建具体实现类 GreenCircle
public class GreenCircle implements DrawAPI {
    @Override
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Drawing green circle with radius " + radius + " at (" + x + ", " + y + ")");
    }
}

// 创建实现抽象类 Shape 的子类 Circle
public class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawAPI drawAPI) {
        super(drawAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    @Override
    public void draw() {
        drawAPI.drawCircle(radius, x, y);
    }
}

// 在客户端代码中使用桥接模式
public class BridgePatternExample {
    public static void main(String[] args) {
        Shape redCircle = new Circle(100, 100, 10, new RedCircle());
        Shape greenCircle = new Circle(200, 200, 20, new GreenCircle());

        redCircle.draw();
        greenCircle.draw();
    }
}
```
#### 命令模式
        命令模式是一种行为型设计模式，它可以将请求转换为一个包含与请求相关的所有信息的独立对象。这种转换让你能根据不同的请求将方法参数化、延迟请求执行或将其放入队列中，且能实现可撤销操作。
        在命令模式中，有四个主要角色： 
        1. 命令（Command）：它声明了执行操作的接口。 
        2. 具体命令（Concrete Command）：它是命令接口的实现类，它对应具体的接收者对象，将接收者对象的动作绑定其中。 
        3. 调用者（Invoker）：它接收客户端的命令并执行命令。 
        4. 接收者（Receiver）：它执行命令具体的操作，是具体命令对象业务的真正实现者。
##### 例子
```java
// 以电视遥控器为例
// 命令接口
interface Command {
    void execute();
}
// 具体命令类
class TurnOnCommand implements Command {
    private TV tv;

    public TurnOnCommand(TV tv) {
        this.tv = tv;
    }

    @Override
    public void execute() {
        tv.turnOn();
    }
}
class TurnOffCommand implements Command {
    private TV tv;

    public TurnOffCommand(TV tv) {
        this.tv = tv;
    }

    @Override
    public void execute() {
        tv.turnOff();
    }
}
// 接收者类
class TV {
    public void turnOn() {
        System.out.println("Turning on the TV");
    }
}
// 调用者类
class RemoteController {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        TV tv = new TV();
        Command command1 = new TurnOnCommand(tv), command2 = new TurnOffCommand(tv);

        RemoteController remoteController = new RemoteController();
        remoteController.setCommand(command1);
        remoteController.pressButton();
        remoteController.setCommand(command2);
        remoteController.pressButton();
    }
}
```
#### 责任链模式
        责任链模式是一种行为型设计模式，它允许你将请求沿着处理者链进行发送，直至其中一个处理者对其进行处理。该模式允许多个对象来处理同一请求，而无需让客户端类了解到底使用哪一个对象来处理它。
        在责任链模式中，有两个主要角色： 
        1. 处理者（Handler）：它声明了一个处理请求的接口，同时实现了后继链（successor link）。 
        2. 具体处理者（Concrete Handler）：它是处理请求的具体处理者，它会对请求进行处理，如果不能处理则会将请求转发给后继者。
##### 例子
```java
// 这里以一个请假审批的例子来说明责任链模式
// 处理者接口
interface Handler {
    void handleRequest(int leaveDays);
}
// 具体处理者类
class Director implements Handler {
    private Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    @Override
    public void handleRequest(int leaveDays) {
        if (leaveDays <= 3) {
            System.out.println("Director approved");
        } else {
            successor.handleRequest(leaveDays);
        }
    }
}
class Manager implements Handler {
    private Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    @Override
    public void handleRequest(int leaveDays) {
        if (leaveDays <= 10) {
            System.out.println("Manager approved");
        } else {
            successor.handleRequest(leaveDays);
        }
    }
}
class CEO implements Handler {
    @Override
    public void handleRequest(int leaveDays) {
        System.out.println("CEO approved");
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        Handler director = new Director();
        Handler manager = new Manager();
        Handler ceo = new CEO();

        director.setSuccessor(manager);
        manager.setSuccessor(ceo);

        director.handleRequest(2);
        director.handleRequest(5);
        director.handleRequest(15);
    }
}
```
#### 中介者模式
        中介者模式是一种行为型设计模式，它可以让你减少对象之间混乱无序的依赖关系。该模式会限制对象之间的直接交互，迫使它们通过一个中介者对象进行合作。
        在中介者模式中，有四个主要角色： 
        1. 中介者（Mediator）：它定义了一个接口，该接口用于与各同事对象之间进行通信。 
        2. 具体中介者（Concrete Mediator）：它是实现了中介者接口的具体中介者类，它通过协调各个同事对象来实现协作行为，因此它必须依赖于各个同事对象。 
        3. 同事类（Colleague）：它定义了各个同事类公有的方法，并声明了一些抽象方法来供子类实现，同时它维持了一个对抽象中介者类的引用，其子类可以通过该引用来与中介者进行通信。 
        4. 具体同事类（Concrete Colleague）：它是各个具体同事类的子类，每个同事只知道自己的行为，而不了解其他同事类的情况，但它们都认识中介者对象。
##### 例子
```java
// 这里以 QQ 群聊为例
// 中介者接口
interface Mediator {
    void sendMessage(String message, User user);
}
// 具体中介者类
class QQGroup implements Mediator {
    private List<User> users = new ArrayList<>();

    @Override
    public void sendMessage(String message, User user) {
        for (User u : users) {
            if (u != user) {
                u.receiveMessage(message);
            }
        }
    }

    public void addUser(User user) {
        users.add(user);
    }
}
// 同事类
abstract class User {
    protected Mediator mediator;

    public User(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void sendMessage(String message);
    public abstract void receiveMessage(String message);
}
// 具体同事类
class NormalUser extends User {
    public NormalUser(Mediator mediator) {
        super(mediator);
    }

    @Override
    public void sendMessage(String message) {
        System.out.println("Normal user sends message: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println("Normal user receives message: " + message);
    }
}
class VIPUser extends User {
    public VIPUser(Mediator mediator) {
        super(mediator);
    }

    @Override
    public void sendMessage(String message) {
        System.out.println("VIP user sends message: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println("VIP user receives message: " + message);
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        Mediator mediator = new QQGroup();

        User user1 = new NormalUser(mediator);
        User user2 = new NormalUser(mediator);
        User user3 = new VIPUser(mediator);

        mediator.addUser(user1);
        mediator.addUser(user2);
        mediator.addUser(user3);

        user1.sendMessage("Hello");
        user3.sendMessage("Hello");
    }
}
```
#### 享元模式
        享元模式是一种结构型设计模式，它通过共享大量细粒度对象来有效地支持大量细粒度的对象。
        在享元模式中，有两个主要角色： 
        1. 享元（Flyweight）：它是一个包含状态独立的不可变（又称固有的）数据的共享对象。 
        2. 工厂（Factory）：它用于构造一个享元对象，它会确保合理地共享享元对象。当用户请求一个享元时，工厂对象会提供一个已创建的实例或者创建一个新的实例。
##### 例子
```java
// 以围棋为例
// 享元类
class GoPiece {
    private String color;

    public GoPiece(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }
}
// 工厂类
class GoPieceFactory {
    private static Map<String, GoPiece> pieces = new HashMap<>();

    public static GoPiece getPiece(String color) {
        GoPiece piece = pieces.get(color);

        if (piece == null) {
            piece = new GoPiece(color);
            pieces.put(color, piece);
        }

        return piece;
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        GoPiece black1 = GoPieceFactory.getPiece("black");
        GoPiece black2 = GoPieceFactory.getPiece("black");
        GoPiece white1 = GoPieceFactory.getPiece("white");
        GoPiece white2 = GoPieceFactory.getPiece("white");

        System.out.println(black1 == black2); // true
        System.out.println(white1 == white2); // true
    }
}
```
#### 解释器模式
        解释器模式是一种行为型设计模式，它允许你定义语言的语法，并解释语言中的句子。它通常用于需要频繁处理一些结构化文本的场景。
        在解释器模式中，有四个主要角色： 
        1. 抽象表达式（Abstract Expression）：它一般是一个抽象类或接口，声明了解释器的抽象方法 interpret()，它是所有终结符表达式和非终结符表达式的公共父类。 
        2. 终结符表达式（Terminal Expression）：它实现了与文法中的终结符相关联的解释操作，在句子中的每一个终结符都是该类的一个实例。通常在一个解释器模式中只有少数几个终结符表达式类，它们的实例可以通过非终结符表达式组成较为复杂的句子。 
        3. 非终结符表达式（Nonterminal Expression）：它实现了文法中非终结符的解释操作，由于在非终结符表达式中可以包含终结符表达式，也可以继续包含非终结符表达式，因此其解释操作一般通过递归的方式来完成。 
        4. 环境（Context）：它定义了各个解释器之间的关系，它一般是一个类，可以使用 HashMap 来存储解释器之间的关系，每个终结符表达式都在环境类中存储了一个对应它的非终结符表达式的引用。
##### 例子
```java
// 以四则运算为例
// 抽象表达式类
interface Expression {
    int interpret();
}
// 终结符表达式类
class NumberExpression implements Expression {
    private int number;

    public NumberExpression(int number) {
        this.number = number;
    }

    @Override
    public int interpret() {
        return number;
    }
}
// 非终结符表达式类
class AddExpression implements Expression {
    private Expression leftExpression, rightExpression;

    public AddExpression(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() + rightExpression.interpret();
    }
}
class SubtractExpression implements Expression {
    private Expression leftExpression, rightExpression;

    public SubtractExpression(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() - rightExpression.interpret();
    }
}
class MultiplyExpression implements Expression {
    private Expression leftExpression, rightExpression;

    public MultiplyExpression(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() * rightExpression.interpret();
    }
}
class DivideExpression implements Expression {
    private Expression leftExpression, rightExpression;

    public DivideExpression(Expression leftExpression, Expression rightExpression) {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() / rightExpression.interpret();
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        Expression expression = new AddExpression(
                new SubtractExpression(
                        new MultiplyExpression(
                                new NumberExpression(10),
                                new NumberExpression(2)
                        ),
                        new NumberExpression(5)
                ),
                new DivideExpression(
                        new NumberExpression(20),
                        new NumberExpression(4)
                )
        );

        System.out.println(expression.interpret()); // 输出: 5
    }
}
```
#### 访问者模式
        访问者模式是一种行为型设计模式，它能将算法与其所作用的对象隔离开来。
        在访问者模式中，有四个主要角色： 
        1. 抽象访问者（Visitor）：它声明了一组访问方法，用于声明访问者可以访问哪些元素。 
        2. 具体访问者（Concrete Visitor）：它实现了抽象访问者所声明的访问方法，它影响了访问者访问到一个类后该类的执行方式。 
        3. 抽象元素（Element）：它定义了一个接受访问者（accept()）的方法，其意义是指每一个元素都要可以被访问者访问。 
        4. 具体元素（Concrete Element）：它实现了抽象元素所定义的接受访问方法（accept()），通常它会调用访问者提供的访问该元素的方法。 
        5. 对象结构（Object Structure）：它是一个元素的集合，提供了遍历它的方法。它可以结合组合模式来实现，也可以是一个简单的集合对象，如一个List对象或一个Set对象。
##### 例子
```java
// 以购物车为例
// 抽象访问者类
interface Visitor {
    void visit(Book book);
    void visit(Fruit fruit);
}
// 具体访问者类
class ShoppingCartVisitor implements Visitor {
    @Override
    public void visit(Book book) {
        System.out.println("Book: " + book.getName() + ", price: " + book.getPrice());
    }

    @Override
    public void visit(Fruit fruit) {
        System.out.println("Fruit: " + fruit.getName() + ", price: " + fruit.getPrice());
    }
}
// 抽象元素类
interface ItemElement {
    void accept(Visitor visitor);
}
// 具体元素类
class Book implements ItemElement {
    private String name;
    private int price;

    public Book(String name, int price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
class Fruit implements ItemElement {
    private String name;
    private int price;
    private int weight;

    public Fruit(String name, int price, int weight) {
        this.name = name;
        this.price = price;
        this.weight = weight;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }

    public int getWeight() {
        return weight;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
// 客户端代码
public class Main {
    public static void main(String[] args) {
        ItemElement[] items = new ItemElement[]{
                new Book("Book 1", 10),
                new Book("Book 2", 20),
                new Fruit("Apple", 5, 2),
                new Fruit("Banana", 10, 1)
        };

        int total = 0;
        Visitor visitor = new ShoppingCartVisitor();

        for (ItemElement item : items) {
            item.accept(visitor);
            total += item.getPrice();
        }

        System.out.println("Total: " + total);
    }
}
```