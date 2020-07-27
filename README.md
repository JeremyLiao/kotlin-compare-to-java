# Kotlin Compare to Java
> 对比着java学习kotlin，事半功倍

[toc]

## 变量定义
- kotlin

```
    var a: Int = 1          //指定了类型并赋初值
    var b = 1               //不指定类型
    var c: Int              //不初始化，报错
    var d: String = null    //赋值为null，报错
    var e: String? = null   //赋值为null，可为空，正确
```

```
    print(e.length)     //直接访问，报错
    print(e?.length)    //正确
    print(e!!.length)   //正确
```

- java

```
    int a = 1;          //整形基本类型
    Integer b = 1;      //整形包装类型
    int c;              //不初始化，自动初始化为0
    Integer d = null;   //赋值为null
```

> kotlin用var定义变量，可以指定类型，也可以不指定类型，但是不同于java，kotlin用var定义的变量需要指定初始值，java可以不指定初始值。

> 变量类型如Int是不能设为null的，如果一个变量有可能设置为null，类型需要设置成“类型+?”，如“String?”。访问有可能为空的变量的成员，直接写.编译器会报错，需要写成?.或者!!.，这个后面再说。

---

## 只读变量
- kotlin

```
    val a:Int = 1           //指定了类型并赋值
    val b = 1               //不指定类型
    val c                   //不赋值，报错
    val d:Int = null        //赋值为null，报错
    val e:Int? = null       //赋值为null，可为空，正确
```

```
    print(a)            //访问，正确
    a = 2               //修改，报错
```

- java

```
    final int a = 1;
```
> kotlin中的val可以理解成java中的final变量
> 也可以理解成java中只有getter没有setter的类成员变量

---

## 变量null检查
- kotlin

```
    val a: String? = "hello world"
```

```
    print(a.length)            //报错，不能直接访问
    print(a?.length)           //正确，若为空不做处理返回null
    print(a!!.length)          //正确，若为空抛出空指针异常
```

- java

```
    String a = "hello world";
```

```
    if (a != null) {
        int length = a.length();
    }
```
or

```
    int length = a != null ? a.length() : 0;
```

> 可控变量必须使用null检查访问成员变量或方法，直接访问会报错，?.若为空不做处理返回null，!!.若为空抛出空指针异常

---

## const常量
- kotlin

```
const val THOUSAND = 1000

object myObject {
    const val constNameObject: String = "constNameObject"
}


class MyClass {

    companion object Factory {
        const val constNameCompanionObject: String = "constNameCompanionObject"
    }
}
```

- java

```
class MyClass {
    public static final int THOUSAND = 1000;

    public static final String CONST_NAME = "const_name";
}
```
> const 必须修饰val

> const 只允许在top-level级别和object中声明

---

## 类型检测及自动类型转换
- kotlin

```
    var obj: Any = "hello world"
    
    if (obj is String) {
        val length = obj.length     // 做过类型判断以后，obj会被系统自动转换为String类型
    }
```

- java

```
    Object obj = "hello world";
    
    if (obj instanceof String) {
        int length = ((String) obj).length();
    }
```
> kotlin中用is判断是不是某种类型，也可以用!is判断不是某种类型

---

## 字符串拼接
- kotlin

```
    val a: String = "a"
    val b: String = "b"
    val c: String = "$a and $b"
```

- java

```
    String a = "a";
    String b = "b";
    String c = a + " and " + b;
```

---

## 三元表达式
- kotlin

```
    val input: Int = 10
    val ret: Int = if (input > 0) input else 0
```

- java

```
    int input = 10;
    int ret = input > 0 ? input : 0;
```

---

## switch/case条件匹配
- kotlin

```
    val score: Int = 10
    val result = when (score) {
        100 -> "full score"
        in 90..99 -> "excellent"
        in 80..89 -> "good"
        in 60..79 -> "not bad"
        else -> "fail"
    }
```

- java

```
    int score = 10;
    String result;
    switch (score) {
        case 100:
            result = "full score";
            break;
        case 99:
        case 98:
        case 90:
            result = "excellent";
            break;
        case 89:
        case 88:
        case 80:
            result = "good";
            break;
        case 79:
        case 78:
        case 60:
            result = "not bad";
            break;
        default:
            result = "fail";
```
---

## for循环
- kotlin

```
    for (i in 1..10) { }
    
    for (i in 1 until 10) { }
    
    for (i in 10 downTo 0) { }
    
    for (i in 1..10 step 2) { }
    
    for (i in 10 downTo 0 step 2) { }
    
    for (item in collection) { }
    
    for ((key, value) in map) { }
```

- java

```
    for (int i = 1; i <= 10 ; i++) { }
    
    for (int i = 1; i < 10 ; i++) { }
    
    for (int i = 10; i >= 0 ; i--) { }
    
    for (int i = 1; i <= 10 ; i+=2) { }
    
    for (int i = 10; i >= 0 ; i-=2) { }
    
    for (String item : collection) { }
    
    for (Map.Entry<String, String> entry: map.entrySet()) { }
```
---

## 方法
- kotlin

```
    fun doSomething() {

    }

    fun doSomething(input: Int) {

    }

    fun doSomething(vararg inputs: Int) {

    }

    fun doSomething(input: String): Int {
        return 0
    }
```

- java

```
    void doSomething() {

    }

    void doSomething(int input) {

    }

    void doSomething(int... inputs) {

    }

    int doSomething(String input) {
        return 0;
    }
```
---

## Util类（工具类）
- kotlin

```
class Utils private constructor() {

    companion object {

        fun compute(input: Int): Int {
            return 2 * input
        }
    }
}

// another way

object Utils {

    fun compute(input: Int): Int {
        return 2 * input
    }
}
```

- java

```
public class Utils {

    private Utils() {
        // This utility class is not publicly instantiable
    }

    public static int compute(int input) {
        return 2 * input;
    }
}
```
---
## 类的构造函数
- kotlin

```
class Person constructor(name: String) {
    var name: String = ""
    var age: Int = 0

    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
}
```

- java

```
class Person {
    String name;
    int age;

    public Person(String name) {
        this.name = name;
    }

    public Person(String name, int age) {
        this(name);
        this.age = age;
    }
}
```
> 在Kotlin中一个类可以有一个主构造函数和一个或多个次构造函数；如果不写构造函数会有一个默认空的构造函数

> 主构造函数是类头的一部分：它跟在类名（和可选的类型参数）后。如果主构造函数没有任何注解或可见性修饰符，constructor关键字可省略，否则是必须的
---

## 数据类（Bean）
- kotlin

```
data class Student(val name: String, val age: Int)
```

- java

```
public class Student {

    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Student developer = (Student) o;

        if (age != developer.age) return false;
        return name != null ? name.equals(developer.name) : developer.name == null;

    }

    @Override
    public int hashCode() {
        int result = name != null ? name.hashCode() : 0;
        result = 31 * result + age;
        return result;
    }

    @Override
    public String toString() {
        return "Developer{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```
> kotlin的简洁体现得淋漓尽致
---

## 类的初始化块
- kotlin

```
class Person constructor(name: String) {
    var name: String
    var age: Int

    init {
        this.name = ""
        this.age = 0
    }

    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
}
```

- java

```
class Person {
    String name;
    int age;

    {
        name = "";
        age = 0;
    }

    public Person(String name) {
        this.name = name;
    }

    public Person(String name, int age) {
        this(name);
        this.age = age;
    }
}
```
---

## 类的Getter和Setter
- kotlin

```
class Person {
    var name: String = ""
    var age: Int = 0
    val no: Long = 0
}
```

- java

```
class Person {
    private String name;
    private int age;
    final private long no = 0;

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public long getNo() {
        return no;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
> 在Kotlin中，getter和setter是可选的，如果你没有在代码中创建它们，它是会默认自动生成

> val不允许设置setter函数，因为它是只读的
---

## 抽象类
- kotlin

```
abstract class Person {
    var name: String = ""
    var age: Int = 0
    val no: Long = 0

    abstract fun absFun()
}
```

- java

```
abstract class Person {
    String name;
    int age;
    final long no = 0;

    abstract void absFun();
}
```
---

## 内部类
- kotlin

```
class Outer {
    private val bar: Int = 1
    var v = "成员属性"

    /**嵌套内部类**/
    inner class Inner {
        fun foo() {
            print(bar)
        }

        fun innerTest() {
            print(this@Outer.v)
        }
    }
}
```

- java

```
class Outer {
    private int bar = 1;
    String v = "成员属性";

    /**
     * 嵌套内部类
     **/
    class Inner {
        void foo() {
            System.out.print(bar);
        }

        void innerTest() {
            System.out.print(Outer.this.v);
        }
    }
}
```
---

## 匿名内部类
- kotlin

```
interface TestInterFace {
    fun test()
}

class Test {

    var interFace: TestInterFace = object : TestInterFace {
        override fun test() {
            print("hello world")
        }
    }
}
```

- java

```
interface TestInterFace {
    void test();
}

class Test {

    TestInterFace interFace = new TestInterFace() {
        @Override
        public void test() {
            System.out.print("hello world");
        }
    };
}
```
---

## 类的所有方法和变量均为static（Util类）
- kotlin

```
object DemoManager {
    private val TAG = "DemoManager"

    fun staticFun() {
        print("hello world")
    }
}
```

- java

```
class DemoManager {
    private static final String TAG = "DemoManager";

    public static void staticFun() {
        System.out.print("hello world");
    }
}
```
---

## 静态内部类
- kotlin

```
class OutterClass {
    object InnerClass {
        fun someFun() {
            print("hello world")
        }
    }
}
```

- java

```
class OutterClass {
    static class InnerClass {
        static void someFun() {
            System.out.print("hello world");
        }
    }
}
```
---

## 单例模式
- kotlin

```
class SomeManager private constructor() {

    companion object {
        fun getInstance(): SomeManager {
            return Holder.holder
        }
    }

    private object Holder {
        val holder = SomeManager()
    }

    fun someFun() {

    }
}
```
call

```
SomeManager.getInstance().someFun()
```

- java

```
class SomeManager {

    private SomeManager() {
    }

    private static class SingletonHolder {
        private static final SomeManager INSTANCE = new SomeManager();
    }

    public static SomeManager getInstance() {
        return SingletonHolder.INSTANCE;
    }

    public void someFun() {

    }
}
```
call

```
SomeManager.getInstance().someFun();
```
---

## 继承
- kotlin

```
open class Base(p: Int)

class Derived(p: Int) : Base(p)
```

- java

```
class Base {
    public Base(int p) {
    }
}

class Derived extends Base {
    public Derived(int p) {
        super(p);
    }
}
```
> Kotlin 中所有类都继承该 Any 类，它是所有类的超类，对于没有超类型声明的类是默认超类

> 如果一个类要被继承，需要使用open关键字进行修饰，否则就是final类
---

## 派生类的方法重写
- kotlin

```
open class Person {
    open fun study() {
        println("我毕业了")
    }
}

class Student : Person() {
    override fun study() {
        println("我在读大学")
    }
}
```

- java

```
class Person {
    protected void study() {
        System.out.print("我毕业了");
    }
}

class Student extends Person {
    @Override
    protected void study() {
        System.out.print("我在读大学");
    }
}
```
> 在Kotlin基类中，使用fun声明函数时，此函数默认为final修饰，不能被子类重写。如果允许子类重写该函数，那么就要手动添加open修饰它, 子类重写方法使用override关键词
---

## 接口
- kotlin

```
interface MyInterface {
    var name: String //name 属性, 抽象的
    fun bar()
    fun foo() {
        // 可选的方法体
        println("foo")
    }
}

class MyImpl : MyInterface {
    override var name: String = "runoob" //重写属性
    override fun bar() {
        // 方法体
        println("bar")
    }
}
```

- java

```
interface MyInterface {

    String name = "name";

    void bar();

    void foo();
}

class MyImpl implements MyInterface {
    @Override
    public void bar() {

    }

    @Override
    public void foo() {

    }
}
```
> Kotlin接口允许方法有默认实现，java不允许

> Kotlin接口可以定义属性，并且属性只能是抽象的，不允许初始化值，接口不会保存属性值，实现接口时，必须重写属性；相对的，java的接口中定义的属性实际是个static final变量，不能被重写
---

## 扩展（Kotlin特有）
- kotlin

```
class User(var name: String)

/**扩展函数**/
fun User.print() {
    print("用户名 $name")
}
```
call

```
var user = User("Runoob")
user.print()
```

> Kotlin可以对一个类的属性和方法进行扩展，且不需要继承

> 扩展是一种静态行为，对被扩展的类代码本身不会造成任何影响
---

## 模板类
- kotlin

```
class Box<T>(t: T) {
    var value = t
}
```
call

```
val box: Box<Int> = Box(1)
```
- java

```
class Box<T> {
    T value;

    public Box(T value) {
        this.value = value;
    }
}
```
call

```
Box<Integer> box = new Box<>(1);
```

> 定义泛型类型变量，可以完整地写明类型参数，如果编译器可以自动推定类型参数，也可以省略类型参数
---

## 枚举
- kotlin

```
enum class Color {
    RED, BLACK, BLUE, GREEN, WHITE
}
```

- java

```
enum Color {
    RED, BLACK, BLUE, GREEN, WHITE
}
```
---

## 委托模式
- kotlin

```
interface Base {
    fun print()
}

class BaseImpl(val x: Int) : Base {
    override fun print() {
        print(x)
    }
}

class Delegate(b: Base) : Base by b
```
call

```
val b = BaseImpl(10)
val d = Delegate(b)
d.print() // 输出 10
```
- java

```
interface Base {
    void print();
}

class BaseImpl implements Base {
    private int value;

    public BaseImpl(int value) {
        this.value = value;
    }

    @Override
    public void print() {
        System.out.print(value);
    }
}

class Delegate implements Base {

    private Base base;

    public Delegate(Base base) {
        this.base = base;
    }

    @Override
    public void print() {
        base.print();
    }
}
```
call

```
Base b = new BaseImpl(10);
Base d = new Delegate(b);
d.print();
```
> Kotlin直接支持委托模式。Kotlin通过关键字by实现委托。
---
