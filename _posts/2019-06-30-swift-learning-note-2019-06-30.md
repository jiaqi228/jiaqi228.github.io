---
title: "Swift Learning Note"
categories:
  - Swift
  - Learning Note
tags:
  - Swift
  - Learning Note
---

## Function Closure

### Example
```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

names.sorted(by:)
```

### Writen in common way

```swift
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]

```

### Closure Expression Syntax
```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

### Inferring Type From Context
```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

### Implicit Returns from Single-Expression Closures
```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

### Shorthand Argument Names
```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

### Operator Methods
```swift
reversedNames = names.sorted(by: > )
```


抜粋:: Apple Inc. “The Swift Programming Language (Swift 5.0)”。 Apple Books  https://books.apple.com/jp/book/the-swift-programming-language-swift-5-0/id881256329