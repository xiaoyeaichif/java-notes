# Java接口的使用及注意事项

## 一：接口的使用和定义

### 1：接口的定义：是一种 抽象类型，用于指定类必须实现的一组方法，是面向对象编程中实现多态和解耦的重要机制。需要注意的是，接口只是提供一种规范，具体的实现由对应的方法来做。

### 2：接口使用

```Java
interface InterfaceName{ 
    //接口中的成员变量, 需要注意的是，接口中成员变量默认是public static final的

    //接口中的成员方法,默认是abstract方法，也就是public abstract
}
// ---- 常见的用法,定义一个eat接口，不同的动物或者人执行的eat操作逻辑不同
interface Eatable{
    void eat();
}
// ------ 如何使用，也是需要重写接口当中的函数来进行
class Dog implements Eatable{
    @Override
    public void eat(){
        System.out.println("狗吃狗粮");
    }
}
```

## 二：接口与类有什么区别？

1. 接口与抽象类区别：抽象类可以有抽象方法，也可以有具体方法，接口只能有抽象方法。

2. 接口可以实现多继承，而类只能单继承，这是java语法规定的。

3. 接口中成员变量默认是public static final的，而抽象类中的成员函数是自定义的。

4. 接口不能有构造函数，而抽象类可以有构造函数。

## 三：接口的新特性

默认的实现:  接口中可以有默认的实现方法，接口中的方法默认是抽象方法，但是接口中的方法可以有默认的实现方法。

```Java
public interface MyInterface {
    default void defaultMethod() {
        System.out.println("默认方法");
    }
//
    static void staticMethod() {
        System.out.println("静态方法");
    }
}
```