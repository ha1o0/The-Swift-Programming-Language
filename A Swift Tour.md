## 一次Swift旅行


当我们学习一门新的语言时，按照传统第一个程序应该是打印出`Hello, world`，Swift可以只用一行来实现它：
```
print("Hello, world!")
// Prints "Hello, world!"
```

如果你曾经写过C或者Objective-C的代码，这个语法你一定很熟悉。但是在Swift这里，这行代码就是一个完整的程序，你不需要引入其他的像input/output或者字符串处理等单独的函数类库。同时，在全局作用域内写的代码就是程序的入口，所以也不需要一个`main()`函数。每行代码最后也不必加`;`。

本次练习将会展示如何完成多种多样的编程任务，从中会有足够的信息来告诉你如何开始编写Swift代码。如果你对一些代码无法理解，不要担心，本次练习中给出的每一个知识点都会在本书剩余部分进行详细的介绍。

```
备注
你可以在安装了Xcode的Mac或带有Swift Playground的iPad上以playground方式打开本节代码，
Playgrounds允许你编辑代码的同时即时显示运行结果。
[下载Playground](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.playground.zip)
```

### 简单的值类型
使用`let`来创建常量，使用`var`来创建变量。常量的值不需要在编译时就知道，但是你必须且只能给它赋一次值，也就是说，你可以用常量来给那些一次定义多处使用的变量赋值。
```
var myVariable = 42
myVariable = 50
let myConstant = 42
```

一个常量或者变量一定要和你想要赋给它的值是同一个类型。然而，你不必每次都显式地写出它的类型，编译器会根据你给的值自动推断出它的类型。在上面这个例子中，编译器会推断出`myVariable`这个变量是整型，因为它的初始化值是一个整数。

如果变量的初始化值不足以推断出它的类型（或者根本没有初始化的值），就需在变量后面显式指明类型，二者以`:`分开。
```
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

```
尝试练习
创建一个显式类型为`float`并且值为4的常量。
```

值绝对不会自动转换成其他的类型。如果你需要把一个类型的值转为其他不同的类型，那么就得显式生成其他类型的实例。
```
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

```
尝试练习
如果移除最后一行中转换为字符串的代码，会抛出什么错误？
```

还有一种更简单的方法来在字符串中插入其他的值。把变量写在括号中，并且在括号前加上斜杠`\`即可。例如：
```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit.
```

```
尝试练习
用`\()`在一个字符串中插入浮点数的算式，以及在一个打招呼的字符串中插入某人的名字。
```

用三双引号`"""`来生成多行字符串。删除每行引号开头的缩进，只要它与右引号的缩进相匹配。例如：
```
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

用中括号`[]`来创建数组和字典类型，并且可以通过中括号里的数组下标或者字典键来访问各个元素。最后一个元素后面允许增加逗号:
```
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

数组会在增加元素时自动扩容。
```
shoppingList.append("blue paint")
print(shoppingList)
```

用以下初始化语法来创建一个空数组或空字典：
```
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

如果类型可以被推断出来，你就可以用`[]`来创建一个空数组，以及用`[:]`来创建一个空字典。例如当需要为变量赋新值或者向函数内传参数时：
```
shoppingList = []
occupations = [:]
```

### 控制流
用`if`和`switch`来实现条件控制，用`for-in`，`while`和`repeat-while`来实现循环控制。条件语句或者循环变量两边的括号是可选的。但整体代码块的大括号时必须的。
```
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Prints "11"
```

对于if语句，条件必须是布尔表达式，也就是说形如`if score { ... }`的条件是错误的，分数变量没有与零进行比较。
当条件语句中的变量值可能不存在时，你可以同时使用`let`来辅助判断。这种变量就是可选类型变量，它要么拥有自己的值，要么就是`nil`。
我们可以在变量类型后加`?`来代表它是可选类型。

```
var optionalString: String? = "Hello"
print(optionalString == nil)
// Prints "false"

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

```
尝试练习
把`optionalName`变为`nil`，`greeting`会是什么结果?把这种情况加在`else`条件中试一下。
```

如果可选类型变量值是`nil`, 那么条件表达式就是`false`, 自然if代码块也不会执行。除此以外, 未解包的可选类型变量在`let`后赋给了一个常量，那这个常量就可以在条件为真的代码块中使用。

另外一种处理可选类型变量值的方法是用`??`提供一个默认值，如果值不存在时，就用默认的这个值替换。
```
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)
```

`Switch`支持任意类型数据和多种比较表达式，不仅限于整数和相等性的测试。
```
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
// Prints "Is it a spicy red pepper?"
```

```
尝试练习
尝试把`default`移除掉，会抛出什么错误?
```

请注意这里是如何用`let`来给常量赋值并将值用于表达式中进行case匹配。

执行完switch中的匹配到的case后，程序即退出switch，不会继续执行后续case，因此没有必要在每个case后增加`break`。

你可以使用`for-in`来进行字典键值的遍历，由于字典是无序的集合，所以键值会以自由的顺序进行遍历。
```
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Prints "25"
```

```
尝试练习
增加一个变量来记录哪种（Prime, Fibonacci, Square）数字是最大的, 也就是说最大的数字属于哪种类型。
```

用`while`来循环执行一段代码块，直到不符合循环条件即退出。循环的条件可以放在最后，这样可以确保循环至少运行一次。
```
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Prints "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Prints "128"
```

用`..<`来表示数字范围，区间为左闭右开，用`...`来表示左闭右闭的区间。

### 函数和闭包

用`func`来声明一个函数。用函数名加带有参数的圆括号来调用这个函数。用`->`来分割函数参数和函数返回值类型。