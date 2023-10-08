# 设计模式
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
#### 接口和抽象类  
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
#### 泛型  
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
#### 委托和事件  
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
        类（Class）：用矩形框表示，框内写上类的名称。分为三部分，上面类名，中间特性（字段或属性），最后操作（方法或行为）。
        属性（Attributes）：表示类的特征或状态，用名称和类型表示。属性通常写在类的顶部。例如，一个名为"age"的属性可以表示为：-age:int （"-"表示私有属性，"int"表示属性的类型）。
        方法（Methods）：表示类的行为或操作，用名称和参数列表表示。方法通常写在类的底部。例如，一个名为"getName"的方法可以表示为：+getName():String （"+"表示公有方法，"String"表示方法的返回类型）。
        关联关系（Association）：表示类之间的关联，通常使用实线箭头来表示。箭头指向关联的目标类。例如，如果类A和类B之间存在关联关系，可以用以下形式来表示：[A]-->[B]。
        继承关系（Inheritance）：表示类之间的继承关系，通常使用空心箭头来表示。箭头指向父类。例如，如果类B继承自类A，可以用以下形式来表示：[A]<|--[B]。
        实现关系（Interface）：表示类实现接口的关系，通常使用空心三角形箭头来表示。箭头指向接口。例如，如果类A实现了接口B，可以用以下形式来表示：[A]..▷[B]。
        聚合关系（Aggregation）：表示整体与部分之间的关系，通常使用空心菱形箭头来表示。箭头指向整体。例如，如果类A包含一个类B的对象，可以用以下形式来表示：[B]◇-->[A]。
        组合关系（Composition）：表示整体与部分之间的强关系，通常使用实心菱形箭头来表示。箭头指向整体。例如，如果类A包含一个类B的对象，并且类B的生命周期依赖于类A，可以用以下形式来表示：[B]◆-->[A]。
### 基本原则
#### 单一职责原则  
    单一职责（Single Responsibility Principle）是面向对象设计原则之一，它要求一个类应该只有一个引起它变化的原因，即一个类应该只有一个职责。
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
#### 开发-封闭原则  
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
#### 依赖倒转原则  
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
#### 迪米特原则  
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
    在上述例子中，购物车（ShoppingCart）只与商品（Product）和用户（User）类直接交互，并不知道具体商品或用户的内部实现细节。这样，购物车只需要和自己的朋友打交道，降低了系统的耦合度。
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
      
// 状态接口
interface State {
    void doAction();
}

// 具体状态类
class AngryState implements State {
    public void doAction() {
        System.out.println("攻击其他角色");
    }
}

class HappyState implements State {
    public void doAction() {
        System.out.println("跳舞");
    }
}

class SadState implements State {
    public void doAction() {
        System.out.println("哭泣");
    }
}

// 上下文类
class Character {
    private State currentState;

    public Character() {
        currentState = new HappyState();
    }

    public void setState(State state) {
        currentState = state;
    }

    public void performAction() {
        currentState.doAction();
    }
}

// 客户端代码
public class Main {
    public static void main(String[] args) {
        Character character = new Character();

        character.performAction(); // 输出: 跳舞

        character.setState(new AngryState());
        character.performAction(); // 输出: 攻击其他角色

        character.setState(new SadState());
        character.performAction(); // 输出: 哭泣
    }
}
```
#### 适配器模式  
        适配器模式是一种设计模式，它用于使不兼容的接口能够一起工作。通俗地说，适配器就像一个转接头，可以连接不同类型的设备。
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