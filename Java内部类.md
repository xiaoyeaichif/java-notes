# Java内部类

## 一：内部类的分类

### 成员内部类：直接声明在外部类的里面

#### 1：使用static修饰：静态的成员内部类

```Java
public class OutClassTest {
    public static void main(String[] args) {
        System.out.print("静态成员内部类的使用: ");
        Person.Dog  dog = new Person.Dog();
        dog.eat();
    }
}
class Person{ // 外部类
    // 静态成员内部类
    static class Dog{
        void eat(){
            System.out.println("dog eat");
        }
    }
    // 非静态成员内部类
    class Cat{
        void eat(){
            System.out.println("cat eat");
        }
    }
}
```

#### 2：不适用static修饰：非静态的成员内部类

```Java
public class OutClassTest {
    public static void main(String[] args) {
        System.out.print("非静态成员内部类使用: ");
        Person person = new Person();
        Person.Cat cat = person.new Cat();
        cat.eat();
    }
}
class Person{ // 外部类
    // 静态成员内部类
    static class Dog{
        void eat(){
            System.out.println("dog eat");
        }
    }
    // 非静态成员内部类
    class Cat{
        void eat(){
            System.out.println("cat eat");
        }
    }
}
```

### 局部内部类：声明在方法内，构造器内，代码块的类

#### 1：匿名的局部内部类

```Java
public class OutClassTest {
    public static void main(String[] args) {
        person.show();
    }
}
class Person{ // 外部类
    // 匿名局部类
    public void show(){
        class Bird{
            void fly(){
                System.out.println("Bird fly");
            }
        }
        // 创建匿名局部类的实例
        Bird bird = new Bird();
        bird.fly();
    }

    // 非匿名局部类
    public void show2(){
        class Bird{
            void fly(){
                System.out.println("Bird fly");
            }
        }
    }
}
```

#### 2：非匿名的局部内部类