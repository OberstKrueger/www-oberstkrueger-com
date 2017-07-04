---
category: programming
created: 2017.07.02:1915
title: The Krueger Report - Helpful Algorithms
type: page
updated: 2017.07.03:2130
---

# Helpful Algorithms

## Greatest Common Divisor

### Python

	def gcd(x, y):
		while y:
			x, y = y, x % y
		return x

### Swift

	func gcd(_ first: Int, _ second: Int) -> Int {
		var x = first, y = second
		while y > 0 { (x, y) = (y, x % y) }
		return x
	}

## Lowest Common Multiple

### Python

	def lcm(x, y):
		if x == y == 0: return 0
		a, b = x, y
		while b:
			a, b = b, a % b
		return int((x / a) * y)

### Swift

	func lcm(_ first: Int, _ second: Int) -> Int {
		if first == 0 && second == 0 { return 0 }
		var x = first, y = second
		while y > 0 { (x, y) = (y, x % y) }
		return (first / x) * second
	}

## Palindrome Check

### Python

	def palindrome_check(s):
		return s == s[::-1]

### Swift

	extension String {
		var isPalindrome: Bool {
			return self == String(self.characters.reversed())
		}
	}

## Primality Check

Note: This algorithm uses a languages standard square root function. Most languages have efficient implementations of the function that are faster than anything else that could be coded by hand.

### Python

	from math import sqrt
	
	def prime_check(n):
		if n <= 1: return False
		if n % 2 == 0: return n == 2
		if n % 3 == 0: return n == 3
		r, f = int(sqrt(n)), 5
		while f <= r:
			if n % f == 0 or n % (f+2) == 0: return False
			f += 6
		return True

### Swift

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

## Prime Numbers Using the Sieve of Eratosthenes

The [sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) returns all prime numbers up to the value n provided to the function. This implementation returns the values as an array.

Note: For large enough values of n, some environments might run out of memory due to the initial large boolean array. If this is the case, running all numbers against the above mentioned primality check is faster than modifying this algorithm to check against known primes.

### Python

	from math import sqrt
	
	def prime_sieve(n):
		if n <= 1: return []
		c = [True] * (n + 1)
		p = []
		for i in range(2, int(sqrt(n)), 1):
			if c[i]:
				p.append(i)
				for x in range(i * i, n + 1, i): c[x] = False
		for i in range(int(sqrt(n)) + 1, n + 1, 1):
			if c[i]: p.append(i)
		return p
		
	print(prime_sieve(101))

### Swift

	import Foundation
	
	func primeSieve(_ target: Int) -> [Int] {
		if target <= 1 { return [] }
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