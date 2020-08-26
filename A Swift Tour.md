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
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
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
把optionalName变为nil，greeting会是什么结果?把这种情况加在else条件中试一下。
```

如果可选类型变量值是`nil`, 那么条件表达式就是`false`, 自然if代码块也不会执行。除此以外, 未解包的可选类型变量在`let`后赋给了一个常量，那这个常量就可以在条件为真的代码块中使用。

另外一种处理可选类型变量值的方法是用`??`提供一个默认值，如果值不存在时，就用默认的这个值替换。
```
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
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
尝试把default移除掉，会抛出什么错误?
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
```
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

```
尝试练习
移除参数day, 增加一个参数使得greet中包含今天的午餐。
```

默认情况下，函数中会使用形参的名称来作为参数的标签，你也可以在参数前自定义一个别名或者用`_`来忽略参数标签。
```
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

使用元组可以构造一个混合值，例如，一个函数可以利用元组返回多个值。元组的每个元素可以用名称或者数字访问到。

```
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Prints "120"
print(statistics.2)
// Prints "120"
```

函数是可以嵌套的。嵌套的函数可以访问在外部函数声明的变量。你可以使用嵌套函数来组织很长或者很复杂的函数内的代码。
```
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

函数也是一种类型。这意味着函数也可以返回另一个函数作为其返回值。
```
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

一个函数可以把另一个函数作为它的参数之一。
```
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

函数是闭包的一种特例。什么是闭包？闭包是一个可以延后调用的代码块。闭包内的代码可以访问闭包创建时所属作用域内的变量和函数，即使它是在另一个不同的作用域内执行的。前面的嵌套函数就是一个例子。同时你可以用`({})`包裹着代码写出一个匿名闭包。使用`in`来分割参数和返回体。

```
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

```
尝试练习
重写闭包来让所有奇数数字都返回0。
```

你可以有多种选择来实现更简洁的闭包。当一个闭包的类型已经明确，例如是一个`delegate`的回调，你可以忽略参数的类型或返回值类型或二者都忽略。单语句闭包隐式返回其唯一语句的值。
```
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Prints "[60, 57, 21, 36]"
```

你可以使用数字而不是名称来指代参数，这个方法尤其适用于很短的闭包。当一个闭包是一个函数的最后一个参数时，闭包可以直接尾随函数括号。当闭包是函数的唯一一个参数时，可以直接忽略掉函数括号(如下例子)。
```
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Prints "[20, 19, 12, 7]"
```

### 对象和类

`class`后加上类名就可以构造一个类。类的成员属性无论是常量还是变量在类中的声明方式都是一样的，同样，类中的方法和函数的声明也是一样的。
```
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

```
尝试练习
用let增加一个常量属性，同时增加另外一个带有参数的方法。
```

在类名后加上圆括号就可以创造一个类的实例。用`.`来访问类实例的成员属性和方法。
```
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

这个Shape类的写法缺少了一个重要的东西：当实例创建时执行的构造器。使用`init`定义一个构造器。
```
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

请注意这里是用`self`来将构造函数中的name参数和类的成员属性name来区分开的。当创建类的实例时，构造器的参数就和函数调用一样传入了构造函数。每个属性都需要赋值，无论是在变量声明(如numberOfSides)中还是构造函数(如name)中。

如果你需要在对象被回收之前做一些清理工作，你可以使用`deinit`来创造一个析构函数。

类名称后加上父类名称，二者中以`:`分隔，即可实现子类继承父类。类没有强制要求必须继承自某个标准的根类，所以你可以根据需求来继承或者不继承。

子类内的方法可以加`override`前缀来代表覆写父类的方法，如果不加并且覆写了，编译器会检测并报错。同样的，如果加了`override`却不是覆写父类方法，编译器也会检测出来并报错。

```
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

```
尝试练习
写出另外一个继承自NamedShape类的子类，名字叫Circle。它的构造函数的参数有两个：name和radius。同时在此类中实现area()和simpleDescription()方法。
```

除了存储的简单的属性，属性也可以有getter和setter。
```
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Prints "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Prints "3.3000000000000003"
```

在上面`perimeter`属性的setter中，新的属性值有一个默认的名称`newValue`，当然，你也可以在`set`后加上圆括号，并在其中显示给新值一个自定义的变量名称。

请注意`EquilateralTriangle`类的构造器中执行了三步：
1. 给自己类中声明的变量(sideLength)赋值。
2. 调用父类的构造函数。
3. 改变父类中定义的属性(numberOfSides)的值。任何需要用到方法、getter和setter的构造工作都可以放在这里进行。

如果你不需要计算属性值，但是需要在属性值改变前后执行一些代码，那么使用`willSet`和`didSet`可以实现。这些代码会在构造器之外的当属性值改变的任意时刻执行。例如下面的类中：三角形的边长和四边形的边长会始终保持相等。
```
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// Prints "10.0"
print(triangleAndSquare.triangle.sideLength)
// Prints "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Prints "50.0"
```

当用到可选类型时，你可以在方法、属性和取下标等操作之前加`?`。如果`?`前面的变量值是`nil`, `?`后面的所有操作都会被忽略，并且整个表达式的结果就是`nil`。否则，可选类型就是未解包的，那么`?`后的所有操作都会基于未解包的值进行。在以下例子中，两个表达式的值都是可选类型。
```
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```

### 枚举和结构体

使用`enum`可以创建枚举类型。就像类和其他的命名类型一样，枚举内也可以有相关的方法。
```
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

```
尝试练习
写一个方法来通过比较rawValue来比较两个Rank的值。
```

默认情况下，Swift会从零开始逐个加一来给枚举元素赋原生值，但是你也可以通过显示给出特定的值来改变这一默认行为。
在上面这个例子中，`Ace`被显示给出了它的原生值为1，剩下元素的原生值会依次按顺序加一。枚举的原生值的类型可以是字符串或者浮点数。
使用`rawValue`属性可以访问枚举元素的原生值。

使用`init?(rawValue:)`构造器可以根据一个原生值来创建出对应的枚举实例。如果原生值可以从枚举中匹配到，那么就返回该枚举实例，否则返回`nil`。

```
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

枚举的值就是一个真实的值，它不是原生值的另一种写法。事实上，在某些原生值没有意义的情况下，完全可以不给枚举提供原生值。
```
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```


```
尝试练习
给上面的Suit增加一个color()方法，当spades和clubs时返回"black", 另外两种情况时，返回"red"
```

请注意上面例子中对Suit中hearts的两种代指写法：当把它赋值给常量`hearts`时，`Suit.hearts`是用全写去代指的，因为这个常量没有指明自己的类型。但是在枚举内部的`switch`中，枚举元素是用缩写(`.heart`)来代指的，因为此时`self`已经知道类型就是`Suit`了。所以在任何知道变量类型的情况下都可以用枚举的缩写。

如果一个枚举有原生值，那些值在声明时就被定义好，那意味着一个指定的枚举实例都有同样的原生值。然而，对于枚举元素而言，另外一个赋值的选择是当你实例化枚举时，它的值是可以随实例不同而不同的。你可以将关联的值视为与枚举实例的存储属性类似的行为。考虑这个例子，我们需要从服务端请求获取日出和日落的时间，服务端要么返回请求所需要的信息，要么返回一个请求错误描述。
```
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
// Prints "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```

```
尝试练习
给ServerResponse和switch方法增加第三种情况。
```

请注意日出和日落时间是如何从ServerResponse值中提取出来的，并switch中匹配值的一部分。

使用`struct`可以创建一个结构体。结构体支持类中的很多行为特性，包括方法和构造器。结构体和类之间最大的区别之一是当在代码中传递时，结构体总是拷贝副本传递而类是传递实例的引用。


```
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

```
尝试练习
写一个方法，返回值是一个数组，数组中包含一整副牌，每张牌都包含等级和花色。
```


### 协议和扩展

使用`Protocol`可以声明一个协议。
```
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}
```

类，枚举和结构体都可以使用协议。
```
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

```
尝试练习
给ExampleProtocol增加另外一个要求。那么你应该怎么做才能让SimpleClass和SimpleStructure都仍然符合该协议？
```

请注意SimpleStructure声明中的`mutating`关键字的使用，它是用来修饰一个可以改变当前结构体的方法的。SimpleClass中的方法就不需要这个关键字，因为类中的方法总是被允许修改该类。

使用`extension`可以给一个已经存在的类型增加功能，比如新的方法和可计算属性。可以使用扩展将协议一致性添加到其他地方声明的类型，甚至可以添加到从库或框架导入的类型。
```
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
// Prints "The number 7"
```

```
尝试练习
给Double类型写一个扩展来增加一个绝对值属性。
```

可以像使用任何其他命名类型一样使用协议名。例如，可以创建一个不同类型的对象组成的集合，但所有对象都可以遵循同一个协议。处理类型为协议类型的值时，协议定义之外的方法不可用。
```
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// Prints "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Uncomment to see the error
```

即使变量protocolValue有一个SimpleClass的运行时类型，编译器仍然会把它当做给出的ExampleProtocol类型来处理。这就意味着不能访问除了在它遵循的协议内定义的方法和变量，即使它们在类中实现了。


### 错误处理

可以使用任何遵循了`Error`协议的类型来表示错误。
```
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

使用`throw`来抛出错误，使用`throws`来标记方法代表方法可以抛出错误。如果在一个方法中抛出了错误，方法会立即返回，并且调用该方法的代码会处理抛出的错误。
```
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

有几种方式来处理错误。一种是使用`do-catch`。在`do`代码块内，你可以在可能抛出错误的代码前面用`try`来修饰，在`catch`代码块内，错误会默认以`error`为名称，当然你也可以给一个不同的名称。
```
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// Prints "Job sent"
```

```
尝试练习
把printer的名字变成'Never Has Toner', 这样send方法就会抛出一个错误。
```

可以提供多个`catch`代码块来处理特定类型的错误。你可以像在`switch`中的`case`一样给error写一个匹配规则。
```
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// Prints "Job sent"
```

```
尝试练习
增加代码以便在do代码块内抛出一个错误。如果需要让错误被第一个catch代码块所捕获，你需要那种类型的错误？如果是第二或第三个catch捕获呢？
```


另外一中处理错误的方法是使用`try?`,它可以把结果转为一个可选类型。如果方法抛出一个错误，特定的错误会被忽略，并且结果是`nil`, 否则没有错误的话， 结果就是一个包含方法返回值的可选类型。
```
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

使用`defer`可以修饰一个代码块，这个代码块将在方法执行完其他代码后并且在返回值之前执行。并且即使方法抛出错误这些代码依然会执行。
可以使用defer将安装代码和清理代码一起编写，即使它们需要在不同的时间执行。
```
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }

    let result = fridgeContent.contains(food)
    return result
}
fridgeContains("banana")
print(fridgeIsOpen)
// Prints "false"
```

### 泛型
在尖括号内写一个名称可以创建泛型函数或类型。
```
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result = [Item]()
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```

你可以创建函数，方法，类，枚举和结构体的泛型。
```
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```

在方法体之前使用`where`关键字可以给泛型指明一个条件列表。例如，要求类型必须实现某个协议，或者要求两个类型必须一致，或者要求类必须继承自某个父类。
```
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

```
尝试练习
修改anyCommonElements方法，让它返回一个由任意两个序列共同元素组成的数组。
```

写法`<T: Equatable>`和写法`<T> ... where T: Equatable` 效果是一样的。
