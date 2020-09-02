#### 常量和变量

常量和变量关联了一个名称（比如`maximumNumberOfLoginAttempts`或者`welcomeMessage`）和一个特定类型的值（比如数字10或者字符串"Hello"）。常量的值一旦设定好就不允许改变，但变量可以改变。

##### 声明常量和变量

常量和变量在使用前必须先声明。你可以用使用`let`关键字来声明常量，用`var`关键字来声明变量。这里有一个例子，展示了追踪一个用户尝试登陆次数场景中，常量和变量是如何使用的：
```
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

这段代码的意思是：
声明一个名为`maximumNumberOfLoginAttempts`的常量,给它赋值为10，然后，声明一个名为`currentLoginAttempt`的变量，并且给它一个初始值为0。
在这个例子中，允许尝试登陆的最大次数声明为常量，因为最大值不能改变。当前尝试登陆次数被声明为变量，因为这个值在每次登录尝试失败后再次尝试时一定会增加。

你可以在单行代码中声明多个常量或多个变量，中间用逗号分开即可：
```
var x = 0.0, y = 0.0, z = 0.0
```

```
注意
如果你代码中的一个值永远不变，那么就用let关键字把它声明为一个常量。只有当它需要改变时才使用变量。
```

##### 类型注释

当声明一个常量或者变量时，可以使用类型注释来指明此常量或者变量所存储的值的类型。在常量或者变量名称后加上冒号空格和类型即可完成类型注释。
下面这个例子给一个名叫`welcomeMessage`的变量提供了一个类型注释，表明了它可以存储字符串类型的值：
```
var welcomeMessage: String
```

冒号的意思是：……的类型，所以上面的代码意思是：“声明了一个名叫`welcomeMessage`的字符串类型变量。”
现在这个变量可以被赋予任何字符串值而不报错。
```
welcomeMessage = "Hello"
```

你可以在单行代码中定义多个相同类型的变量，中间用逗号分开，最后一个变量后面加上类型注释即可。
```
var red, green, blue: Double
```

```
注意
在实际使用中，很少有需要类型注释的情况。如果在常量或者变量被定义时就赋予它一个初始值，Swift可以根据这个值推断出它们的类型，这叫做“类型安全和类型推断”。在上面welcomeMessage的例子中，没有提供一个初始值，所以它的类型直接用类型注释指明，而不是由初始值推断出来。
```

##### 常量和变量命名

变量和常量的名称可以包含几乎任何字符，包括Unicode字符：
```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

变量和常量的名称不能包含空格，数学符号，箭头，私有Unicode标量，横线和制表符。同时既不能以数字开头，也不能在其中包含任何数字。
一旦已经声明了一个确定类型的变量或常量，就不能再用同样的名称再次声明，也不能改变它存储的值类型。同时，常量不能变成变量，变量也不能变成常量。
```
注意
如果你需要用Swift保留关键字作为变量或常量的名称，那么需要在关键字周围用"`"包裹即可。但是，除非你的确没有其他选择了，否则应该避免使用保留关键字作为变量名称。
```

你可以改变一个已定义的变量值，在这个例子中，`friendlyWelcome`变量值由"Hello"变为"Bonjour"。
```
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

与变量不同，常量一旦赋值就不能改变。试图改变常量的值会在代码编译时报错：
```
let languageName = "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.
```

##### 打印常量和变量

你可以使用`print(_:separator:terminator:)`函数来打印常量或者变量的当前值：
```
print(friendlyWelcome)
// Prints "Bonjour!"
```

这里的`print(_:separator:terminator:)`函数是一个打印一个或多个值到适当的输出处的全局函数。例如在Xcode中，这个函数会把输出结果打印到xCode的控制台中。separator和terminator参数有默认值，所以你可以在调用时忽略它。默认情况下，这个函数会在打印的行尾增加一个换行符。如果要打印出尾部没有换行符，那么需要传一个空字符串作为terminator参数值。例如，`print(someValue, terminator: "")`。如果要获取更多有关参数默认值的信息，请查看[默认参数值]()。

Swift使用字符串插值将常量或变量的名称作为占位符包含在较长的字符串中，并提示Swift将其替换为该常量或变量的当前值。将名称括在括号中，并在左括号前用反斜杠转义：
```
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!"
```

```
注意
你可以使用的字符串插值选项可以在[字符串插值]()中查看。
```

#### 注释

代码中的非执行文本会被注释掉作为笔记或者提醒。注释会被Swift编译器在编译时忽略。
Swift中的注释和C语言中的很类似，使用双斜杠开头来注释单行文本。
```
// This is a comment.
```

使用单斜杠和星号开头以及星号和单斜杠结尾来注释多行文本。
```
/* This is also a comment
but is written over multiple lines. */
```

与C语言中的多行注释不同，Swift中的多行注释允许在其他多行注释中嵌套。编写嵌套注释的方法是先写一个多行注释块，然后在第一个块中嵌入第二个多行注释。然后先关闭第二个块，然后关闭第一个块：
```
/* This is the start of the first multiline comment.
 /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```

嵌套注释使得你可以快速简单地注释掉大段代码，即使代码中已经包含有多行注释。

##### 分号

与其他语言不同，Swift不要求在每行代码最后加写分号，当然你愿意的话也可以加上。但是，当你在一行代码中写多个语句时，分号必须加上。
```
let cat = "🐱"; print(cat)
// Prints "🐱"
```

##### 整数

整数是没有分数部分的数字，例如42和-23。整数分为有符号数(正数，零和负数)和无符号数(正数和零)。

Swift提供了8、16、32和64位的有符号和无符号整数。这些正数沿用了类似于C语言的命名习惯：8位无符号数为UInt8类型，32位有符号数为Int32类型。与Swift中的所有类型一样，这些整数类型的名称都是大写开头的。

###### 整数范围

你可以用整数的`min`和`max`属性来获取每种整数类型所能表示的最小和最大值：
```
let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8
```

这些属性的值具有适当大小的数字类型（如上例中的UInt8），因此可以在表达式中与相同类型的其他值一起使用。

###### Int

在大部分情况下，你不需要在代码中指明你要使用的整数大小。Swift提供了额外的一个整数类型，`Int`， 这个类型会拥有跟平台位数一样的大小：
```
在32位平台上，Int和Int32占用同样空间大小。
在64位平台上，Int和Int64占用同样空间大小。
```

除非你的确需要指明整形的大小，否则在你的代码始终使用`Int`代表整数即可。这有助于代码的统一和互操作。
即使在32位平台上，Int类型也可以存储任意一个在-2,147,483,648和2,147,483,647之间的整数，
这对很多整数范围而言已经足够大了。

###### UInt

Swift也提供了一种无符号整数类型`UInt`, 这个类型会拥有跟平台位数一样的大小：
```
在32位平台上，UInt和UInt32占用同样空间大小。
在64位平台上，IUnt和UInt64占用同样空间大小。
```

```
注意
只有当你明确需要一个和当前平台位数相同的无符号整数类型时，才使用UInt。
否则，即使知道存储的值是非负数,使用Int类型也更合适。对整数类型统一使用Int有助于代码的互操作性，
这可以避免在不同数字类型之间的相互转换，与整数的类型推断也相匹配，这里可以在[类型安全和类型推断]()中有描述。
```

##### 浮点数

浮点数是有小数部分的数字，比如3.14159，0.1以及-273.15.
浮点数类型可以代表比整数范围更大的数字，并且可以存储比Int数字大得多或者小得多的数字。Swift提供了两种浮点数类型：
+ `Double`代表64位精度浮点数。
+ `Float`代表32位精度浮点数。

```
注意
Double类型拥有至少15位小数的精度，而Float是6位。实际使用当中，究竟哪种浮点数类型更合适取决于你的代码中数字值的性质和范围。
如果两种都可以，那么优先使用Double更好些。
```

#### 类型安全和类型推断

Swift是一种类型安全的语言。一种类型安全的语言会鼓励你明确代码中的值的类型。如果你的代码需要String类型，那么就不能错误地传递给他Int类型。
由于它的类型安全，Swift会在代码编译时进行类型检测，并且把类型的误使用标记成错误。这就可以让你在开发过程中尽可能早地发现并修正错误。

类型检查会在你使用不同类型变量时帮助你避免错误使用，但是，这不意味着你必须要每次都显式声明每个常量或者变量的类型。如果你没有给你所使用的值标明类型，Swift会使用类型推断推断出合适的类型。类型推断会使编译器在编译代码时，简单地根据你所提供的初始值来自动推断出特定表达式的值类型。

正是由于有了类型推断，相比于像C或者Objective-C之类的语言，Swift几乎很少要求对变量进行类型声明。常量和变量仍然是类型明确的，只不过大部分类型确定的工作都已经自动为你做好了。

类型推断尤其是在你声明了一个有初始值的常量或者变量时有用处。这个过程其实就是在声明常量或者变量时，给它一个字面值。（一个字面值就是源代码中直接出现的那个值，比如下面例子中的42和3.14159）。

例如，如果你新建了一个常量，但是没有指明它的类型，却给了它一个字面值42，Swift就会推断出你想要这个常量的类型是Int，因为你用了一个像整数一样的数字来初始化它：
```
let meaningOfLife = 42
// meaningOfLife is inferred to be of type Int
```

同样的，如果你没有给浮点数的字面值指明类型，Swift也会推断出你想创建一个Double类型：
```
let pi = 3.14159
// pi is inferred to be of type Double
```

对于浮点数的类型推断，Swift总是会选择Double而不是Float类型。
如果你在一个表达式里组合了整数和浮点数，那么根据上下文推断出来的还是Double类型：
```
let anotherPi = 3 + 0.14159
// anotherPi is also inferred to be of type Double
```

上面例子中，3的字面值类型没有明确，所以由于表达式中另一部分浮点数的出现，推断出输出Double类型是比较合适的。

##### 数值的字面值

整数的字面值可以写成：
+ 无前缀的十进制数字。
+ 以`0b`为前缀的二进制数字。
+ 以`0o`为前缀的八进制数字。
+ 以`0x`为前缀的十六进制数字。

下面所有的整数字面值的十进制值都是17：
```
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
```

浮点数的字面值可以是无前缀的十进制数，或者以`0x`为前缀的十六进制数。它们的小数点两边都必须有一个数字（或十六进制数）。十进制的浮点数可以有一个可选择的由大写或者小写e表示的指数。十六进制的浮点数必须要有一个由大写或者小写p表示的指数。
对于指数为exp的十进制数，值就是基数乘以10<sup>exp</sup>。

+ 1.25e2 等于 1.25 x 102, 或者 125.0.
+ 1.25e-2 等于 1.25 x 10-2, 或者 0.0125.

对于指数为exp的十六进制数，值就是基数乘以2<sup>exp</sup>。

+ 0xFp2 等于 15 x 22, 或者 60.0.
+ 0xFp-2 等于 15 x 2-2, 或者 3.75.

下面这些所有浮点数的字面值的十进制都是12.1875：
```
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

数字的字面值允许包含其他额外的格式来使其具有更好的可读性。无论是整数还是浮点数，都可以用额外的零进行填充，并且可以添加下划线来增强可读性。下面的字面值都不会因为格式化而改变：
```
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

##### 数字类型转换

对于所有通用的整数型常量或变量，即使明确它们是非负数，也要使用Int类型。在每个场景中都使用这个默认的整数类型就意味着你代码中的整数型常量和变量是可以直接互相操作的，并且这也和整数型字面值所推断出的类型相一致。

只有当手边的任务有明确的需要，比如来自外部资源数据的大小明确，出于性能考虑的内存使用或其他必要优化时，才会使用其他整数类型。
在这些情况下使用明确大小的类型有助于捕获任何意外的值溢出，并隐式记录所使用数据的性质。

###### 整型转换

整型常量或者变量所存储的值的范围是随着不同的数字类型而不同的。Int8类型的常量或变量所能存储的数字范围是-128到127，与此相对的UInt8的范围是0到255。
当数字不在整型大小范围内时，编译器就会报错：
```
let cannotBeNegative: UInt8 = -1
// UInt8 cannot store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 cannot store a number larger than its maximum value,
// and so this will also report an error
```

由于不同的数字类型所存储的值范围不同，你必须根据实际情况进行类型转换。这个方法可防止隐藏的转换错误，并有助于在代码中明确表示类型转换意图。
为了把一个指定数字类型转换为另外一个，你可以用已出现的值初始化一个目标类型的新数字。在下面的例子中，常量`twoThousand`是UInt16类型的，`one`是UInt8类型的。他们不能直接相加，因为他们不是同一个类型。相反，这个例子调用了`UInt16(one)`方法用原来的值初始化出一个UInt16类型的值，并以此来替代原有的值进行相加操作。
```
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

由于加号两边的值类型都是UInt16，相加操作才被允许。输出的结果`twoThousandAndOne`类型被推断为UInt16, 因为它是两个UInt16值的和。

SomeType（ofInitialValue）这种方法是以传递初始值作为参数来调用Swift的类型构造器的默认方法。在这个场景背后，UInt16有一个构造器方法，它允许接收一个UInt8的值，所以这个构造器就可以被用来从已出现的UInt8类型创建一个新的UInt16类型。但是这里你不能传递任何其他类型，这个类型必须是UInt16提供的构造器所接收的才行。扩展已出现的类型来使其提供接收新类型（包括自定义的类型）的构造器会在[扩展]()章节中介绍。

###### 整形和浮点型转换

整型和浮点型数字类型的转换必须显示标明：
```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
```
这里，常量`three`的值被用来创建一个同样值的Double类型，以此来保证加号两边具有同样的类型。没有这里的转换，加法是不被允许的。

浮点数转成整数也一定要显示标明。一个整数类型可以用一个Double或者Float类型的值来初始化：
```
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
```

浮点数用这种方法转换成整型总是会被舍去小数部分而变小，这就意味着，4.75变成4， -3.9变成-3。
```
注意
数字常量和变量的组合规则是随着数字字面值不同而不同的。字面值3可以直接和字面值0.14159相加，是因为数字字面值没有显式的类型。
只有在编译器对其求值时才推断出它们的类型。
```


#### 类型别名

类型别名定义了一个已出现类型的另外一个名字。你可以用`typealias`关键字来定义类型别名。
当你希望用一个上下文更合适的名字来代指一个类型时，类型别名是很有用的。例如在处理来自外部源的特定大小的数据时：
```
typealias AudioSample = UInt16
```

一旦定义好了类型别名，就可以在任何用到原来名字的地方使用这个别名：
```
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound is now 0
```

这里，`AudioSample`就被定义成了UInt16类型的别名。因为它是一个别名，所以调用`AudioSample.min`实际上就是调用的`UInt16.min`，这个值是0，被提供给变量`maxAmplitudeFound`作为其初始值。


#### 布尔值

Swift有一种基础的`Boolean`类型，叫做`Bool`。布尔值被称为逻辑值，因为他们只能是真或者假。Swift给布尔类型提供了两个常量，`true`和`false`:
```
let orangesAreOrange = true
let turnipsAreDelicious = false
```

`orangesAreOrange`和`turnipsAreDelicious`两个变量由于初始值是布尔型字面值，所以会被自动推断为Bool类型。就像前面我们提到的Double和Int类型一样，在创建变量或常量时，不必声明类型为Bool，给他们赋予true或者false的初始值即可。在用已知类型的值来初始化变量或者常量时，类型推断会帮助Swift代码变得简洁和易读。

布尔值在在使用像if语句一样的条件语句时会特别有用：
```
if turnipsAreDelicious {
    print("Mmm, tasty turnips!")
} else {
    print("Eww, turnips are horrible.")
}
// Prints "Eww, turnips are horrible.
```

像if语言一样的条件语句会在[控制流]()章节有更详细的介绍。

Swift的类型安全会防止非布尔值替代布尔值，下面这个例子就会抛出编译错误：
```
let i = 1
if i {
    // this example will not compile, and will report an error
}
```

但是，下面这个例子是有效的:
```
let i = 1
if i == 1 {
    // this example will compile successfully
}
```

`i == 1`比较的结果就是Bool类型，因此第二个例子会通过类型检查。像`i == 1`这种比较表达式在[基本操作符]()章节有介绍。

和Swift中其他的类型安全的例子一样，这种方法会避免意外错误的发生，并且可以确保一段特定的代码的意图清晰明确。

元组会把多个值组合到一起成为一个单一的混合值。一个元组中的值可以是任何类型，并且各个值不必是同一种类型。
在这个例子中，`(404, "Not Found")`就是一个面熟HTTP状态码的元组。一个HTTP状态码是当你请求网页数据时，由web服务端返回的特殊值。当你请求的网页不存在时，返回的状态码就是“404 Not Found”。
```
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```

这个`(404, "Not Found")`元组是把一个Int类型和一个String类型的值组合在一起，这两部分就是HTTP状态码的数字部分和人类可读的描述部分。
他可以被描述为“一个类型为`(Int, String)`”的元组。

你可以用任何排列组合的方式来创建一个元组，并且其中包含的任意不同的类型。比如这样`(Int, Int, Int)`或者这样`(String, Bool)`或者其他你需要的任何排列组合。

你可以从一个元组中解析出单个的变量或者常量，通常的做法如下：
```
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found
```

当你分解析元组时，如果你只需要元组中的一部分值，那么其余不需要的值可以使用下划线(_)来忽略其他部分值：
```
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404
```

还有一点，你可以使用从零开始的数字下标来访问元组中单一元素的值：
```
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found"
```

你还可以在元组定义时，给其中的每个元素命名：
```
let http200Status = (statusCode: 200, description: "OK")
```

如果你给每个元素都命名了，那么就可以用这些名字来访问这些元素的值：
```
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK"
```

元组在作为函数返回值时尤其有用。比如一个试图获取网页的函数可以返回一个`(Int, String)`类型的元组，来描述请求的成功或者失败。
相比于只返回一个单一类型的值，通过返回一个拥有两个不同类型不同值的元组，函数可以提供更多有关它的结果的有用信息。要获取更多相关信息，
可以参考[多返回值的函数]()章节。

```
注意
元组对把相关联的值简单组合在一起很有用。但它们不适用于创建复杂的数据结构。如果你的数据结构很可能更复杂，
那么把它定义成类或者结构体更合适。要获取更多相关信息，可以参考"结构体和类"章节。
```

#### 可选类型

当一个值可能不存在时你就可以使用可选类型了。可选类型代表了两种可能：要么有一个值，并且你可以对整个变量解包来访问这个值，要么值根本不存在。
```
注意
可选类型的概念在C或者Objective-C中是不存在的。Objective-C中最接近可选类型的就是本该返回一个对象的函数返回了nil，代表“无有效对象”。
然而，这也仅仅只局限于类，对结构体，C语言基本类型以及枚举类型是不存在返回nil这种情况的。
对这些类型来说，Objective-C的方法一律会返回一个特殊的值（比如NSNotFound）来代表值的不存在。
这个方法会假定函数的调用者知道有一个特殊值要测试，并记得要检查它。
Swift的可选类型允许你让任何类型的值都不存在，而不需要特殊的常量。
```

这里是一个可选类型如何被用来处理值不存在的例子。Swift的Int类型有一个构造器方法可以把String类型转换为Int类型。
然而，不是所有的字符串都能够转换成整数。字符串”123“可以被转换成数字123，但是字符串”Hello, World“不能。
下面这个例子就是用构造器方法试图把String类型转为Int类型：
```
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int
```

由于构造器方法也许会失败，所以它的返回结果是可选的Int类型，而不是Int类型。可选的Int类型写作`Int?`, 不是`Int`。
这个问号代表了它的值是可选的，意味着它肯能包含一些Int类型的值，也可能根本不包含任何值。
（但它不能包含任何其他的类型值，比如布尔值或者字符串值，它要么是一个Int值，要么什么值都没有。）