# Java面向对象

## 一：封装特性

- 定义：封装是面向对象的特性之一，通过不同的权限解释器，从而获得不同的权限，执行后续操作。
- 固有权限：public,protected,default,private。权限依次从高到低。

| 修饰符                    |同类中   |  同包中 | 子类中 | 不同包中  |
| --------------           |  ----   |  ----  |  ---   | -------- |
| `public`                 |   ✅   |   ✅   |  ✅   | ✅        |
| `protected`              |   ✅   |   ✅   |  ✅   | ❌（除非是子类）|
| `default`（无修饰）       |   ✅   |   ✅   |  ❌   | ❌        |
| `private`                |   ✅   |   ❌   |  ❌   | ❌        |

- 1:`public`：任何地方都可以访问，任何地方都可以修改。
  
```Java
public int age;
```

- 2:`protected` —— 受保护的：同包+子类可以访问

```Java
protected String school;
```

- 3:`default` —— 默认的：同包可以访问，子类也不能进行访问。
  
```java
int score; // 没有写任何权限修饰符
```  

- 4:`private` —— 私有的，仅当前类可访问
  
```Java
private String name;
```

例子：假设我们有两个包：com.a 和 com.b，其中：

```Java
// com.a.Person.java
package com.a;
public class Person {
    public String a = "public";
    protected String b = "protected";
    String c = "default";
    private String d = "private";
}
```

```Java
// com.b.Test.java
package com.b;
import com.a.Person;

public class Test extends Person {
    public static void main(String[] args) {
        Person p = new Person();
        System.out.println(p.a); // ✅ public
        // System.out.println(p.b); ❌ protected，不能通过父类对象访问
        // System.out.println(p.c); ❌ default，不同包
        // System.out.println(p.d); ❌ private
    }
}
```

- 继承的目的：不让外部随便修改对象的属性，只能通过方法修改。
  
- JavaBean：将属性私有化，提供get/set方法，通过方法修改属性。
  
```Java
class Person{
    private int age;
    prinvate String name;
    // 提供set 和 get方法
    // 这两个方法都是提供public的权限，外包或者其他类都可以进行调用
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

## 二：继承特性

1：定义：父类和子类之间存在继承关系，子类对象可以指向父类对象，父类对象指向子类对象。
2：作用：降低代码的冗余度，提高代码的扩展性。（本质上就是想减少代码重复）
3：语法：extends的使用

```java
class P1 extens P2{
    // 继承父类的属性和方法
}
// 上面的语法就是P1类继承P2类的写法
```

比如：

```java
class Person{
    private int age;
    prinvate String name;
    // 提供set 和 get方法
    // 这两个方法都是提供public的权限，外包或者其他类都可以进行调用
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
// 学生类继承PerSon类
class Student extends Person {
    private int score; // 成绩
}
/*
> 1:从现在开始创建一个学类的时候，成员变量有三个：age，name，score,只是操作学生类的时候，不能通过对象操作父类的age以及name变量。需要通过set和get方法进行操作才行。
> 2:学生类天然可以使用父类的方法，比如getName()方法。
*/

// 主函数的调用
public class PersonTest
{
    public static void main(String[] args)
    {
        // 父类对象指向子类
        Person  student = new Student();
        student.setName("张三");
        student.setAge(20);
        System.out.println("姓名是："+ student.getName()+"，年龄是："+ student.getAge());
    }
}
```

4：注意：继承也是有权限之分的，一般情形下使用public较多。

## 三：多态特性

1：定义：多态特性是指同一个方法在不同的子类中具有不同的功能，即子类重写了父类中的方法，这种行为就称为多态。（同一个方法调用，实现不同的行为）
2：优势：可扩展性强，新增一个子类不需要修改原有的代码。
3：缺点：由于多态是在继承的基础上实现的，所以在创建一个子类对象的时候，会创建父类，会有内存资源的消耗。
4：多态实现的条件

- 继承
- 方法重写：需要写一个和父类方法返回值以及参数值相同的方法，只是方法体不同。
- 父类的引用指向子类
  
5：例子

```java
class Animal {
    public void speak() {
        System.out.println("Animal speaks");
    }
}

class Cat extends Animal {
    @Override
    public void speak() {
        System.out.println("Cat meows");
    }
}

class Dog extends Animal {
    @Override
    public void speak() {
        System.out.println("Dog barks");
    }
}
// 主函数
public class Main {
    public static void main(String[] args) {
        Animal a1 = new Cat(); //此时还是是Animal
        Animal a2 = new Dog(); //此时还是Animal

        a1.speak(); // Cat meows 运行时绑定
        a2.speak(); // Dog barks 运行时绑定
    }
}
// 1：从上述主函数可以看出，多态使用的试运行绑定，只有执行到当前的代码段之后，才确认调用的是子类的方法还是父类的方法。

```

## 四：Object类的方法（所有类的父类）

1：Object包含的成员函数

- toString()--> 这个类也需要我们重写
  
- equals()---->这个类是需要我们重写的
  
- hashCode()
  
- getClass()---->获取当前对象运行时的“真实类”（Class 类型对象）。
  
- clone()
  
- wait()---->多线程中常用
  
- notify()---->多线程中常用
  
- notifyAll()---->多线程中常用
  
- finalize()---->多线程中常用
  
2：常见函数的重写

- equals()---->判断两个对象是否相等

不重写导致的危害

```java
// 重写equals方法
class Person{
    private String name;
    private int age;

    // 构造函数的使用

    public Person() {
    }

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
}

// 主函数
public class EqualTest {

    public static void main(String[] args) {
        // 检验两个对象的相等性
        Person person1 = new Person(18,"nihao");
        Person person2 = new Person(18,"nihao");
        // 检测两个是不是相等
        System.out.println(person1.equals(person2)); // 输出为false，在JDK中其实是两个对象，也就是地址不同
        System.out.println("person1 = "+person1); // 输出地址为：com.hanzhoudian.Person@3b07d329
        System.out.println("person2 = "+person2); // 输出地址为：com.hanzhoudian.Person@3d075dc0
    }
}
// 不重写会调用Obeject的equals方法
// 这个方法只检查传进来的对象的地址是不是一致
// 上述方式创建的是两个对象，在JVM中的地址是不同的，所以直接返回的就是false
public boolean equals(Object obj) {
    return (this == obj);
}
```

重写equals方法

```java
class Person{
    private String name;
    private int age;

    // 构造函数的使用

    public Person() {
    }

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
     // 重写equals方法
    @Override
    public boolean equals(Object o) {
        // 如果当前传入的数据与this是一个地址，也就是一个对象，但是名称不同直接返回
        if(this == o) return true;
        // 如果不是同一个对象
        // 但是要求age和name相同就返回true，直接返回true
        // 大到小，需要强转操作避免精度问题
        // 如果 o 是 Person 类型，则强转后比较 name 和 age
        if(o instanceof Person){
            Person person = (Person) o;
            if(this.age == person.age && this.name.equals(person.name)){
                return true;
            }
        }
        return false;
    }

    // 还有一种实现方式
    @Override
    public boolean equals(Object otherObject) {
        // 如果当前传入的数据与this是一个地址，也就是一个对象，但是名称不同直接返回
        if(this == otherObject) return true;
        // 判断创建otherObject是否为null，如果是null返回false，因为null不能调用函数
        if(otherObject == null) return false;
        // 判断otherObject是否为当前类对象，如果不是返回false
        if(this.getClass() != otherObject.getClass()){
            return false;
        }
        // 目的是比较name + age表示的两个对象是否相等----》指的是值相等
        Person other = (Person) otherObject; //强转
        return this.age == other.age && Objects.equals(this.name, other.name);
    }
}

// 在进行比较
public class EqualTest {

    public static void main(String[] args) {
        // 检验两个对象的相等性
        Person person1 = new Person(18,"nihao");
        Person person2 = new Person(18,"nihao");
        // 检测两个是不是相等
        System.out.println(person1.equals(person2)); // 输出为true
        System.out.println("person1 = "+ person1); // 输出地址为：com.hanzhoudian.Person@c1ad7c38
        System.out.println("person2 = "+ person2); // 输出地址为：com.hanzhoudian.Person@3d075dc0
    }
}
/* 
> 1:从源代码中可以看出，equals方法默认情况下，比较的是两个对象的地址，即判断两个对象是否相等。
这里比较的是值相等，其实在JDK中还是两个对象。
> 2:如果两个对象是同一个对象，那么两个对象地址相同。要使得值和地址都相同只需要再重写HashCode方法或者是toSting方法即可。
*/

```

重写toString方法

1.重写toString方法，返回对象的字符串表示。

```java
public class EqualTest {

    public static void main(String[] args) {
        // 检验两个对象的相等性
        Person person1 = new Person(18,"nihao");
        Person person2 = new Person(18,"nihao");
        // 检测两个是不是相等
        System.out.println(person1.equals(person2)); // 输出为true
        System.out.println("person1 = "+person1); // 输出为：person1 = Person{name='nihao', age=18}
        System.out.println("person2 = "+person2); // 输出为：person2 = Person{name='nihao', age=18}
    }
}

// 重写equals方法 + toString方法
class Person{
    private String name;
    private int age;

    // 构造函数的使用

    public Person() {
    }

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
     // 重写equals方法
    @Override
    public boolean equals(Object o) {
        // 如果当前传入的数据与this是一个地址，也就是一个对象，但是名称不同直接返回
        if(this == o) return true;
        // 如果不是同一个对象
        // 但是要求age和name相同就返回true，直接返回true
        // 大到小，需要强转操作避免精度问题
        // 如果 o 是 Person 类型，则强转后比较 name 和 age
        if(o instanceof Person){
            Person person = (Person) o;
            if(this.age == person.age && this.name.equals(person.name)){
                return true;
            }
        }
        return false;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

重写 hashCode方法

```java
public class EqualTest {

    public static void main(String[] args) {
        // 检验两个对象的相等性
        Person person1 = new Person(18,"nihao");
        Person person2 = new Person(18,"nihao");
        // 检测两个是不是相等
        System.out.println(person1.equals(person2)); // 输出为true
        System.out.println("person1 = "+ person1); // 输出为：person1 = com.hanzhoudian.Person@c1ad7c38
        System.out.println("person2 = "+ person2); // 输出为：person2 = com.hanzhoudian.Person@c1ad7c38
    }
}


class Person{
    private String name;
    private int age;

    // 构造函数的使用

    public Person() {
    }

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
     // 重写equals方法 
    @Override
    public boolean equals(Object o) {
        // 如果当前传入的数据与this是一个地址，也就是一个对象，但是名称不同直接返回
        if(this == o) return true;
        // 如果不是同一个对象
        // 但是要求age和name相同就返回true，直接返回true
        // 大到小，需要强转操作避免精度问题
        // 如果 o 是 Person 类型，则强转后比较 name 和 age
        if(o instanceof Person){
            Person person = (Person) o;
            if(this.age == person.age && this.name.equals(person.name)){
                return true;
            }
        }
        return false;
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
```
