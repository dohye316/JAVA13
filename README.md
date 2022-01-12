# JAVA13
final 讲解
final关键字
基本介绍
final
可以修饰类、属性、方法和局部变量
在某些情况下，程序员可能有以下需求，就会使用到final
1.当不希望类被继承时，可以用final修饰
2.当不希望父类的某个方法被子类覆盖/重写时，可以用final关键字修饰。
3.当不希望类的某个属性的值被修改，可以用final修饰。
4.当不希望某个局部变量被修改，可以使用final修饰
public class Final01 {
}
//如果我们要求A类不能被其他类继承
//可以使用final修饰 A类
final class A{
    
}
//class B extends A{
//    
//}不能被继承不能重写，


final使用注意事项和细节讨论
1.final修饰的属性又叫常量，一般用xx_xx_xx来命名
2.final修饰的属性在定义时，必须赋初值，并且以后不能再修改，赋值可以在如下位置之一：
1.定义时：如 public final double TAX_RATE = 0.08;
2.在构造器中
3.在代码块中
3.如果final修饰的属性是静态的，则初始化的位置只能是
1.定义时 2.在静态代码块 不能再构造器中赋值。
4.final类不能继承，但是可以实例化对象。
5.如果类不是final类，但是含有final方法，则该方法虽然不能重写，但是可以被继承。

 
final关键字
5.一般来说，如果一个类已经是final类了，就没有必要再将方法修饰成final方法。
6.final不能修饰构造方法（即构造器）
7.final和static往往搭配使用，效率更高，底层编译器做了优化处理。
8.包装类（Integer，Double，Float，Boolean等都是final）
，String也是final类





抽象类
当父类的某些方法，需要声明，但是又不确定如何实现，可以将其声明为抽象方法，那么这个类就是抽象类

abstract class Animal {
    private String name;
    public Animal(String name){
        this.name =name;
    }
    //思考：这里eat 这里你实现了，其实没有什么意义
     //即：父类方法不确定性的问题
     //考虑将该方法设计成为抽象（abstract）方法
     //所谓抽象方法就是没有实现的方法
     //所谓没有实现就是没有方法体
     //当一个类中存在抽象方法时，需要将该类声明为abstract
     public abstract void eat();
 }
抽象类介绍：
1.用abstra传统关键字来修饰一个类时，这个类就叫抽象类
访问修饰符abstract类名{}
2.用abstract 关键字来修饰一个方法时，这个方法就是抽象方法访问修饰符abstract返回类型 方法名（参数列表）；//没有方法体
3.抽象类的 价值更多作用是在于设计，是设计者设计好后，让子类继承并实现抽象类（）
4.抽象类，是考官比较爱问的知识点，在框架和设计模式使用较多

抽象类细节：
1.抽象类不能被实例化
2.抽象类不一定要包含abstract方法。也就是说，抽象类可以没有abstract方法
3.一旦类包含了abstract方法，则这个类必须要声明为abstract
4.abstract只能修饰类和方法，不能修饰属性和其他
。
5.抽象类可以有任意成员【因为抽象类还是类】，比如：非抽象方法，构造器，静态属性等等
6.抽象方法不能有主体，即不能实现
abstract void name()不能有{}
7.如果一个类继承了抽象类，则它必须实现抽象类的所有抽象方法，除非它自己也声明为abstract类。
抽象方法不能使用private/final和static来修饰，因为这些关键字都是重写相违背的


抽象类
抽象类细节
模板设计模式
1.有多个类，完成不同的任务job
2.要求统计得到各自完成任务的时间
//设计一个抽象类Template，
//1.编写方法calculateTime（），可以计算某段代码的耗时时间
//2.编写抽象方法code（）
//3.编写一个子类Sub，继承抽象类Template，看看是否好用
abstract public class TestTemplate {
   public abstract  void job();//继承模板
       public void caleTime(){
       long start = System.currentTimeMillis();
       job();//动态绑定
       long end = System.currentTimeMillis();
       System.out.println("耗时=" + (end - start));

    }
}
public class AA extends TestTemplate{

    public void job(){
        long num = 0;

        for (long i = 1; i <=8000000 ; i++) {
            num += i;
        }
        //得到结束的时间

    }
}
public class BB extends TestTemplate{

    public void job(){
        long num = 0;

        for (long i = 1; i <=8000000 ; i++) {
            num *= i;
        }
        //得到结束的时间

    }
}
