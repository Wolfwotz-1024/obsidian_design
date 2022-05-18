## 1、为什么引入泛型
> 泛型的本质是为了参数化类型（在不创建新的类型的情况下，通过范型指定的不同类型来控制形参具体限制的类型）。也就是说在泛型使用的过程中，操作的数据类型被指定为一个参数，这种参数可以用在类、接口和方法中，分别被称为泛型类、泛型接口、泛型方法。

引入泛型的意义在于：
+ **适用于多种数据类型执行相同的代码**（代码复用）

我们通过一个例子来阐述，先看下下面的代码：
```java
private static int add(int a, int b) {
    System.out.println(a + "+" + b + "=" + (a + b));
    return a + b;
}

private static float add(float a, float b) {
    System.out.println(a + "+" + b + "=" + (a + b));
    return a + b;
}

private static double add(double a, double b) {
    System.out.println(a + "+" + b + "=" + (a + b));
    return a + b;
}
```

如果没有泛型，要实现不同类型的加法，每种类型都需要重载一个add方法；通过泛型，我们可以复用为一个方法：

```java
private static <T extends Number> double add(T a, T b) {
    System.out.println(a + "+" + b + "=" + (a.doubleValue() + b.doubleValue()));
    return a.doubleValue() + b.doubleValue();
}
```
 
 + 泛型中的类型在使用时制定，不需要强制类型转（**类型安全**，编译器会**检查类型**）

看下这个例子：
```java
List list = new ArrayList();
list.add("xxString");
list.add(100d);
list.add(new Person());
```

我们在使用上述list中，list中的元素都是Object类型（无法约束其中的类型），所以在取出集合元素时需要人为的强制类型转化到具体的目标类型，且很容易出现`java.lang.ClassCastException`异常。

引入泛型，它将提供类型的约束，提供编译前的检查：
```java
List<String> list = new ArrayList<String>();

// list中只能放String, 不能放其它类型的元素
```

