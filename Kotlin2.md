---
title: Kotlin教程2---类和对象
date: 2018-01-28 14:29:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
1、类  
关键字也是class，和java不同的是它的构造函数直接在类声明时就声明了，小括号中就是构造函数的参数列表
```kotlin
class Person constructor(firstName: String) {} //当主构造器没有注解或可见性修饰时可以省略关键字constructor
```
2、初始化代码块  
由于没有像java那样显式个构造方法，所以初始化操作就在init方法中进行
```kotlin
class Person{
	init{
		print("在这里做一些初始化操作")
	}
}
```
3、构造函数  
类默认拥有一个无参构造，如果有了其他的构造，那么默认的就没了。  
次构造器：
```kotlin
class Person(name:String){
	constructor(name:String,age:Int):this(name){}
}
```
次构造器要委托（继承）主构造器 **:this(arg)**  
如果使用父类的构造器就用super代替this  
super\<Parent>//代表具体的某个父类，当有多个父类时可以来区分不同的父类,如：
```kotlin
class A:B,C{
	super<B>.name = "B的"
	super<C>.name = "C的"
}
```
4、可见性  
默认就是是public可见的，peivate是不可见的

5、属性  
属性的可见性、默认setter、getter方法这是和scala一样的  
不同点：成员属性在scala中可以先声明后初始化。而在kotlin中必须声明并初始化  
自定义setter、getter方法不同。如：
```kotlin
class Person(){
    var name:String = "张三"  //此处就是为幕后字段field赋值
    get() = field  
    set(value){ field = value} 

    var isEmpty:Boolean = false  //成员变量必须要初始化，不管用没用到field
    get()=xxxx
    val isEmpty:Boolean  //成员常量没有用到field就不需要初始化
    get()=true
    val isEmpty:Boolean = false  //成员常量用到field就要初始化
    get()=field
}
```
类的可见属性默认是有getset方法的。如果我们自己不满足系统提供给我们的setget方法时，我们就可以自己去重写。标准格式如上，其中有一个幕后字段field。  
它就代表该属性的原始值，可以理解成堆中的值。还可以在setget方法前加private进行私有化
如果是常量val，就不能有set方法

6、编译期常量  
在java中就是一个类的静态常量public static final  xxx  
在kotlin中就是const val xxx  
- 注意：在kotlin中的编译期常量必须满足
    - 位于顶层   或者  是 object 的一个成员   //顶层的意思就是在类的外部
    - 用 String 或原生类型 值初始化
    - 没有自定义 getter

如：创建一个文件Constant.kt
```kotlin
const val version = 1
object Constant{
	const val versionName="1.0.0"  //这个可以不写const
}
```
在其他文件中访问
```kotlin
print（version）
//或
print（Constant.varsionName）
```

7、继承  
在java中类默认是可以被继承的，不允许被继承就用fina来修饰。但是在kotlin中刚好相反，类默认是不被继承的，也就是说是默认就额比final修饰的，要想可以被继承，就用open修饰类的继承是继承父类的主构造器，而不是类名。

8、重写（覆盖）  
**override**关键字来重载变量或方法的。当然，变量和方法默认也是**final**的，不能被重写的，所以要想被重写就必须要用open来修饰才能被子类重写。  
一个val可以被覆盖成var，因为val只有getter，覆盖成var就是加一个setter的事，但是反之就不行
重写父类的属性既可以在子类的构造器参数中override，也可以在类中去override，只要属性是open的
operator关键字用来重载操作符和运算符的。  
如：重解构中的**componentN**方法就需要这个关键字修饰  
属性委托中的代理对象的setValue和getValue方法也需要这个关键字

9、抽象类  
抽象类可以被继承，不用open修饰。而类中的属性还是要open修饰后才能重写的

10、接口interface  
和scala一样接口中的方法可以实现也可以不实现
属性可以写getset方法，但是不能调用field幕后字段，因为压根没有幕后字段。也不能初始化赋值
所有的属性和方法可以直接override
实现接口同样用冒号“：”。多实现有逗号隔开

11、可见性  
public默认的、protected、private、internal这个是只在同一个moudel下可见

12、扩展  
```kotlin
class Man(val name:String){}
object Test{
val man = Man("张三")
	man.fly() //Man中没有fly这个方法，那么我们就对Man进行扩展
}
fun Man.fly(){//扩展Man类。添加一个fly方法
	println(this.name+"can fly")  //此处this代表的就是被扩展类的对象。打印就是张三can fly
}
```

类的扩展是静态解析，并没有真正的在类中添加成员，所以调用的时候根据形参来决定调用对象如：
```kotlin
open class A
class B:A{
	fun A.haha()="a"
	fun B.haha()="b"
	fun show(a:A){
	print(a.haha()) //这里决定调谁的方法
}
show(A()) //打印是a
show(B()) //打印的还是a，因为有形参来决定了
```
如果原类中已有某方法，那么再扩展就没有用，当然不同参数就有用

扩展属性
和扩展方法一样，把fun换成var或val即可。注意，由于扩展并未将成员插入类中，所以不能访问幕后字段，所以也不能有初始化器
```kotlin
class B 
class A{
    fun B.haha(){
        toString()  //B的tostring
        this@A.toString()  //A的tostring
    }
}
```
13、数据类  
可以理解成java中的bean类来使用。在类之前加data来修饰  
主构造函数需要至少有一个参数；  
主构造函数的所有参数需要标记为 val 或 var；  
数据类不能是抽象、开放、密封或者内部的；  
会创建copy方法，可以传某个具体参数，只改变该参数对应的属性，其他属性不变，复制出一个对象如：
```kotlin
data class A(val name:String,val age:Int)
val a = A(age = 1,name = "张三")
        println(a.name+":"+a.age)  //张三：1
        val copy = a.copy(age = 12)
        println(copy.name+":"+copy.age)  //张三：12
//还会创建componentN()方法来解构类,按照类中变量的声明顺序来解构
val name = a.component1()
val age = a.component2()
//还有toString方法和hashCode和equals方法都已经重写好了
```
14、密封类  
该类的子类是有限的。用sealed 关键字来修饰class

15、枚举  
该类的成员时有限的。用enum 来修饰class
```kotlin
enum class Season{ SPRING,SUMMER,AUTUMN,WINTER}
```
16、对象表达式  
完全可以理解成java中的匿名内部类，只是要用object来接受  
```kotlin
button.setOnClickListener(object:ClickLisener()，otherClass{
    override fun onClick(view:View){
        //todo
    }
})
```
还有厉害的地方，他可以继续继承或实现其他接口（用逗号隔开再继承其他类otherClass），这是java中的匿名内部类所达不到的

17、单例对象、静态对象  
用object来声明的类就是单例对象、静态对象，直接调用里面的变量和方法。用类名点属性名和方法名

18、伴生对象  
这个伴生对象和scala的伴生对象写法有区别  
```kotlin
class MyClass {
    companion object objName{
        fun create(): MyClass = MyClass()
    }
}
```
伴生对象要写在类中，要用companion和object两个关键字  
伴生对象名可以省略  
获取该伴生对象val x = MyClass.Companion ，要大写  
使用伴生对象中的方法可以用x来调也可以用MyClass来调  

19、委托属性  
属性委托和类委托的思想是一致的，类的委托是让代理类为委托类做事，同样这里是代理属性替委托属性做事，其实就是代理属性的set和get方法替委托属性的set和get方法做事。  
```kotlin
class Man{
    var name:String by People()
}

class People{
    var name:String="男人"//这个自己定义一个，我不知道是不是这么用，反正能表达出意思
    operator fun getValue(man: Man, property: KProperty<*>): String {
        return name
    }
    operator fun setValue(man: Man, property: KProperty<*>, s: String) {
        name = s
    }
}

fun main(args: Array<String>) {
    val man = Man()
    println(man.name)//打印男人
    man.name = "张三"
    println(man.name)//打印张三
}
```
就是调用man的get方法走的是people的getValue方法，调用man的set方法走的是people的setValue方法。完全呗people代理了man的name属性

20、标准委托  
- 懒加载lazy
```kotlin
val lazyValue: String by lazy {
    "Hello"
}
fun main(args: Array<String>) {
    println(lazyValue)//lazyValue原本是没有值的，只有在真正使用的地方才会为其初始化，这就是懒加载。也是一种属性委托
}
```
- 监听、判断  
```kotlin
class Person{
    var name:String by Delegates.observable("张三",{property,oldValue,newValue-> println(newValue)})//张三是初始值，当重新赋值时会触发lambda表达式，先赋值后触发，值已经改变了。
    var age:Int by Delegates.vetoable(1,{p,old,new->new >0}) //当重新赋值时会先判断，如果lambda表达式为true，才会将新值赋进去，否则就是初始值1
}
fun main(args:Array<String>){
val p = Person()
p.name = "李四"//重新赋值
p.age=18
}
```
- 非空初始化  
```kotlin
var tv:TextView by Delegates.notNull<TextView>()
```
作为全局变量要先初始化，但我们还不知道该为他初始化为何值，但又不想让他先为空，因为那样后面操作时都要非空判断，所以就先用这种委托初始化，当真正赋值的地方才为其赋值，如还没真正赋值就调用，就会报异常。类似与空指针
- 从map中映射  
```kotlin
class Configuration(map:	Map<String,	Any?>)	{
    val	width:	Int	by	map
    val	height:	Int	by	map
    val	dp:	Int	by	map
    val	deviceName:	String	by	map
}
```
可以把map中的全部值映射成一个对象

21、自定义委托  
```kotlin
class MyDalegate {
    operator fun getValue(student: Student, property: KProperty<*>): String {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

    operator fun setValue(student: Student, property: KProperty<*>, s: String) {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

}

class MyDelegate2 : ReadWriteProperty<Any,Int> {
    override fun getValue(thisRef: Any, property: KProperty<*>): Int {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

    override fun setValue(thisRef: Any, property: KProperty<*>, value: Int) {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }
}

class MyDelegate3 :ReadOnlyProperty<Any,String> {
    override fun getValue(thisRef: Any, property: KProperty<*>): String {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }
}
```

























































































