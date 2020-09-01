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

Swift提供了8、16、32和64位的有符号和无符号整数。这些正数沿用了类似于C语言的命名习惯：8位无符号数为UInt8类型，32位有符号数为Int32类型。与Swift中的所有类型一样，这些整数类型的名称都是大写的。

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
On a 32-bit platform, Int is the same size as Int32.

On a 64-bit platform, Int is the same size as Int64.
```

除非你的确需要指明整形的大小，否则在你的代码始终使用`Int`代表整数即可。这有助于代码的统一和互操作。
即使在32位平台上，Int类型也可以存储任意一个在-2,147,483,648和2,147,483,647之间的整数，
这对很多整数范围而言已经足够大了。

###### UInt

Swift也提供了一种无符号整数类型`UInt`, 这个类型会拥有跟平台位数一样的大小：
```
On a 32-bit platform, UInt is the same size as UInt32.

On a 64-bit platform, UInt is the same size as UInt64.
```

```
注意
只有当你明确需要一个和当前平台位数相同的无符号整数类型时，才使用UInt。
否则，使用Int类型更合适，即使知道存储的值是非负数。对整数类型统一使用Int有助于代码的互操作性，
这可以避免在不同数字类型之间的相互转换，与整数的类型推断也相匹配，这里可以在[类型安全和类型推断]()中有描述。
```












