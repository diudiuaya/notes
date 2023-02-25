Java 基础面试题目录

[TOC]

# 基础概念与常识
。。。
# 面向对象基础
## 面向对象和面向过程的区别
两者的主要区别在于**思考和解决问题的方式**不同：
- 面向过程：把解决问题的过程拆成一个个方法，通过一个个方法的执行解决问题。
- 面向对象会先抽象出对象，然后用对象执行方法的方式解决问题。
> 面向对象开发的程序一般更易维护、易复用、易扩展。
## 创建一个对象用什么运算符?对象实体与对象引用有何不同?
**`new` 运算符**
new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。

一个对象引用可以指向 0 个或 1 个对象（一根绳子可以不系气球，也可以系一个气球）;一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

对象和对象引用的理解 参考链接：https://baijiahao.baidu.com/s?id=1667836380258781633&wfr=spider&for=pc
## 对象的相等和引用相等的区别
对象的相等：一般比较的是内存中存放的**内容**是否相等。
引用相等：一般比较的是他们指向的**内存地址**是否相等。
## 类的构造方法的作用是什么?
构造方法是一种特殊的方法，主要作用进行**对象的初始化**。
## 如果一个类没有声明构造方法，该程序能正确执行吗?
**关键词：** 默认构造方法

能正确执行。因为一个类即使没有声明构造方法，也会有默认的不带参数的构造方法。

> 如果我们自己添加了类的构造方法（无论是否有参），Java 就不会再添加默认的无参数的构造方法了，我们一直在不知不觉地使用构造方法，这也是为什么我们在创建对象的时候后面要加一个括号（因为要调用无参的构造方法）。如果我们重载了有参的构造方法，记得都要把无参的构造方法也写出来（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。

## 构造方法有哪些特点？是否可被 override?
构造方法特点如下：
- 方法名与类名相同。
- 没有返回值，但不能用 void 声明构造函数。
- 生成类的对象时自动执行，无需调用。

**构造方法不能被 override（重写），但是可以 overload（重载）**，所以你可以看到一个类中有多个构造函数的情况。
## 为什么构造方法不能被重写？
重写的前提是要能被被继承。

构造方法的特点：
- 方法名和类名相等
- 无返回值类型，无返回值
- 生成类的对象时自动执行，无需调用。

根本无法满足方法重写条件。

另外假设可以重写父类构造器，那么子类名字就得和父类相等，显然这是不可能的，所以根本不可能重写父类构造方法。

补充： 方法的重写和重载是实现Java多态的方式，重载一般称为编译时多态，重写通过继承实现，一般称为运行时多态。
## static 关键字
作用：方便在没有创建对象的情况下进行调用，包括变量和方法。也就是说，只要类被加载了，就可以通过类名进行访问。

`static` 可以用来修饰类的成员变量和成员方法。

**静态变量**
如果在声明变量的时候使用了 `static` 关键字，那么这个变量就被称为静态变量。静态变量只在类加载的时候获取一次内存空间，这使得静态变量很节省内存空间。
静态变量存储在静态区。

由于静态变量属于一个类，所以不要通过对象引用来访问，而应该直接通过类名来访问，否则编译器会发出警告。

**静态方法**
- 静态方法属于这个类而不是这个类的对象；
- 调用静态方法的时候不需要创建这个类的对象；
- 静态方法可以访问静态变量。

静态方法不能访问非静态变量和调用非静态方法。

**静态代码块**
```java
public class StaticBlock {
    static {
        System.out.println("静态代码块");
    }

    public static void main(String[] args) {
        System.out.println("main 方法");
    }
}
```
静态代码块通常用来初始化一些静态变量，它会优先于 `main()` 方法执行。

**静态内部类**
不太常用的功能
需要注意的是：
- 第一，静态内部类不能访问外部类的所有成员变量；
- 第二，静态内部类可以访问外部类的所有静态变量，包括私有静态变量。- 第三，外部类不能声明为 static。
### 为什么 main 方法是静态的？
如果 `main` 方法不是静态的，就意味着 Java 虚拟机在执行的时候需要先创建一个对象才能调用 `main` 方法，而 `main` 方法作为程序的入口，创建一个额外的对象显得非常多余。

`java.lang.Math` 类的几乎所有方法都是静态的，可以直接通过类名来调用，不需要创建类的对象。

### 没有 main() 方法的 Java 类能执行成功吗？
Java 1.6 是可以的，但 Java 7 开始就无法执行了。**会报错找不到主类**。

静态代码块在初始集合的时候，真的非常有用。在实际的项目开发中，通常使用静态代码块来加载配置文件到内存当中。
## final 关键字
`final` 关键字可以修饰非抽象类、非抽象类成员方法和变量。

理解可参考：https://blog.csdn.net/weixin_50998882/article/details/123798335

**final变量**
被 `final` 修饰的变量无法重新赋值。换句话说，`final` 变量一旦初始化，就无法更改。不一定是在声明的时候赋值，但必须在使用之前赋初始值.

`final` 修饰的变量有三种：静态变量、实例变量和局部变量，分别表示三种类型的常量 。
`final` 修饰的局部变量可以在使用之前赋值.
`final` 修饰的静态变量必须在声明的时候赋予初始值
`final` 修饰的实例变量可以在构造函数中赋值，不同的对象同一个常量的值可以不同。
`final` 修饰对象的时候不能重新为对象赋值，但可以修改对象的属性，如下:
```java
public class Student{
    public int age;

    public static void main(String args[]){
        final Student stu =new Student();
        //修改对象的属性值可以
        stu.age =20;
        stu.age = 30;
        //为对象重新赋值不可以
        //stu =new Student();
    }
}
```
`final` 修饰的对象不能重新赋值，但可以修改对象的属性。
`final` 修饰的成员变量必须有一个默认值，否则编译器将会提醒没有初始化。
`final` 和 `static` 一起修饰的成员变量叫做常量，常量名必须全部大写。
有时候，我们还会用 `final` 关键字来修饰参数，它意味着参数在方法体内不能被再修改。
```java
public class ArgFinalTest {
    public void arg(final int age) {
    }

    public void arg1(final String name) {
    }
}
```
**final方法**
**被 final 修饰的方法不能被重写。** 如果我们在设计一个类的时候，认为某些方法不应该被重写，就应该把它设计成 `final` 的。

**final类**
如果一个类使用了 `final` 关键字修饰，那么它就无法被继承。
`final` 类中的成员变量可以根据需要设为 `final` ，但是要注意 `final` 类中的所有成员方法都会被隐式地指定为 `final` 方法。
### 一个类是 `final` 的，和一个类不是 `final`，但它所有的方法都是 `final` 的，考虑一下，它们之间有什么区别？
我能想到的一点，就是前者不能被继承，也就是说方法无法被重写；后者呢，可以被继承，然后追加一些非 final 的方法。
`String` 类就是一个 `final` 类。
### * 为什么 String 类要设置成 final 类？
- 为了实现字符串常量池
- 为了线程安全
- 为了 hashCode 的不可变性
关于String类：https://tobebetterjavaer.com/string/immutable.html
关于不可变类：https://tobebetterjavaer.com/basic-extra-meal/immutable.html

一个类的对象在通过构造方法创建后如果状态不会再被改变，那么它就是一个**不可变（immutable）类**。

一个不可变类，必须要满足以下 4 个条件：
- 1）确保类是 final 的，不允许被其他类继承。
- 2）确保所有的成员变量（字段）是 final 的，这样的话，它们就只能在构造方法中初始化值，并且不会在随后被修改。
- 3）不要提供任何 setter 方法。
- 4）如果要修改类的状态，必须返回一个新的对象。
## default 关键字

## 面向对象的三大特征
### 1. 封装
封装是指把一个对象的状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息。但是可以提供一些可以被外界访问的方法来操作属性。

封装的好处：
1. 提高代码的安全性。
2. 提高代码的复用性。
3. “高内聚”：封装细节，便于修改内部代码，提高可维护性。
4. “低耦合”：简化外部调用，便于调用者使用，便于扩展和协作
### 2. 继承
继承是**使用已存在的类的定义作为基础建立新类**的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类。

继承的好处：可重用性、可维护性、开发效率
通过使用继承，可以快速地创建新的类，可以提高代码的重用，程序的可维护性，节省大量创建新类的时间，提高我们的开发效率。
关于继承，记住：
1. 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。
2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
3. 子类可以通过重写用自己的方式实现父类的方法。
### 3. 多态
多态，顾名思义，表示一个对象具有多种的状态，具体表现为**父类的引用指向子类的实例**。

多态的特点:
- 对象类型和引用类型之间具有继承（类）/实现（接口）的关系；
- 引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；
- 多态不能调用“只在子类存在但在父类不存在”的方法；
- 如果子类重写了父类的方法，真正执行的是子类覆盖的方法，如果子类没有覆盖父类的方法，执行的是父类的方法。

多态的好处：
- 可替换性（substitutability）。多态对已存在代码具有可替换性。例如，多态对动物Animal 类工作，对其他任何动物猫，狗，兔子也同样工作。降低代码耦合度。
- 可扩充性（extensibility）。多态对代码具有可扩充性。增加新的子类不影响已存在类的多态性、继承性，以及其他特性的运行和操作。实际上新加子类更容易获得多态功能。 

目前在日常开发中经常使用多态的地方就是使用集合的时候：
```java
List list = new ArrayList();
Map map = new HashMap();
```
### 多态存在的三个必要条件
- 继承
- 重写
- 父类引用指向子类对象：`Parent p = new Child();`
![Alt text](https://www.runoob.com/wp-content/uploads/2013/12/2DAC601E-70D8-4B3C-86CC-7E4972FC2466.jpg)

## 接口和抽象类有什么共同点和区别？
**共同点：**
- 都不能被实例化。
- 都可以包含抽象方法。
- 都可以有默认实现的方法（Java 8 可以用 `default` 关键字在接口中定义默认方法）。

**区别：**
- 接口主要用于对类的**行为**进行约束，你实现了某个接口就具有了对应的行为。抽象类主要用于代码复用，强调的是**所属关系**。
- 一个类只能继承一个类，但是可以实现多个接口。
- 接口中的成员变量只能是 `public static final` 类型的，不能被修改且必须有初始值，而抽象类的成员变量默认 `default`，可在子类中被重新定义，也可被重新赋值。
## 深拷贝和浅拷贝区别了解吗？什么是引用拷贝？
**深拷贝和浅拷贝区别:**
- 浅拷贝：浅拷贝会在堆上创建一个新的对象（区别于引用拷贝的一点），不过，如果原对象内部的属性是引用类型的话，浅拷贝会直接复制内部对象的引用地址，也就是说拷贝对象和原对象共用同一个内部对象。
- 深拷贝 ：深拷贝会完全复制整个对象，包括这个对象所包含的内部对象。
  
> 口头回答：深拷贝和浅拷贝的主要区别在于**拷贝对象时对内部对象的处理**。
> - 如果拷贝对象的内部属性是引用类型，浅拷贝会直接复制内部对象的引用地址。也就是说拷贝对象和原对象共用同一个内部对象。
> - 深拷贝会完全复制整个对象，包括这个对象包含的所有内部对象。

`clone()` 是浅拷贝，而不是深拷贝。可以通过重写 `clone()` 实现浅拷贝和深拷贝。
https://baijiahao.baidu.com/s?id=1732636924566537520&wfr=spider&for=pc
https://baijiahao.baidu.com/s?id=1717686571719151382&wfr=spider&for=pc
实现浅拷贝和深拷贝的方法：

**引用拷贝**

简单来说，引用拷贝就是两个不同的引用指向同一个对象。

浅拷贝、深拷贝与引用拷贝：

![Alt text](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/basis/shallow%26deep-copy.png)

## 说说 List 复制深拷贝和浅拷贝的用法与区别？
https://baijiahao.baidu.com/s?id=1705062480538000508&wfr=spider&for=pc

# Java 常见类
## Object
### Object 类的常见方法有哪些？
Object 类是一个特殊的类，是所有类的父类。它主要提供了以下 11 个方法：
```java
/**
 * native 方法，用于返回当前运行时对象的 Class 对象，使用了 final 关键字修饰，故不允许子类重写。
 */
public final native Class<?> getClass()
/**
 * native 方法，用于返回对象的哈希码，主要使用在哈希表中，比如 JDK 中的HashMap。
 */
public native int hashCode()
/**
 * 用于比较 2 个对象的内存地址是否相等，String 类对该方法进行了重写以用于比较字符串的值是否相等。
 */
public boolean equals(Object obj)
/**
 * naitive 方法，用于创建并返回当前对象的一份拷贝。
 */
protected native Object clone() throws CloneNotSupportedException
/**
 * 返回类的名字实例的哈希码的 16 进制的字符串。建议 Object 所有的子类都重写这个方法。
 */
public String toString()
/**
 * native 方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
 */
public final native void notify()
/**
 * native 方法，并且不能重写。跟 notify 一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
 */
public final native void notifyAll()
/**
 * native方法，并且不能重写。暂停线程的执行。注意：sleep 方法没有释放锁，而 wait 方法释放了锁 ，timeout 是等待时间。
 */
public final native void wait(long timeout) throws InterruptedException
/**
 * 多了 nanos 参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 毫秒。。
 */
public final void wait(long timeout, int nanos) throws InterruptedException
/**
 * 跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
 */
public final void wait() throws InterruptedException
/**
 * 实例被垃圾回收器回收的时候触发的操作
 */
protected void finalize() throws Throwable { }
```
### == 和 equals() 的区别
`==` 对于基本类型和引用类型的作用效果是不同的：

- 对于基本数据类型来说，`==` 比较的是值。
- 对于引用数据类型来说，`==` 比较的是对象的内存地址。

> 因为 Java 只有值传递，所以，对于 == 来说，不管是比较基本数据类型，还是引用数据类型的变量，其本质比较的都是值，只是引用类型变量存的值是对象的地址。

`equals()` 不能用于判断基本数据类型的变量，只能用来判断两个对象是否相等。`equals()` 方法存在于Object类中，而Object类是所有类的直接或间接父类，因此所有的类都有 `equals()` 方法。

`Object` 类 `equals()` 方法：
```java
public boolean equals(Object obj) {
     return (this == obj);
}
```

`equals()` 方法存在两种使用情况：

- 类没有重写 `equals()` 方法 ：通过 `equals()` 比较该类的两个对象时，等价于通过 “==” 比较这两个对象，使用的默认是 `Object` 类 `equals()` 方法。
- 类重写了 `equals()` 方法 ：一般我们都重写 `equals()` 方法来比较两个对象中的属性是否相等；若它们的属性相等，则返回 `true` (即，认为这两个对象相等)。

String 中的 equals 方法是被重写过的，因为 Object 的 equals 方法是比较的对象的内存地址，而 String 的 equals 方法比较的是对象的值。

当创建 String 类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 String 对象。

String类equals()方法：
```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```
### hashCode() 有什么用？
参考链接：
https://blog.csdn.net/weixin_44364444/article/details/120054230
https://blog.csdn.net/seu_calvin/article/details/52094115
作用：获取哈希码。哈希值是int类型，32位。
哈希码代表对象在hash表中的位置。

从Object角度看，JVM每new一个Object，它都会将这个Object丢到一个Hash表中去，这样的话，下次做Object的比较或者取这个对象的时候（读取过程），它会根据对象的HashCode再从Hash表中取这个对象。这样做的目的是提高取对象的效率。若HashCode相同再去调用equal。

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）
### 为什么要有 hashCode ？
`hashCode()` 和 `equals()` 都是用于比较两个对象是否相等。
以“`HashSet` 如何检查重复”为例子来说明为什么要有 `hashCode`？

当你把对象加入 `HashSet` 时，`HashSet` 会先计算对象的 `hashCode` 值来判断对象加入的位置，同时也会与其他已经加入的对象的 hashCode 值作比较，如果没有相符的 hashCode，HashSet 会假设对象没有重复出现。但是如果发现有相同 hashCode 值的对象，这时会调用 equals() 方法来检查 hashCode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。
### 为什么 JDK 还要同时提供这两个方法呢？
因为在一些容器（比如 HashMap、HashSet）中，有了 hashCode() 之后，判断元素是否在对应容器中的效率会更高（参考添加元素进HashSet的过程）！我们在前面也提到了添加元素进HashSet的过程，如果 HashSet 在对比的时候，同样的 hashCode 有多个对象，它会继续使用 equals() 来判断是否真的相同。也就是说 hashCode 帮助我们大大缩小了查找成本。

### 为什么重写 equals() 时必须重写 hashCode() 方法？
因为两个相等的对象的 `hashCode` 值必须相等。也就是说如果 `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode` 值也要相等。如果重写 `equals()` 时没有重写 `hashCode()` 方法的话就可能会导致 `equals` 方法判断是相等的两个对象，`hashCode` 值却不相等。

> 两个对象有相同的 `hashCode` 值，他们也不一定是相等的（哈希碰撞）。
### 重写 equals() 时没有重写 hashCode() 方法的话，使用 HashMap 可能会出现什么问题？


## String
### String、StringBuffer、StringBuilder 的区别？
**1. 可变性**
`String` 是不可变的。
`StringBuilder` 与 `StringBuffer` 都继承自 `AbstractStringBuilder` 类，在 `AbstractStringBuilder` 中也是使用字符数组保存字符串，不过没有使用 `final` 和 `private `关键字修饰，最关键的是这个 `AbstractStringBuilder` 类还提供了很多修改字符串的方法比如 `append` 方法。
```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    char[] value;
    public AbstractStringBuilder append(String str) {
        if (str == null)
            return appendNull();
        int len = str.length();
        ensureCapacityInternal(count + len);
        str.getChars(0, len, value, count);
        count += len;
        return this;
    }
  	//...
}
```

**2. 线程安全性**
`String` 中的对象是不可变的，也就可以理解为常量，线程安全。
`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。
`StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

>补充：`AbstractStringBuilder` 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。

**3. 性能**
每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。

`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

**对于三者使用的总结：**
1. 操作少量的数据: 适用 `String`
2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
3. 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`
### String为什么是不可变的？
1.`String` 类中使用 `final` 关键字修饰的字符数组来保存字符串，而且保存字符串的数组是私有的，并且`String` 类没有提供/暴露修改这个字符串的方法。

2.`String` 类被 `final` 修饰导致其不能被继承，进而避免了子类破坏 `String` 不可变。

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
    private final char value[];
	//...
}
```

补充：
在 Java 9 之后，`String` 、`StringBuilder` 与 `StringBuffer` 的实现改用 `byte` 数组存储字符串。

```java
public final class String implements java.io.Serializable,Comparable<String>, CharSequence {
    // @Stable 注解表示变量最多被修改一次，称为“稳定的”。
    @Stable
    private final byte[] value;
}

abstract class AbstractStringBuilder implements Appendable, CharSequence {
    byte[] value;
}
```
Java 9 为何要将 String 的底层实现由 char[] 改成了 byte[] ?新版的 String 其实支持两个编码方案： Latin-1 和 UTF-16。如果字符串中包含的汉字没有超过 Latin-1 可表示范围内的字符，那就会使用 Latin-1 作为编码方案。Latin-1 编码方案下，byte 占一个字节(8 位)，char 占用 2 个字节（16），byte 相较 char 节省一半的内存空间。JDK 官方就说了绝大部分字符串对象只包含 Latin-1 可表示的字符。
![Alt text](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/jdk9-string-latin1.png)
如果字符串中包含的汉字超过 Latin-1 可表示范围内的字符，byte 和 char 所占用的空间是一样的。
### 字符串拼接用“+” 还是 StringBuilder?
Java 语言本身并不支持运算符重载，“+”和“+=”是专门为 String 类重载过的运算符，也是 Java 中仅有的两个重载过的运算符。

字符串对象通过“+”的字符串拼接方式，实际上是通过 `StringBuilder` 调用 `append()` 方法实现的，拼接完成之后调用 `toString()` 得到一个 `String` 对象 。不过，在循环内使用“+”进行字符串的拼接的话，存在比较明显的缺陷：编译器不会创建单个 `StringBuilder` 以复用，会导致创建过多的 `StringBuilder` 对象。如果直接使用 `StringBuilder` 对象进行字符串拼接的话，就不会存在这个问题了。
```java
String[] arr = {"he", "llo", "world"};
String s = "";
for (int i = 0; i < arr.length; i++) {
    s += arr[i];
}
System.out.println(s);


String[] arr = {"he", "llo", "world"};
StringBuilder s = new StringBuilder();
for (String value : arr) {
    s.append(value);
}
System.out.println(s);
```
### String equals() 和 Object equals() 有何区别？
`String` 中的 `equals` 方法是被重写过的，比较的是 `String` 字符串的值是否相等。
`Object` 的 `equals` 方法是比较的对象的内存地址。
### 字符串常量池的作用了解吗？
**字符串常量池** 是 JVM 为了提升性能和减少内存消耗针对字符串（String 类）专门开辟的一块区域，主要目的是为了**避免字符串的重复创建**。
```java
// 在堆中创建字符串对象”ab“
// 将字符串对象”ab“的引用保存在字符串常量池中
String aa = "ab";
// 直接返回字符串常量池中字符串对象”ab“的引用
String bb = "ab";
System.out.println(aa==bb);// true
```
### String s1 = new String("abc");这句话创建了几个字符串对象？
会创建 1 或 2 个字符串对象。

1、如果字符串常量池中不存在字符串对象“abc”的引用，那么会在堆中创建 2 个字符串对象“abc”。
![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/open-source-project/image-20220413175809959.png)

`ldc` 命令用于**判断字符串常量池中是否保存了对应的字符串对象的引用**，如果保存了的话直接返回，如果没有保存的话，会在堆中创建对应的字符串对象并将该字符串对象的引用保存到字符串常量池中。

2、如果字符串常量池中已存在字符串对象“abc”的引用，则只会在堆中创建 1 个字符串对象“abc”。
### intern 方法有什么作用?
`String.intern()` 是一个 native（本地）方法，其作用是**将指定的字符串对象的引用保存在字符串常量池中**，可以简单分为两种情况：
- 如果字符串常量池中保存了对应的字符串对象的引用，就直接返回该引用。
- 如果字符串常量池中没有保存了对应的字符串对象的引用，那就在常量池中创建一个指向该字符串对象的引用并返回。

```java
// 在堆中创建字符串对象”Java“
// 将字符串对象”Java“的引用保存在字符串常量池中
String s1 = "Java";
// 直接返回字符串常量池中字符串对象”Java“对应的引用
String s2 = s1.intern();
// 会在堆中在单独创建一个字符串对象
String s3 = new String("Java");
// 直接返回字符串常量池中字符串对象”Java“对应的引用
String s4 = s3.intern();
// s1 和 s2 指向的是堆中的同一个对象
System.out.println(s1 == s2); // true
// s3 和 s4 指向的是堆中不同的对象
System.out.println(s3 == s4); // false
// s1 和 s4 指向的是堆中的同一个对象
System.out.println(s1 == s4); //true
```
### String 类型的变量和常量做“+”运算时发生了什么？
先来看字符串不加 `final` 关键字拼接的情况（JDK1.8）：
```java
String str1 = "str";
String str2 = "ing";
String str3 = "str" + "ing";
String str4 = str1 + str2;
String str5 = "string";
System.out.println(str3 == str4);//false
System.out.println(str3 == str5);//true
System.out.println(str4 == str5);//false
```
**对于编译期可以确定值的字符串，也就是常量字符串 ，jvm 会将其存入字符串常量池。** 并且，字符串常量拼接得到的字符串常量在编译阶段就已经被存放字符串常量池，这个得益于编译器的优化。

在编译过程中，Javac 编译器（下文中统称为编译器）会进行一个叫做 **常量折叠(Constant Folding)** 的代码优化。

并不是所有的常量都会进行折叠，只有编译器在程序编译期就可以确定值的常量才可以：
- 基本数据类型( byte、boolean、short、char、int、float、long、double)以及字符串常量。
- `final` 修饰的基本数据类型和字符串变量
- 字符串通过 “+”拼接得到的字符串、基本数据类型之间算数运算（加减乘除）、基本数据类型的位运算（<<、>>、>>> ）

引用的值在程序编译期是无法确定的，编译器无法对其进行优化。
# 异常
Java 异常类层次结构图概览 ：
![Alt text](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/basis/types-of-exceptions-in-java.png)

### Exception 和 Error 有什么区别？
所有的异常都有一个共同的祖先 `java.lang` 包中的 `Throwable` 类。`Throwable` 类有两个重要的子类:

- `Exception` :程序本身可以处理的异常，可以通过 `catch` 来进行捕获。`Exception` 又可以分为 Checked Exception (受检查异常，必须处理) 和 Unchecked Exception (不受检查异常，可以不处理)。
- `Error` ：`Error` 属于程序无法处理的错误 ，我们~~没办法通过 `catch` 来进行捕获~~不建议通过catch捕获 。例如 Java 虚拟机运行错误（Virtual MachineError）、虚拟机内存不够错误(OutOfMemoryError)、类定义错误（NoClassDefFoundError）等 。这些异常发生时，Java 虚拟机（JVM）一般会选择线程终止。

## Checked Exception 和 Unchecked Exception 有什么区别？
**Checked Exception** 即 受检查异常 ，Java 代码在编译过程中，如果受检查异常没有被 `catch` 或者 `throws` 关键字处理的话，就没办法通过编译。

除了 `RuntimeException` 及其子类以外，其他的 `Exception` 类及其子类都属于受检查异常。常见的受检查异常有： IO 相关的异常、`ClassNotFoundException` 、`SQLException`...。

**Unchecked Exception** 即 不受检查异常 ，Java 代码在编译过程中 ，我们即使不处理不受检查异常也可以正常通过编译。`RuntimeException` 及其子类都统称为非受检查异常，常见的有（建议记下来，日常开发中会经常用到）：
- `NullPointerException` (空指针错误)
- `IllegalArgumentException` (参数错误比如方法入参类型错误)
- `NumberFormatException`（字符串转换为数字格式错误，`IllegalArgumentException` 的子类）
- 
- `ArrayIndexOutOfBoundsException`（数组越界错误）
- `ClassCastException`（类型转换错误）
- `ArithmeticException`（算术错误）
- `SecurityException` （安全错误比如权限不够）
- `UnsupportedOperationException` (不支持的操作错误比如重复创建同一用户)
## Throwable 类常用方法有哪些？
- `String getMessage()`: 返回异常发生时的简要描述
- `String toString()`: 返回异常发生时的详细信息
- `String getLocalizedMessage()`: 返回异常对象的本地化信息。使用 `Throwable` 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 `getMessage()` 返回的结果相同
- `void printStackTrace()`: 在控制台上打印 `Throwable` 对象封装的异常信息
## try-catch-finally 如何使用？
- `try` 块 ： 用于捕获异常。其后可接零个或多个  `catch` 块，如果没有 `catch` 块，则必须跟一个 `finally` 块。
- `catch` 块 ： 用于处理 try 捕获到的异常。
- `finally` 块 ： 无论是否捕获或处理异常，`finally` 块里的语句都会被执行。当在 `try` 块或 `catch` 块中遇到 `return` 语句时，`finally` 语句块将在方法返回之前被执行。

```java
try {
    System.out.println("Try to do something");
    throw new RuntimeException("RuntimeException");
} catch (Exception e) {
    System.out.println("Catch Exception -> " + e.getMessage());
} finally {
    System.out.println("Finally");
}
```
输出
```
Try to do something
Catch Exception -> RuntimeException
Finally
```
**注意：不要在 finally 语句块中使用 return!** 当 try 语句和 finally 语句中都有 return 语句时，try 语句块中的 return 语句会被忽略。这是因为 try 语句中的 return 返回值会先被暂存在一个本地变量中，当执行到 finally 语句中的 return 之后，这个本地变量的值就变为了 finally 语句中的 return 返回值。
## finally 中的代码一定会执行吗？
不一定的！在某些情况下，finally 中的代码不会被执行。

就比如说 finally 之前虚拟机被终止运行的话，finally 中的代码就不会被执行。

```java
try {
    System.out.println("Try to do something");
    throw new RuntimeException("RuntimeException");
} catch (Exception e) {
    System.out.println("Catch Exception -> " + e.getMessage());
    // 终止当前正在运行的Java虚拟机
    System.exit(1);
} finally {
    System.out.println("Finally");
}
```

输出：
```
Try to do something
Catch Exception -> RuntimeException
```

另外，在以下 2 种特殊情况下，finally 块的代码也不会被执行：
1. 程序所在的线程死亡。
2. 关闭 CPU。
## 如何使用 `try-with-resources` 代替`try-catch-finally`？
**关键词：关闭资源**

1. 适用范围（资源的定义）： 任何实现 java.lang.AutoCloseable或者 java.io.Closeable 的对象
2. 关闭资源和 finally 块的执行顺序： 在 try-with-resources 语句中，任何 catch 或 finally 块在声明的资源关闭后运行

**面对必须要关闭的资源**，我们总是应该优先使用 `try-with-resources` 而不是`try-finally`。随之产生的代码更简短，更清晰，产生的异常对我们也更有用。`try-with-resources`语句让我们更容易编写必须要关闭的资源的代码，若采用`try-finally`则几乎做不到这点。

多个资源需要关闭的时候，使用 `try-with-resources` 实现起来也非常简单，如果你还是用`try-catch-finally`可能会带来很多问题。
## 异常使用有哪些需要注意的地方？
- 不要把异常定义为静态变量，因为这样会导致异常栈信息错乱。每次手动抛出异常，我们都需要手动 new 一个异常对象抛出。
- 抛出的异常信息一定要有意义。建议抛出更加具体的异常比如字符串转换为数字格式错误的时候应该抛出`NumberFormatException`而不是其父类`IllegalArgumentException`。
- 使用日志打印异常之后就不要再抛出异常了（两者不要同时存在一段代码逻辑中）。
# 泛型
## 什么是泛型？有什么作用？
Java泛型是JDK 5中引入的一个新特性，其本质是**参数化类型**，也就是说所操作的数据类型被指定为一个参数（type parameter）。
这种参数类型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。

使用泛型参数，可以增强代码的可读性以及稳定性。

编译器可以对泛型参数进行检测，并且通过泛型参数可以指定传入的对象类型。比如 `ArrayList<Person> persons = new ArrayList<Person>()` 这行代码就指明了该 `ArrayList` 对象只能传入 `Person` 对象，如果传入其他类型的对象就会报错。
```java
ArrayList<E> extends AbstractList<E>
```
## 泛型的使用方式有哪几种？
泛型一般有三种使用方式:**泛型类**、**泛型接口**、**泛型方法**。

1.泛型类：
```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{

    private T key;

    public Generic(T key) {
        this.key = key;
    }

    public T getKey(){
        return key;
    }
}

如何实例化泛型类：

Generic<Integer> genericInteger = new Generic<Integer>(123456);
```

2.泛型接口 ：
```java
public interface Generator<T> {
    public T method();
}

实现泛型接口，不指定类型：

class GeneratorImpl<T> implements Generator<T>{
    @Override
    public T method() {
        return null;
    }
}

实现泛型接口，指定类型：class GeneratorImpl<T> implements Generator<String>{
    @Override
    public String method() {
        return "hello";
    }
}
```
3.泛型方法 ：
```java
public static < E > void printArray( E[] inputArray ){
    for ( E element : inputArray ){
        System.out.printf( "%s ", element );
    }
    System.out.println();
}

使用：
// 创建不同类型数组： Integer, Double 和 Character
Integer[] intArray = { 1, 2, 3 };
String[] stringArray = { "Hello", "World" };
printArray( intArray  );
printArray( stringArray  );

```
> 注意: public static < E > void printArray( E[] inputArray ) 一般被称为静态泛型方法;在 java 中泛型只是一个占位符，必须在传递类型后才能使用。类在实例化时才能真正的传递类型参数，由于静态方法的加载先于类的实例化，也就是说类中的泛型还没有传递真正的类型参数，静态的方法的加载就已经完成了，所以静态泛型方法是没有办法使用类上声明的泛型的。只能使用自己声明的`<E>`
## 项目中哪里用到了泛型？
- 自定义接口通用返回结果 `CommonResult<T>` 通过参数 `T` 可根据具体的返回类型动态指定结果的数据类型
- 定义 `Excel` 处理类 `ExcelUtil<T>` 用于动态指定 `Excel` 导出的数据类型
- 构建集合工具类（参考 `Collections` 中的 `sort`, `binarySearch` 方法）。
```java
public static <T extends Comparable<? super T>> void sort(List<T> list) {
        list.sort(null);
    }
```
# 反射
## 什么是反射？
反射是指在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取信息以及动态调用对象的方法的功能称为java语言的反射机制。（程序在运行时能够获取自身的信息）

框架的灵魂，它赋予了我们在运行时分析类以及执行类中方法的能力。通过反射你可以获取任意一个类的所有属性和方法，你还可以调用这些方法和属性。
## 反射的优缺点？
优点：可以让代码更加灵活、为各种框架提供开箱即用的功能提供了便利
缺点：反射让我们在运行时有了分析操作类的能力的同时，也增加了安全问题，比如可以无视泛型参数的安全检查（泛型参数的安全检查发生在编译时）。另外，反射的性能也要稍差点，不过，对于框架来说实际是影响不大的。
## 反射的应用场景？
像 Spring/Spring Boot、MyBatis 等等框架中都大量使用了反射机制。这些框架中也大量使用了 **动态代理**，而动态代理的实现也依赖反射。
比如下面是通过 JDK 实现动态代理的示例代码，其中就使用了反射类 `Method` 来调用指定的方法。
```java
public class DebugInvocationHandler implements InvocationHandler {
    /**
     * 代理类中的真实对象
     */
    private final Object target;

    public DebugInvocationHandler(Object target) {
        this.target = target;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
        System.out.println("before method " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("after method " + method.getName());
        return result;
    }
}
```
> 代理：给某一个对象提供一个代理，并由代理对象控制对真实对象的访问。
> 代理模式是结构型设计模式的一种，根据字节码文件的创建时机来分类，可以分为 **静态代理** 和 **动态代理** 。
> https://www.cnblogs.com/huang2979127746/p/16719099.html

另外，像 Java 中的一大利器 **注解** 的实现也用到了反射。

为什么你使用 Spring 的时候 ，一个`@Component`注解就声明了一个类为 Spring Bean 呢？为什么你通过一个 `@Value` 注解就读取到配置文件中的值呢？究竟是怎么起作用的呢？

这些都是因为你可以基于反射分析类，然后获取到类/属性/方法/方法的参数上的注解。你获取到注解之后，就可以做进一步的处理。
# 注解
## 什么是注解？
`Annotation` （注解） 是 Java5 开始引入的新特性，可以看作是**一种特殊的注释**，主要用于修饰类、方法或者变量，提供某些信息供程序在编译或者运行时使用。
注解本质是一个继承了 `Annotation` 的特殊接口：
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {

}

public interface Override extends Annotation{

}
```
JDK 提供了很多内置的注解（比如 `@Override` 、`@Deprecated`），同时，我们还可以自定义注解。
## 注解的解析方法有哪几种？
注解只有被解析之后才会生效，常见的解析方法有两种：
- **编译期直接扫描** ：编译器在编译 Java 代码的时候扫描对应的注解并处理，比如某个方法使用`@Override` 注解，编译器在编译的时候就会检测当前的方法是否重写了父类对应的方法。
- **运行期通过反射处理** ：像框架中自带的注解(比如 Spring 框架的 `@Value` 、`@Component`)都是通过反射来进行处理的。
# SPI
## 什么是SPI?
SPI 即 Service Provider Interface ，字面意思就是：“服务提供者的接口”，我的理解是：专门提供给服务提供者或者扩展框架功能的开发者去使用的一个接口。
# 序列化和反序列化
## 什么是序列化？什么是反序列化？
**序列化：** 将数据结构或对象转换成二进制字节流的过程
**反序列化：** 将在序列化过程中所生成的二进制字节流转换成数据结构或者对象的过程

如果我们需要持久化 Java 对象比如将 Java 对象保存在文件中，或者在网络传输 Java 对象，这些场景都需要用到序列化。

序列化和反序列化常见应用场景：
- 对象在进行网络传输（比如远程方法调用 RPC 的时候）之前需要先被序列化，接收到序列化的对象之后需要再进行反序列化；
- 将对象存储到文件之前需要进行序列化，将对象从文件中读取出来需要进行反序列化；
- 将对象存储到数据库（如 Redis）之前需要用到序列化，将对象从缓存数据库中读取出来需要反序列化；
- 将对象存储到内存之前需要进行序列化，从内存中读取出来之后需要进行反序列化。
## 序列化协议对应于 TCP/IP 4 层模型的哪一层？
我们知道网络通信的双方必须要采用和遵守相同的协议。TCP/IP 四层模型是下面这样的，序列化协议属于哪一层呢？
应用层
传输层
网络层
网络接口层
![Alt text](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/cs-basics/network/tcp-ip-4-model.png)

如上图所示，OSI 七层协议模型中，**表示层** 做的事情主要就是对应用层的用户数据进行处理转换为二进制流。反过来的话，就是将二进制流转换成应用层的用户数据。这不就对应的是序列化和反序列化么？

因为，OSI 七层协议模型中的应用层、表示层和会话层对应的都是 TCP/IP 四层模型中的应用层，所以序列化协议属于 TCP/IP 协议**应用层** 的一部分。

## 如果有些字段不想进行序列化怎么办？
对于不想进行序列化的变量，使用 `transient` 关键字修饰。`transient` 关键字的作用是：阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被 `transient` 修饰的变量值不会被持久化和恢复。

关于 `transient` 还有几点注意：
- `transient` 只能修饰变量，不能修饰类和方法。
- `transient` 修饰的变量，在反序列化后变量值将会被置成类型的默认值。例如，如果是修饰 `int` 类型，那么反序列后结果就是 `0`。
- `static` 变量因为不属于任何对象(Object)，所以无论有没有 `transient` 关键字修饰，均不会被序列化。

## 常见序列化协议有哪些？
JDK 自带的序列化方式一般不会用 ，因为序列化效率低并且存在安全问题。比较常用的序列化协议有 Hessian、Kryo、Protobuf、ProtoStuff，这些都是基于二进制的序列化协议。

像 JSON 和 XML 这种属于文本类序列化方式。虽然可读性比较好，但是性能较差，一般不会选择。
## 为什么不推荐使用 JDK 自带的序列化？
我们很少或者说几乎不会直接使用 JDK 自带的序列化方式，主要原因有下面这些原因：
- **不支持跨语言调用** : 如果调用的是其他语言开发的服务的时候就不支持了。
- **性能差** ：相比于其他序列化框架性能更低，主要原因是序列化之后的字节数组体积较大，导致传输成本加大。
- **存在安全问题** ：序列化和反序列化本身并不存在问题。但当输入的反序列化的数据可被用户控制，那么攻击者即可通过构造恶意输入，让反序列化产生非预期的对象，在此过程中执行构造的任意代码。
## I/O
### Java IO 流了解吗？

### I/O 流为什么要分为字节流和字符流呢?

### Java IO 中的设计模式有哪些？

### BIO、NIO 和 AIO 的区别？

## 语法糖