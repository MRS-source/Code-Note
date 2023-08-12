---
created: 2023-08-11T03:43:16.209Z
modified: 2023-08-12T15:56:07.861Z
---
## 内置函数

    println("Hello, World!") // 打印显示
    
    val //（value的简写）声明一个不可变的变量
    val a: Int = 1 //数据类型可以省略
    var // （variable的简写）用来声明一个可变的变量
    var a: Int = 1 // 数据类型可以省略
    // 永远优先使用val来声明一个变量，而当val没有办法满足需求时再使用var
    
    listOf("name1", "name2", "name3") // 创建一个不可变的List集合
    mutableListOf("name1", "name2", "name3") // 创建一个可变的List集合
    setOf("name1", "name2", "name3") // 创建一个不可变的不重复Set集合
    mutableSetOf("name1", "name2", "name3") // 创建一个可变的不重复Set集合
    mapOf("name1" to 1, "name2" to 2, "name3" to 3) // 创建一个不可变的Map集合
    mutableMapOf("name1" to 1, "name2" to 2, "name3" to 3) // 创建一个可变的Map集合
    
    let {} // 配合?.操作符来进行辅助判空处理

## 对象数据类型表

    Int // 整型
    Long // 长整型
    Short // 短整型
    Float // 单精度浮点型
    Double // 双精度浮点型
    Boolean // 布尔型
    Char // 字符型
    Byte // 字节型

## 函数

    fun main() {} // 入口函数
    
    fun methodName(param1: Int, param2: Int): Int {
        return 0
    } // 普通的函数，没有返回值时，括号后的数据类型可省略
    
    fun methodName(param1: Int, param2: String = "Jim") {} // 设定参数默认值
    methodName(19) // 使用中不给第二参数传值则使用默认值
    fun methodName(param1: Int = 19, param2: String) {} // 设定第一参数默认值
    methodName(param2 = "Jim") // 使用键值对给第二参数传值
    
    fun largerNumber(num1: Int, num2: Int): Int = max(num1, num2) // 单语句函数语法糖，省略掉函数的花括号，可进一步简化去掉括号后的数据类型

### 函数可见性修饰符表

    public 所有类可见（默认）
    private 当前类可见
    protected 当前类、子类可见
    internal 同一模块中的类可见

## 逻辑控制

### if-else if-else:

    if (name == "Jim") {
        value = "Jim"
    } else if (name = "Jack") {
        value = "Jack"
    } else {
        value = "Nobody"
    } // 普通的if
    
    val value = if (num1 > num2) {
        num1
    } else {
        num2
    } // if可以带有返回值，从而直接赋值，语句每一个条件中最后一行代码就是返回值
    
    fun largerNumber(num1: Int, num2: Int): Int {
        return if (num1 > num2) {
            num1
        } else {
            num2
        }
    } // 在函数内可以简化成直接返回if的返回值
    fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) {
        num1
    } else {
        num2
    } // 省略掉括号后的数据类型、函数的花括号、return
    fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) num1 else num2 // 再进一步简化成单行语句

### when:

    when (name) {
        "Jim" -> {
            value = "Jim"
        }
        "Jack" -> {
            value = "Jack"
        }
        else -> {
            value = "Nobody"
        }
    } // 普通的when
    
    fun getScore(name: String) = when (name) {
        "Tom" -> 86
        "Jim" -> 77
        "Jack" -> 95
        "Lily" -> 100
        else -> 0
    } // 和if语句一样也是可以带有返回值，从而直接赋值，单行执行逻辑可以省略掉函数的花括号
    
    fun checkNumber(num: Number) {
        when (num) {
            is Int -> println("number is Int")
            is Double -> println("number is Double")
            else -> println("number is support")
        }
    } // 进行类型匹配
    
    fun getScore(name: String) = when {
        name.startsWith("Tom") -> 86 // name开头为Tom的都返回86
        name == "Jim" -> 77
        name == "Jack" -> 95
        name == "Lily" -> 100
        else -> 0
    } // 不带参数，在结构体中判断

## 循环

### do-while:

    while (i <= 5) {
        println(i)
        i++
    } // 普通的while
    
    do {
        println(i)
        i++
    } while (i <= 5) // 不管满不满足条件do都会执行一次
    
    while (i <= 5) println(i++)
    do println(i++) while (i <= 5) // 单行执行逻辑可以省略掉花括号

### for-in:

    val range = 0..10 // ..创建双端闭区间，11次 ~= [0,10]
    val range = 0 until 10 // until创建左闭右开单端闭区间，10次，最后的10不会被打印 ~= [0,10)
    val range = 0 until 10 step 2 // 执行循环都会在区间范围内递增2
    val range = 10 downTo 0 // 创建降序的区间 ~= [10,0]
    
    for (i in range) {
        println(i)
    } // 普通的for-in

## 类与对象

    class Person {
        var name = ""
        var age = 0
        
        fun eat() {
            println("$name is eating. He is $age years old.")
        }
    } // 使用class定义名为Person的类，她有一个名为eat的函数
    
    val p = Person() // 实例化
    p.name = "Jack"
    p.age = 19
    p.eat() // 简单使用
    
    open class Person {} // 默认类不可被继承，使用open class让该类可以被继承
    class Student : Person() {
        var sno = ""
        var grade = 0
    } // 使用:类名来继承某个类
    
    class Student(val sno: String, val grade: Int) : Person() {}
    val student = Student("a123", 5)
    // 两种构造函数：主构造函数和次构造函数。每个类默认都会有一个不带参数的主构造函数，也可以显式地给它指明参数，主构造函数的特点是没有函数体，直接定义在类名的后面
    
    class Student(val sno: String, val grade: Int) : Person() {
        init {
            println("sno is $sno")
            println("grade is $grade")
        }
    } // 所有主构造函数中的逻辑都可以写在init结构体里面，很少使用
    
    open Person(val name: String, val age: Int) {}
    class Student(val sno: String, val grade: Int, name: String, age: Int) : Person(name, age) {}
    // Student类的主构造函数中加上name和age这两个参数，再将这两个参数传给Person类的构造函数，name和age不能再将它们声明成val，因为在主构造函数中声明成val或者var的参数将自动成为该类的字段，这就会导致和父类中同名的name和age字段造成冲突，不用加任何关键字，让它的作用域仅限定在主构造函数当中即可
    
    class Student(val sno: String, val grade: Int, name: String, age: Int) : Person(name, age) {
        constructor(name: String, age: Int) : this("", 0, name, age) {}
        constructor() : this("", 0) {}
    }
    val student1 = Student()
    val student2 = Student("Jack", 19)
    val student3 = Student("a123", 5, "Jack", 19)
    // 当一个类既有主构造函数又有次构造函数时，所有的次构造函数都必须调用主构造函数（包括间接调用），次构造函数是通过constructor关键字来定义
    class Student(val sno: String = "", val grade: Int = 0, name: String = "", age: Int = 0) : Person(name, age) {}
    // 使用给参数设定默认值简化替代次构造函数
    
    class Student : Person {
        constructor(name: String, age: Int) : super(name, age) {}
    }
    val student = Student("Jack", 19)
    // 类中只有次构造函数，没有主构造函数。Student类是没有主构造函数的，既然没有主构造函数，继承Person类的时候不需要再加上括号，由于没有主构造函数，次构造函数只能直接调用父类的构造函数，将this关键字换成了super关键字

### 接口

    interface Study {
        fun readBooks()
        fun doHomework() {
            println("do homework default implementation.")
        } // 该函数为默认实现
    } // 使用interface创建名为Study接口，定义了readBooks()待实现函数和doHomework()默认函数
    
    class Student(name: String, age: Int) : Person(name, age), Study {
        override fun readBooks() {
            println($name is reading.)
        }
        override fun doHomework() {
            println("$name is doing homework.")
        }
    } // 使用:接口名来继承某个接口，接口的后面不用加上括号，因为它没有构造函数可以去调用。继承后类必须实现接口的未实现的函数，使用override关键字来重写父类或者实现接口中的函数，doHomework()函数如果不复写则使用接口默认函数
    
    fun doStudy(study: Study) {
        study.readBooks()
        study.doHomework()
    }
     val student = Student("Jack", 19)
     doStudy(student)
     // 类的实例是可以传递给doStudy()函数，doStudy调用了Study接口的readBooks()和doHomework()函数，这种叫作面向接口编程，也可以称为多态

### 数据类

    data class Cellphone(val brand: String, val price: Double)
    // 使用data class创建数据类，当一个类中没有任何代码时，可以将尾部的{}省略
    
    val cellphone1 = Cellphone("Samsung", 1299.99)
    val cellphone2 = Cellphone("Samsung", 1299.99)
    println(cellphone1)
    println("cellphone1 equals cellphone2 " + (cellphone1 == cellphone2))
    // 数据类的使用

### 单例类

    object Singleton {
        fun singletonTest() {
            println("singletonTest is called.")
        }
    } // 使用object创建单例类，用于避免创建重复的对象，类在全局最多只能拥有一个实例
    
    Singleton.singletonTest() // 单例类的使用

## Lambda

### 表达式的语法结构

    {参数名1: 参数类型, 参数名2: 参数类型 -> 函数体}
    // 完整的语法结构定义。首先最外层是花括号，如果有参数传入到表达式中，还需要声明参数列表，参数列表的结尾使用->，表示参数列表的结束以及函数体的开始，函数体中可以编写任意行代码（不建议编写太长的代码），并且最后一行代码会自动作为表达式的返回值

### 集合

    val list1 = listOf("Apple", "Banana", "Orange", "Pear", "Grape") // 使用listOf()创建一个不可变的List集合
    val list2 = mutableListOf("Apple", "Banana", "Orange", "Pear", "Grape") // mutableListOf()创建一个可变的List集合
    list2.add("Watermelon") // 可变的List集合可以加入数据
    // 不可重复的Set集合使用setOf()和mutableSetOf()，使用上和List一样，但是Set集合中不可以存放重复元素，如果存放了多个相同的元素，只会保留其中一个
    
    for (fruit in list) {
        println(fruit)
    } // 使用for-in循环来遍历List集合
    
    val map1 = mapOf("Apple" to 1, "Banana" to 2, "Orange" to 3, "Pear" to 4, "Grape" to 5) // 使用mapOf()创建一个不可变的Map集合
    val map2 = mutableMapOf("Apple" to 1, "Banana" to 2, "Orange" to 3, "Pear" to 4, "Grape" to 5) // 使用mutableMapOf()创建一个可变的Map集合
    map2["Watermelon"] = 6 // 可变的Set集合可以加入数据
    
    for ((fruit, number) in map1) {
        println("fruit is $fruit, number is $number")
    } // 使用for-in循环来遍历Map集合

### 集合的函数式API

    list.maxBy // 接收一个Lambda类型的参数，并且会在遍历集合时将每次遍历的值作为参数传递给Lambda表达式。maxBy函数根据传入的条件遍历集合，从而找到该条件下的最大值
    list.map // 用于将集合中的每个元素都映射成一个另外的值，映射的规则在表达式中指定，最终生成一个新的集合
    list.filter // 用于过滤集合中的数据
    list.any // 用于判断集合中是否至少存在一个元素满足指定条件，返回true或者false
    list.all // 用于判断集合中是否所有元素都满足指定条件，返回true或者false
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
    val lambda = { fruit: String -> fruit.length }
    val maxLengthFruit = list.maxBy(lambda)
    // 找出字数最长的元素，啰嗦的表现
    val maxLengthFruit = list.maxBy({ fruit: String -> fruit.length }) // 删除不必要的变量
    val maxLengthFruit = list.maxBy() { fruit: String -> fruit.length } // Lambda参数是函数的最后一个参数时，可以将表达式移到函数括号的外面
    val maxLengthFruit = list.maxBy { fruit: String -> fruit.length } // Lambda参数是函数的唯一一个参数时，可以将函数的括号省略
    val maxLengthFruit = list.maxBy { fruit -> fruit.length } // 删除不必要的声明参数类型
    val maxLengthFruit = list.maxBy { it.length } // Lambda表达式的参数列表中只有一个参数时，不必声明参数名，可以使用it关键字来代替
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
    val newList = list.map { it.uppercase() }
    for (fruit in newList) {
        println(fruit)
    } // 将所有元素的单词转换成大写
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
    val newList = list.filter { it.length <= 5 }.map { it.uppercase() }
    for (fruit in newList) {
        println(fruit)
    } // 过滤掉大于5个字符的元素，并将其单词转换成大写，先调用filter再调用map效率会比先调用map再调用filter高得多
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
    val anyResult = list.any { it.length <= 5 }
    val allResult = list.all { it.length <= 5 }
    println("anyResult is $anyResult, allResult is $allResult")
    // 分别判断集合中是否至少存在一个元素满足指定条件和是否所有元素都满足指定条件

### 字符串内嵌表达式

    "hello, " + obj.name + ". nice to meet you!" // 拼接字符串可以优化成以下语句
    "hello, ${obj.name}. nice to meet you!" // 在字符串里嵌入${}这种语法结构的表达式，并在运行时使用表达式执行的结果替代这一部分内容
    "hello, $name. nice to meet you!" // 当表达式中仅有一个变量的时候，可以将两边的花括号省略

## 空指针检查

    // 默认的类型都为不可空。在类型名后增加?可使该类型可为空，例如在Int后面加上Int?表示可为空的整型、在String后面加上String?就表示可为空的字符串。在操作符前增加?可以简化判断处理，例如在.前面加上?.当对象不为空时正常调用相应的方法，当对象为空时则什么都不做、在:前面加上?:左边表达式的结果不为空就返回左边表达式的结果，否则就返回右边表达式的结果
    
    fun doStudy(study: Study?) {
        study.readBooks()
        study.doHomework()
    } // 可以传入空的null参数，但是会造成空指针异常，所以不被允许编译通过
    fun doStudy(study: Study?) {
        if (study != null) {
            study.readBooks()
            study.doHomework()
        }
    } // 可以传入空的null参数，并加了判断处理，所以允许编译通过（if无法判断全局变量，如果study是全局变量，仍旧会报错）
    fun doStudy(study: Study?) {
        study?.readBooks()
        study?.doHomework()
    } // 使用?.简化判断处理，当对象不为空时正常调用相应的方法，当对象为空时则什么都不做
    fun doStudy(study: Study?) {
        study?.let { stu ->
            stu.readBooks()
            stu.doHomework()
        }
    } // 结合使用?.操作符和let函数来对代码进行优化，let会将study对象本身作为参数传递到表达式中
    fun doStudy(study: Study?) {
        study?.let {
            it.readBooks()
            it.doHomework()
        }
    } // 简化表达式后的代码
    
    val c = if (a ! = null) {
        a
    } else {
        b
    } // 可以简化成以下语句
    val c = a ?: b // 左边表达式的结果不为空就返回左边表达式的结果，否则就返回右边表达式的结果
    
    fun getTextLength(text: String?): Int {
        if (text != null) {
            return text.length
        }
        return 0
    } // 可以简化成以下语句
    fun getTextLength(text: String?) = text?.length ?: 0 // 当text为空时，text?.length会返回一个null值，借助?:操作符返回0
    
    var content: String? = "hello"
    if (content != null) {
        printUpperCase()
    }
    fun printUpperCase() {
        val upperCase = content.uppercase()
        println(upperCase)
    } // 外部已经对content变量进行了非空检查，但认为printUpperCase这里存在空指针风险，所以不被允许编译通过
    fun printUpperCase() {
        val upperCase = content!!.uppercase()
        println(upperCase)
    } // 在.前面增加!!.使用!!非空断言工具，跳过非空检查，有风险的写法，允许编译通过

## 标准函数

### with:

        with(obj) {
        // 这里是obj的上下文
        "value" // with函数的返回值
        } // with函数接收两个参数：第一个参数可以是一个任意类型的对象，第二个参数是一个Lambda表达式。with函数会在Lambda表达式中提供第一个参数对象的上下文，并使用Lambda表达式中的最后一行代码作为返回值返回
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")
    val builder = StringBuilder()
    builder.append("Start eating fruits.\n")
    for (fruit in list) {
        builder.append(fruit).append("\n")
    }
    builder.append("Ate all fruits.")
    val result = builder.toString()
    println(result) // 原始代码，连续调用了多次builder对象
    
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")
    val result = with(StringBuilder()) {
        append("Start eating fruits.\n")
        for (fruit in list) {
            append(fruit).append("\n")
        }
        append("Ate all fruits.")
        toString()
    }
    println(result)
    // 给with函数的第一个参数传入了StringBuilder对象，接下来整个Lambda表达式的上下文就会是这个StringBuilder对象。于是在Lambda表达式中就不用再像刚才那样调用builder.append()和builder.toString()方法，而是可以直接调用append()和toString()方法。Lambda表达式的最后一行代码会作为with函数的返回值返回，最终将结果打印出来

### run:

    val result = obj.run {
        // 这里是obj的上下文
        "value" // run函数的返回值
    } // run函数的用法和使用场景和with函数是非常类似，稍微有一些语法改动。run函数通常不会直接调用，而是要在某个对象的基础上调用；其run函数只接收一个Lambda参数，并且会在Lambda表达式中提供调用对象的上下文。其他方面和with函数是一样的，包括也会使用Lambda表达式中的最后一行代码作为返回值返回
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")
    val result = StringBuilder().run {
        append("Start eating fruits.\n")
        for (fruit in list) {
            append(fruit).append("\n")
        }
        append("Ate all fruits.")
        toString()
    }
    println(result)
    // 只是将调用with函数并传入StringBuilder对象改成了调用StringBuilder对象的run方法

### apply:

    val result = obj.apply {
        // 这里是obj的上下文
    }
    // result == obj
    // apply函数和run函数也是极其类似，都要在某个对象上调用，并且只接收一个Lambda参数，也会在Lambda表达式中提供调用对象的上下文，但是apply函数无法指定返回值，而是会自动返回调用对象本身
    val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")
    val result = StringBuilder().apply {
        append("Start eating fruits.\n")
        for (fruit in list) {
            append(fruit).append("\n")
        }
        append("Ate all fruits.")
    }
    println(result.toString())
    // 由于apply函数无法指定返回值，只能返回调用对象本身，因此这里的result实际上是一个StringBuilder对象，所以在最后打印的时候还要再调用它的toString()方法才行

## 定义静态方法

    class Util {
        fun doAction1() {
            println("do action1")
        }
        companion object {
            fun doAction2() {
                println("do action2")
            }
            @JvmStatic
            fun doAction3() {
                println("do action3")
            }
        }
    } // 除了使用单例类还可以用companion object创建静态方法。companion object关键字实际上会在Util类的内部创建一个伴生类，而doAction2()方法就是定义在这个伴生类里面的实例方法，调用Util.doAction2()方法实际上就是调用了Util类中伴生对象的doAction2()方法。加上@JvmStatic注解（只能加在单例类或companion object中的方法上）可以使方法成为真正的静态方法，不管是在Kotlin中还是在Java中都可以使用Util.doAction3()的写法来调用
    
    // create file: Helper.kt
    fun doSomething() {
        println("do something")
    } // 顶层方法指的是那些没有定义在任何类中的方法。Kotlin编译器会将所有的顶层方法全部编译成静态方法，因此只要定义了一个顶层方法，那么它就一定是静态方法，所有的顶层方法都可以在任何位置被直接调用，不用管包名路径，也不用创建实例，直接键入doSomething()即可
    // 在Java代码中调用，会发现是找不到doSomething()这个方法的，因为Java中没有顶层方法这个概念，所有的方法必须定义在类中。刚才创建的Kotlin文件名叫作Helper.kt，Kotlin编译器会自动创建一个叫作HelperKt的Java类，doSomething()方法就是以静态方法的形式定义在HelperKt类里面，因此在Java中使用HelperKt.doSomething()的写法来调用就可以了