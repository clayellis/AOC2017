# 🎄 Advent of Code 👨‍💻
My solutions to [Advent of Code 2017](http://adventofcode.com/2017)

## [Day 1](http://adventofcode.com/2017/day/1)

### Challenge 1
> Find the sum of all digits that match the next digit in the list. The list is circular, so the digit after the last digit is the first digit in the list.

```
Example Input:
91212129

Excpected Output:
9
```

```swift
func captcha(for input: String) -> Int {
    var sum = 0
    let digits = Array(input).flatMap { Int(String($0)) }
    for (index, digit) in digits.enumerated() {
        var lookupIndex = index + 1
        if lookupIndex > digits.endIndex - 1 {
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

```
Example Input:
12131415

Excpected Output:
4
```

```swift
func captcha(for input: String) -> Int {
    var sum = 0
    let digits = Array(input).flatMap { Int(String($0)) }
    let offset = digits.count / 2
    for (index, digit) in digits.enumerated() {
        var lookupIndex = index + offset
        let distancePastEnd = lookupIndex - digits.endIndex - 1
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

## [Day 2](http://adventofcode.com/2017/day/2)

## Challenge 3
> For each row, determine the difference between the largest value and the smallest value; the checksum is the sum of all of these differences.

```
Example Input:
5 1 9 5
7 5 3
2 4 6 8

Excpected Output:
18
```

```swift
func checksum(for input: String) -> Int {
    let intRows = input
        .components(separatedBy: .newlines)
        .map { $0.components(separatedBy: .whitespaces) }
        .map { $0.flatMap { Int($0) } }

    let checksum = intRows
        .map { ($0.max()!, $0.min()!) }
        .map(-)
        .reduce(0, +)

    return checksum
}
```

## Challenge 4
> Find the only two numbers in each row where one evenly divides the other - that is, where the result of the division operation is a whole number. They would like you to find those numbers on each line, divide them, and add up each line's result.

```
Example Input:
5 9 2 8
9 4 7 3
3 8 6 5

Excpected Output:
9
```

```swift
func checksum(for input: String) -> Int {
    let intRows = input
        .components(separatedBy: .newlines)
        .map { $0.components(separatedBy: .whitespaces) }
        .map { $0.flatMap { Int($0) } }

    let checksum = intRows
        .flatMap { row -> (first: Int, second: Int)? in
            for (outerIndex, outerDigit) in row.enumerated() {
                for (innerIndex, innerDigit) in row.enumerated() {
                    guard outerIndex != innerIndex else { continue }
                    if outerDigit % innerDigit == 0 {
                        return (outerDigit, innerDigit)
                    }
                }
            }
            return nil
        }
        .map(/)
        .reduce(0, +)

    return checksum
}
```
