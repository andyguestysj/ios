---
title: Swift Basics
permalink: /docs/swift-0/
---

SpriteKit is a games library/framework for the Swift programming language. Swift is an object oriented programming language so has a familiar structure but its syntax is different in a number of ways. This page covers the basics of the Swift syntax for a number of standard coding concepts. It doesn't go in to any depth, it assumes you know these concepts from Java (or another OOP language), it just shows the syntax.

### Variables

Variables in Swift are created using the `var` keyword. The `var` keyword tells the compiler the value is a variable and can be changed (it will tell you off if you create a `var` and don't later change it!). You don't need to specify the variable type but you can if you wish.  

|Type|Declaration|
|---|---|
|String|`var myString: String = "Hello"`|
|Integer|`var myNo: Int = 24`|
|Double|`var myDouble: Double = 3.14156`|
|Float|`var myFloat: Float = 2.19`|
|Boolean|`var myBoolean: Bool = true`|

Without specifying type it is simply `var myString = "hello"`  

If you want to create a constant then use `let` instead of `var`.  

`let pi = 3.1415`  

### Maths

Mathematical operations are as you would expect `=, -, /, *, +=, -=, ++, --`  

### Conditional Statements

#### if

```swift
var myTestNo = 12

if myTestNo < 30 {
  print("less than 30")
} else if myTestNo < 50 {
  print("greater than 29 but less than 50")
} else {
  print("fifty or more")
}
```

#### switch

```swift
var index = 3

switch index: {
  case 1: 
    print("1")
  case 2,5:
    print("2 or 5")
  default:
    print("default case")
}
```

### Arrays

```swift
var fruitList = ["apple", "orange", "banana", "pear"]

fruitList[0] = "watermelon"
print (fruitList[1])
```

### Loops

#### For In Loop

```swift
let employees = ["Andy", "Bob", "Chuck"]
for emp in employees {
  print(emp)
}
```

#### For Numeric

```swift
for index in 1..5 {
  print(index)
}

for index in 1..<8 {
  print(index)
}
```

#### While

```swift
var i = 1
while i < 5 {
  print(i)
  i += 1
}
```

### Functions

```swift
func hello() {
  print("hello")
}

hello()
```

Passing in parameters

```swift
func hello(name: String, age: Int) {
  print("hello ", name)
  print("you are ", age)
}

hello(name: "Andy", age: 21)
```

Returning values

```swift
func hello(name: String, age: Int) -> String {
  print("hello ", name)
  print("you are ", age)
  return "Aye Right"
}

let response = hello(name: "Andy", age: 21)
```
