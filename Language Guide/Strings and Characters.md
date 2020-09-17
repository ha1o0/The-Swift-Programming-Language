### 字符串和字符

字符串是字符的集合，比如"hello, world" 或者 "albatross"。 Swift字符串使用的是`String`类型。字符串的内容可以用多种方式访问到，包括作为字符的集合。

Swift的`String`和`Character`类型提供了一种方便快速的Unicode兼容的方式来处理代码中的文本数据。字符串创建和操作的语法是轻量级且易读性很强，它的语法跟C语言中的很相似。字符串的拼接就是把两个字符串用＋号连接起来，并且字符串可变性是通过在常量或变量之间进行选择来管理的，这一点和Swift中其他的值一样。你也可以使用字符串来把变量、常量、字面量或者表达式插入到更长的字符串中。这让创建一个自定义字符串来展示，存储和打印变得很容易。

尽管字符串语法很简单，但是Swift的string类型仍然是一种高效的现代化实现方式。每个字符串都是有独立编码的Unicode字符组成，并且提供了多种Unicode形式的字符访问的支持。

```
注意
Swift的字符串类型是与Foundation中的NSString类进行桥接的。Foundation也扩展了String类型，暴露了一些由NSString定义的方法。也就是说，如果你导入了Foundation，就可以在String类型上使用NSString提供的方法，而不需要类型转换。
更多有关在Foundation和Cocoa中使用String的信息，请查看[String和NSString的桥接]()章节。
```

#### 字符串字面量

你可以在代码中用预定义的String类型值来作为字符串字面量。一个字符串字面量就是一系列由双引号包裹的字符。
你可以用字符串字面量来作为一个常量或者变量的初始值：
```
let someString = "Some string literal value"
```

注意Swift会给`someString`这个常量自动推断为字符串类型，因为它是由一个字符串字面量初始化的。

#### 多行字符串字面量

如果你需要一个多行的字符串，那么可以使用多行字符串字面量————一个由三双引号包裹的一系列字符：
```
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

