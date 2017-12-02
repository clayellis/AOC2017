# AOC2017
My solutions to Advent of Code 2017 http://adventofcode.com/2017

## Day 1

### Challenge 1
> Find the sum of all digits that match the next digit in the list. The list is circular, so the digit after the last digit is the first digit in the list.

```swift
func checksum(input: String) -> Int {
    var sum = 0
    let digits = Array(input).flatMap { Int(String($0)) }
    for (index, digit) in digits.enumerated() {
        guard index + 1 < digits.endIndex else {
            if digit == digits[0] { sum += digit }
            break
        }

        if digit == digits[index + 1], digits.count > 2 {
            sum += digit
        }
    }
    return sum
}
```
