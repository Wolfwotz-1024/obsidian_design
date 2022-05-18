## 1、抽象类与接口
### 1）、抽象类
抽象类和抽象方法都使用`abstract`	关键字进行声明。抽象类一般会包括抽象方法，抽象方法一定位于抽象类中。

抽象类和普通类最大的区别是，抽象类不能被实例化，需要继承抽象类才能实例化其子类。
```java
public abstract class AbstractClassExample{
	protected int x;
	private int y;
	
	public abstract void func1();
	
	public void func2(){
		System.out.println("func2");
	}
}
```

```java
public class AbstractExtendClassExample extends AbstractClassExample{
	@Override
	public void func1(){
		System.out.println("func1");
	}
}
```

```java
// AbstractClassExample ac1 = new AbstractClassExample();
AbstractClassExample ac2 = new AbstractExtendClassExample();
ac2.func1();
```


### 2）、接口
接口是抽象类的延伸，在 Java 8 之前，它可以看成是一个完全抽象的累，也就是说他不能有任何的方法实现。

从 Java 8 开始，接口也可以拥有默认的方法实现，这是因为不支持默认方法的接口的维护成本太高了。在 Java 8 之前，如果一个接口想要添加新的方法，那么要修改所有实现了该接口的类。

接口的成员（字段 + 方法）默认都是 public 的，并且不允许定义为 private 或者 protected。

接口的字段默认都是 static 和 final 的。

```java
public interface InterfaceExample{
	void func1();
	
	default void func2(){
		System.out.println("func2");
	}
	
	int x = 123;
	
	public int z = 0;
}
```

```java
public class InterfaceImplementExample implements InterfaceExample{
	@Override
	public void func1(){
		System.out.println("func1");
	}
}
```

```java
// InterfaceExample ie1 = new InterfaceExample(); // 'InterfaceExample' is abstract; cannot be instantiated
InterfaceExample ie2 = new InterfaceImplementExample();
ie2.func1();
System.out.println(InterfaceExample.x);
```


### 3）、比较

-   从设计层面上看，抽象类提供了一种 IS-A 关系，那么就必须满足里式替换原则，即子类对象必须能够替换掉所有父类对象。而接口更像是一种 LIKE-A 关系，它只是提供一种方法实现契约，并不要求接口和实现接口的类具有 IS-A 关系。
-   从使用上来看，一个类可以实现多个接口，但是不能继承多个抽象类。
-   接口的字段只能是 static 和 final 类型的，而抽象类的字段没有这种限制。
-   接口的成员只能是 public 的，而抽象类的成员可以有多种访问权限。

### 4）、使用选择

使用接口:

-   需要让不相关的类都实现一个方法，例如不相关的类都可以实现 Compareable 接口中的 compareTo() 方法；
-   需要使用多重继承。

使用抽象类:

-   需要在几个相关的类中共享代码。
-   需要能控制继承来的成员的访问权限，而不是都为 public。
-   需要继承非静态和非常量字段。

在很多情况下，接口优先于抽象类，因为接口没有抽象类严格的类层次结构要求，可以灵活地为一个类添加行为。并且从 Java 8 开始，接口也可以有默认的方法实现，使得修改接口的成本也变的很低。


## 2、Java中，Serializable 与 Externalizable 的区别？
Serializable 接口是一个序列化 Java 类的接口，以便于它们可以在网格上传输或者可以将它们的状态保存在磁盘上，是 JVM 内嵌的默认序列化方式，成本高、脆弱而且不安全。Externalizable 允许你控制整个序列化过程，指定特定的二进制格式，增加安全机制。

## 3、说出 JDK 1.7 中的三个新特性？
虽然 JDK 1.7 不像 JDK 5 和 8 一样的大版本，但是，还是有很多新的特性，如 try-with-resource 语句，这样你在使用流或者资源的时候，就不需要手动关闭，Java 会自动关闭。Fork-Join 池某种程度上实现 Java 版的 Map-reduce。允许 Switch 中有 String 变量和文本。菱形操作符(<>)用于泛型推断，不再需要在变量声明的右边申明泛型，因此可以写出可读写更强、更简洁的代码。另一个值得一提的特性是改善异常处理，如允许在同一个 catch 块中捕获多个异常。

## 4、说出 5 个 JDK 1.8 引入的新特性？
Java 8 在 Java 历史上是一个开创新的版本，下面 JDK 8 中 5 个主要的特性: Lambda 表达式，允许像对象一样传递匿名函数 Stream API，充分利用现代多核 CPU，可以写出很简洁的代码 Date 与 Time API，最终，有一个稳定、简单的日期和时间库可供你使用 扩展方法，现在，接口中可以有静态、默认方法。 重复注解，现在你可以将相同的注解在同一类型上使用多次。

下述包含 Java 面试过程中关于 SOLID 的设计原则，OOP 基础，如类，对象，接口，继承，多态，封装，抽象以及更高级的一些概念，如组合、聚合及关联。也包含了 GOF 设计模式的问题。

## 5、异常
相关的关键字 throw、throws、try...catch、finally
+ throws 用在方法签名上，以便抛出的异常可以被调用者处理
+ throw 方法内部通过 throw 抛出异常
+ try 用于检测包住的语句块，若有异常，catch 子句捕获并执行 catch 块

## 6、关于finally
+ finally不管有没有异常都要处理
+ 当try和catch中有return时，finally仍然会执行，finally比retrun先执行
+ 不管有没有异常抛出，finally在return返回前执行
+ finally 是在return 后面的表达式运算后执行的（此时并没有返回运算后的值，而是先把要返回的值保存起来，管finally中的代码怎么样，返回的值都不会改变，仍然是之前保存的值），所以函数返回值是在finally执行前确定的。

注意：<font color= red>finally 中最好不要包含 return， 否则程序会提前退出，返回值不是try 或 catch中保存的返回值</font>。

finally 不执行的几种情况：程序提前终止如调用了System.exit, 病毒，断电

## 7、this() & super()在构造方法中的区别
+ 调用super()必须写在子类构造方法的第一行，否则编译不通过
+ super从子类调用父类构造，this在同一类中调用其他构造均需要放在第一行
+ 尽管可以用this调用一个构造器，却不能调用2个
+ this和super不能出现在同一个构造器中，否则编译不通过
+ this()、super() 都指的对象，不可以在 static 环境中使用
+ 本质 this 指向本对象的指针。super是一个关键字。

## 8、序列化
声明为 static 和 transient 类型的数据不能被序列化，反序列化需要一个无参构造函数。

## 9、Java移位运算符
java中有三种移位运算符
+ `<<`: 左移运算符，`x << 1`，相当于 x 乘以2（不溢出的情况下），低位补0
+ `>>`: 带符号右移，`x >> 1`，相当于 x 除以2，正数高位补0，负数高位补1
+ `>>>`:无符号右移，忽略符号位，空位都以0补齐

## 10、局部变量为什么要初始化
局部变量是指类方法中的变量，必须初始化。局部变量运行时被分配在栈中，量大，生命周期短，如果虚拟机给每个局部变量都初始化一下，是一笔很大的开销，但变量不初始化为默认值就使用是不安全的。出于速度和安全性两方面的考虑，解决方案就是虚拟机不初始化，但要求编写者一定要在使用前给变量赋值。
