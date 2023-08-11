---
created: 2023-08-11T03:43:16.209Z
modified: 2023-08-11T06:00:36.189Z
---
## 内置函数

    println("$a") // 打印显示
    
    max(num1, num2) // 返回两个数中最大的数
    
    val //（value的简写）声明一个不可变的变量
    val a: Int = 1 //数据类型可以省略
    var // （variable的简写）用来声明一个可变的变量
    var a: Int = 1 // 数据类型可以省略
    // 永远优先使用val来声明一个变量，而当val没有办法满足需求时再使用var

## 函数

    fun main() {} // 入口函数
    
    fun methodName(param1: Int, param2: Int): Int {
        return 0
    } // 定义普通函数，没有返回值时，括号后的数据类型可省略
    
    fun largerNumber(num1: Int, num2: Int): Int = max(num1, num2) // 单语句函数语法糖，可进一步简化去掉括号后的数据类型

## 逻辑控制

### if-else if-else:

    if (name == "Jim") {
        value = "Jim"
    } else if (name = "Jack") {
        value = "Jack"
    } else {
        value = "Nobody"
    }
    
    val value = if (num1 > num2) {
        num1
    } else {
        num2
    } // if可以带有返回值，从而可以直接赋值，if语句每一个条件中最后一行代码就是返回值

    fun largerNumber(num1: Int, num2: Int): Int {
        return if (num1 > num2) {
            num1
        } else {
            num2
        }
    } // 在函数内可以精简直接返回if返回值
    fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) {
        num1
    } else {
        num2
    } // 可以进一步精简省略掉return
    fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) num1 else num2 // 再进一步精简成单行语句

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
    }

    fun getScore(name: String) = when (name) {
        "Tom" -> 86
        "Jim" -> 77
        "Jack" -> 95
        "Lily" -> 100
        else -> 0
    } // 与if语句一样也是可以带有返回值，从而可以直接赋值，单行执行逻辑可以省略掉{}
    
    fun checkNumber(num: Number) {
        when (num) {
            is Int -> println("number is Int")
            is Double -> println("number is Double")
            else -> println("number is support")
        }
    } // 允许进行类型匹配
    
    fun getScore(name: String) = when {
        name.startsWith("Tom") -> 86 // name开头为Tom的都返回86
        name == "Jim" -> 77
        name == "Jack" -> 95
        name == "Lily" -> 100
        else -> 0
    } // 可以不带参数，在结构体中判断

## 循环

### do-while:

     while (i <= 5) {
        println(i)
        i++
    }
    do {
        println(i)
        i++
    } while (i <= 5) // 和主流语言相差不多，不管满不满足条件do都会执行一次
    
    while (i <= 5) println(i++)
    do println(i++) while (i <= 5) // 单行执行逻辑可以省略掉{}

### for-in:

    val range = 0..10 // ..创建双端闭区间，11次 ~= [0,10]
    val range = 0 until 10 // until创建左闭右开单端闭区间，10次，最后的10不会被打印 ~= [0,10)
    val range = 0 until 10 step 2 // 执行循环都会在区间范围内递增2
    val range = 10 downTo 0 // 创建降序的区间 ~= [10,0]
    
    for (i in range) {
        println(i)
    }

## 对象数据类型

    Int // 整型
    Long // 长整型
    Short // 短整型
    Float // 单精度浮点型
    Double // 双精度浮点型
    Boolean // 布尔型
    Char // 字符型
    Byte // 字节型