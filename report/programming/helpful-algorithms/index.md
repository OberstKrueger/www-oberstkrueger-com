---
category: programming
created: 2017.07.02:1915
title: Helpful Algorithms
type: page
updated: 2017.10.23:1310
---

## Greatest Common Divisor

	func gcd(_ first: Int, _ second: Int) -> Int {
		var x: Int = first
		var y: Int = second
		while y > 0 {
			(x, y) = (y, x % y)
		}
		return x
	}

## Lowest Common Multiple

	func lcm(_ first: Int, _ second: Int) -> Int {
		if first == 0 && second == 0 { return 0 }
		var x: Int = first
		var y: Int = second
		while y > 0 {
			(x, y) = (y, x % y)
		}
		return (first * second) / x
	}

<div></div>

	func lcm(_ numbers: [Int]) -> Int {
		if numbers.count < 2 { return 0 }
		var baseNumber: Int = numbers.first!
		for index in 1 ..< numbers.endIndex {
			baseNumber = lcm(baseNumber, numbers[index])
		}
		return baseNumber
	}

## Palindrome Check

	import Foundation
	
	extension String {
		var isPalindrome: Bool {
			let s: String = String(self.unicodeScalars.filter({CharacterSet.alphanumerics.contains($0)})).lowercased()
			return s == String(s.reversed())
		}
	}

## Primality Check

Note: This algorithm uses a languages standard square root function. Most languages have efficient implementations of the function that are faster than anything else that could be coded by hand.

	import Foundation
	
	extension Int {
		var isPrime: Bool {
			if self <= 1 { return false }
			if self % 2 == 0 { return self == 2 }
			if self % 3 == 0 { return self == 3 }
			let r: Int = Int(sqrt(Double(self)))
			var f: Int = 5
			while f <= r {
				if self % f == 0 || self % (f + 2) == 0 { return false }
				f += 6
			}
			return true
		}
	}

## Prime Factors

	extension Int {
		var primeFactors: [Int] {
			var f: [Int] = []
			var i: Int = 2
			var m: Int = self
			while i <= m {
				if m % i == 0 {
					f.append(i)
					m /= i
				} else { i += 1 }
			}
			return f
		}
	}

## Prime Numbers Using the Sieve of Eratosthenes

The [sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) returns all prime numbers up to the value n provided to the function. This implementation returns the values as an array.

Note: For large enough values of n, some environments might run out of memory due to the initial large boolean array. If this is the case, running all numbers against the above mentioned primality check is faster than modifying this algorithm to check against known primes.

	import Foundation
	
	func primeSieve(_ target: Int) -> [Int] {
		if target <= 1 { return [] }
		if target == 2 { return [2] }
		if target == 3 { return [2, 3] }
		let targetSquareRoot = Int(sqrt(Double(target)))
		var checks: [Bool] = Array(repeating: true, count: target + 1)
		var primes: [Int] = []
		for number in 2...targetSquareRoot {
			if checks[number] {
				primes.append(number)
				for notPrime in stride(from: number * number, to: target + 1, by: number) { checks[notPrime] = false }
			}
		}
		for number in (targetSquareRoot + 1)...target {
			if checks[number] { primes.append(number) }
		}
		return primes
	}
