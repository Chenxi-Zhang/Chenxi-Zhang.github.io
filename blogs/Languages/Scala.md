# Scala

----
### 开始
* [在线运行](https://scalafiddle.io)
* [官方教程](https://docs.scala-lang.org/zh-cn/tour/tour-of-scala.html)
* 本地安装需要JDK。如果JDK>9，需要scala>2.12.4，否则会报错`java.lang.NoClassDefFoundError: javax/script/Compilable`。[reason](https://stackoverflow.com/questions/47697735/scala-throws-an-exception-when-i-try-to-launch-it-on-ubuntu)。

----
### 基础
* 储存脚本以`.scala`为扩展名。`def main(args: Array[String])`为main函数。
* 关于identifier，基本与Java一样。`$`在Scala中视作字母，不过应该避免使用。避免下划线`_`结尾。包含`-` `:` `?`等符号，Scala内部会转义为`$colon`，`$minus`，如果需要在Java中访问则需使用转义后的标识符。在\`\`之间可以使用任意合法标识符，包括keywords。
* 注释与Java类似。
* Scala面向行，语句可以用`;`或换行符结束。如果用`;`，一行可以多个语句。
* `package example.com`。package允许使用大括号，设定其scope。
* `import java.awt.Color` || `import java.awt._ // 引入所有成员`
```scala
import users._  // 导入包 users 中的所有成员
import users.User  // 导入类 User
import users.{User, UserPreferences}  // 仅导入选择的成员
import users.{UserPreferences => UPrefs}  // 导入类并且设置别名

import _root_._  // 项目的根目录
```
* Scala可以在任何地方import包。效果与变量作用域相同。

----
### Data Types
* `Byte, Short, Int, Long, Float, Double, Char, String, Boolean, Unit, Null, Nothing, Any, AnyRef`

----
### Variable
* 变量声明`var`，常量声明`val`。
* 声明语法：`(var || val) identifier: type [= initial value]`
* 如果有初始值，可以推断类型，所以类型可以省略。
* 赋值多个变量：`var a1, a2, a3 = 10`，三个变量均为Int值10。
* tuple声明：`val pa = (40, "Foo")`
* tuple访问：`pa._1`，使用下划线加数字语法，访问pa的第一个元素。
* tuple解构：`val (name, age) = (22, "Chenxi")`。注意与**多个变量赋值**区分。

----
### Access Modifier
* `private`成员。内部私有成员不能被外部访问。
* `protected`成员。只允许保护成员在定义了该成员的类的子类中访问。（java中同一包也能访问）。
* `public`成员。默认修饰符。任何地方都可以访问。
* 作用域保护：`private[x] || protected[x]`。由该修饰符修饰的成员可以被`x`访问，除此以外和`private || protected`一致。

----
### Operator
* Arithmetic operator: `+` `-` `*` `/` `%`
* Relational operator: `==` `!=` `>` `<` `>=` `<=`
* Logical operator: `&&` `||` `!`
* Bitwise operator: `~`按位取反，`&`按位与，`|`按位或，`^`按位异或。
* Assignment operator: `=` `+=` `-=` `*=` `/=` `%=` `<<=` `>>=` `&=` `!=` `^=`

----
### If...else...
* Almost same as Java
```scala
if(boolean expression 1) {
    // Block to execute if boolean expression 1 is true.
} else if(boolean expression 2) {
    // Boolean expression 1 is false and boolean expression 2 is true.
} else {
    // All expressions above are false. 
}
```
* If...else... statement has return value, so it can be used to assign a value to variable. `val schema = if (ssl) "https://" else "http://"` 

----
### Loop
* `while (condition) {statement;}`
* `do {statements;} while (condition)`
* `for ( var x <- Range ) { statements; }`
* `for ( var x <- List ) { statements; }`
* `for ( var x <- List if condition1; if condition2... ) { statements; }`
* `var retVal = for { var x <- List if condition1 } yield x`，返回值为可迭代的List，可以用在for (x <- List)中获得所有元素，也可以使用.foreach()。
* 多重循环for ( i <- 1 to 10 ; j <- i to 10) {statments;}
* `break` (if Scala>2.8)。没有`continue`。用法为：
```scala
import scala.util.control._
val loop = new Breaks;
loop.breakable{
    for (...) {
        ...
        loop.break // jump out loop
    }
}
```

----
### Function and Method
* Method是类的一部分，无法操作。Function是一个对象，可以进行赋值，传递。如果要操作Method，需要先将其转换为Function，比如`val func1 = method1(_)`。However，当在一个需要Function的地方传入一个合法的Method时，Scala自动转换成Function。
* 声明：`def functionName ([arg1: Type, ...]): [return Type]`。该方法隐式声明为抽象方法。
* 定义：
```scala
def functionName ([arg1: Type, ...]): [return Type] = {
    function body
    return [expr]
}
```
* call: `[instance.]functionName( args )`
* return: In Scala, if there is no `return` then the last expression is taken to be the return value. If...else statement may lead to different last expressions. 
* call-by-value style (x: Int), and call-by-name style (x: => Int). [Explanation](https://stackoverflow.com/questions/13337338/call-by-name-vs-call-by-value-in-scala-clarification-needed). 
* Scala allows the omission of parentheses on methods of arity-0 (no arguments).
```scala
scala> def a = { println("hello") }
a: Unit

scala> def b() = { println("hello") }
b: ()Unit

// It's illegal to call a() because of error: Unit does not take parameters
// But call b is the same as b(). 
```
* Scala允许**最后一个参数**为可变长度参数，syntax为在参数类型后面加`*`。可以用for循环遍历该参数，获取每一个传入的值。
* 默认参数值，类似Python，在参数类型后加`= (default value)`。无默认值的参数在前，有默认值的参数在后。Java调用时所有默认参数必填。
* 同样类似Python，传递参数时，可以指定函数参数名，此时不需要按顺序传递。
* Scala允许递归函数，允许高阶函数
* Method中可以定义局部Method。
* 偏应用函数（partial applied function）。对于多参数的函数，我们可以先赋值部分变量，剩余变量列表的每一个使用`_`来替代，表示还未传入。对函数使用`_`作为变量将会返回一个偏应用函数，该偏应用函数将会在传入剩余参数后运行函数主体部分。
```scala
val sum = (a: Int, b: Int, c: Int) => a + b + c
val f = sum(1, 2, _)
// f: Int => Int
f(3)
// return: 6
```
* 匿名函数。`([args list]) => { function body }`。如果每个参数在函数主体中都仅出现一次，则可以使用一个`_`代替一个变量，并且先后顺序一一对应。比如`(x: Int, y: Int) => x + 2 * y`等价于`(_: Int) + 2 * (_: Int)`。如果编译器可以推断出参数类型，则不用写`_`的类型。
* 闭包（closure）。与JavaScript，Python的概念相同。[解释](https://www.jianshu.com/p/8f24150fad2a)。
* Currying function: `def add(x: Int)(y: Int) = x + y`. 多参数列表，或者柯里化，类似于偏应用函数，允许先调用部分参数列表，返回一个函数，在其中储存已传入的参数，并在传入剩下所有参数列表后运行函数主体。隐式参数：implicit，应该使用多参数列表。

----
### Class
* 定义：`class` + identifier。
* 构造器：`class Point(var x: Int, var y: Int) {}`。可以添加默认值。不带`var || val`的参数是私有的。
* Getter/Setter：Getter可以设置成访问私有变量的方法，Setter方法的名字为getter方法名字后加`_=`，并在后面跟上参数和方法主体。

### Trait
* 定义：`trait` + identifier。类似于Java中的接口。其中可以使用泛型和抽象方法。
* 使用：`extends`关键字来扩展trait，然后使用`override`实现（改写）原方法。

### MixIn
* 使用：with混入类。一个类只能有一个父类，但却可以有多个混入。e.g.`class A extends B with C with D`

### 实例化
* 使用`new`关键字。

### 单例对象
* 定义：`object` + identifier。
* 创建：延迟创建，当它第一次被使用时。
* 伴生对象：一个单例对象和某个类共享一个名字，这个单例对象称为伴生对象，该类称为伴生类。伴生类和伴生对象可以相互访问私有变量。一般在伴生对象中定义静态变量或者静态方法，可以在伴生类中使用。

### Extractor提取器
* 定义：包含一个`unapply()`方法的单例对象object。`apply()`方法像构造函数，返回一个实例对象。反之，`unapply()`接受一个实例对象，返回其构造时的参数。
* 用法：
```scala
val variable = Singleton(args)
// variable is the return value of Singleton.apply(args)
val Singleton(args2) = variable
// args is the return value of Singleton.unapply(variable)
val args3 = Singleton.unapply(variable).get
// the same as above
```
* 要求：`unapply()`的返回值满足其中之一，1. Boolean类型。2. Option[T]。3. Option[(T1, T2, ...)]。

----
### Case classes
* 定义：`case class` + identifier + `([arg list])`。
* 参数：不用加修饰符，默认`public val`。e.g.`case class Book(id: Int, name: String)`
* 实例化：不使用new。
* 比较：case类使用值，而不是引用，来进行比较。
* 拷贝：`.copy()`

----
### 模式匹配
* Syntax：
```scala
variable match {
    case case1 => ret1
    case case2 => ret2
    case _ => otherReturn
}
```
* 常见用途：模式匹配与case class很适用。对多个继承自同一基类的case class，用case进行匹配。精确匹配子类后，运行其后主体。子类实例的成员变量，按顺序使用变量或者`_`传入函数主体。
* 允许使用`if`语句过滤，`case case1 if <expression> => ret1`，其中expression中可以使用case1中定义的变量。
* 仅匹配类型，在case中定义希望匹配类型的变量。`case a: Klass1 => ret1`
* `sealed`可以标记`class`和`trait`。要求其所有子类必须与之定义在相同文件里。

----
### 泛型
* 定义：使用`[]`来接受类型参数。惯例用`A`。

### 型变
* [Explanation](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)) && [Interesting explanation](https://stackoverflow.com/questions/2723397/what-is-pecs-producer-extends-consumer-super?rq=1)
* 协变（covariance）：注释`+A`，意味着对于`class List[+A]`，如果`A`是`B`的子类，那么`List[A]`是`List[B]`的子类。可类比Java`List <? extends A>`。
* 逆变（contravariance）：注释`-A`，与协变相反，`A`是`B`的子类，那么`Klass[B]`是`Klass[A]`的子类。可类比Java`Klass <? super A>`

### 类型边界
* 上界：`[A <: B]`，表示泛型A必须是B或者B的子类。类比Java`<A extends B>`。
* 下界：`[B >: A]`，表示泛型B必须是A或者A的超类。类比Java`<B super A>`。

----
### 内部类
* 类似于Java，关键在于inner class和外部实例绑定。当声明一个内部类类型的变量时，需要使用`outerInstance.InnerKlass`。从不同外部类实例所得到的内部类是不同的，比如`outer1.Inner`和`outer2.Inner`是两个不同的类，不能混用。
* 如果要混用，需要使用`Outer#Inner`的方式连接外部类和内部类，这种类型的内部类，在不同外部类实例的之间类型相同。

----
### 抽象类型
* trait和abstract class中可以定义**一个**抽象类型成员。该成员可以在子类中定义。
* 定义：`type T`。

### 复合类型
* `with`连接多个类型。

### 自类型
* 定义：`this: SomeTrait =>`

----
### 隐式参数
* 定义：`implicit identifier`
* Scala 在调用包含有隐式参数块的方法时，将首先查找可以直接访问的**隐式定义**和**隐式参数** (无前缀)。
* 然后，它在所有伴生对象中查找与隐式候选类型相关的有隐式标记的成员。

### 隐式转换
* 在以下情况发生：1. 类型不匹配。2. 调用的成员不存在。
* 自动搜索当前context的隐式转换，转换为匹配类型，或者具有调用成员的类型。
* 自定义隐式转换：`implicit def`

----
### 多态方法
* 定义：`def func[A](x: A) = {}`
* 使用：`func[Int](1) || func("str")`
* 类似于泛型，方法中也可以定义类型参数，并在参数列表中使用。
* 使用时往往不需要显示声明参数类型，Scala可以通过上下文或者参数类型推断出类型参数。

----
### 类型推断
* 返回值类型一致且明确的表达式可以推断类型。
* 建议明确类型的情况：
    - 递归可能无法正确推断类型。
    - 公开的API最好给出明确的类型。
    - 不希望定义过于具体的类型。e.g.`var obj = null`将会推断出`Null`类型，从而不能接受任何高于`Null`的类型。

----
### 运算符
* 单个参数的方法都可以用作*中缀运算符*。`10.+(1) // 10 + 1, return 11`

----
### 注解@annotation
* 定义：`@deprecated([args list])`
* 用法：该注解会影响其之后的第一个定义或声明。注解顺序不重要。
* 与Java区别在于，Scala注解中value()都可省略。

----
### 包对象
* 定义：文件`package.scala`源文件。
* 包对象可以定义任何内容，甚至可以继承类和特质。
* 每个包可以有一个包对象。在包对象中任何定义被认为是包自身成员。

----
### 注释
* Nil代表空List。
* `element :: List`将`::`左侧元素加入右侧列表中。