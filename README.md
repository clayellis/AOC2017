# 🎄 Advent of Code 👨‍💻
My solutions to Advent of Code 2017 http://adventofcode.com/2017

## Day 1

### Challenge 1
> Find the sum of all digits that match the next digit in the list. The list is circular, so the digit after the last digit is the first digit in the list.

```swift
func captcha(for input: String) -> Int {
    var sum = 0
    let digits = Array(input).flatMap { Int(String($0)) }
    for (index, digit) in digits.enumerated() {
        var lookupIndex = index + 1
        if lookupIndex > digits.count {
            lookupIndex = 0
        }

        if digit == digits[lookupIndex] {
            sum += digit
        }
    }
    return sum
}
```

### Challenge 2
> Now, instead of considering the next digit, it wants you to consider the digit halfway around the circular list. That is, if your list contains 10 items, only include a digit in your sum if the digit 10/2 = 5 steps forward matches it. Fortunately, your list has an even number of elements.

```swift
func captcha(for input: String) -> Int {
    var sum = 0
    let digits = Array(input).flatMap { Int(String($0)) }
    let offset = digits.count / 2
    for (index, digit) in digits.enumerated() {
        var lookupIndex = index + offset
        let distancePastEnd = lookupIndex - digits.count
        if distancePastEnd > 0 {
            lookupIndex = distancePastEnd - 1
        }

        if digit == digits[lookupIndex] {
            sum += digit
        }
    }
    return sum
}
```
