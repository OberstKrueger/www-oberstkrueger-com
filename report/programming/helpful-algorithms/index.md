---
category: programming
created: 2017.07.02:1915
title: The Krueger Report - Helpful Algorithms
type: page
updated: 2017.07.02:1915
---

# Helpful Algorithms

The below examples are written in [Python](https://python.org) due to the fact that Python looks like [executable pseudocode](http://archive.is/2013.09.02-020216/http://www.melbpc.org.au/pcupdate/2108/2108article9.htm).

### Greatest Common Divisor

	def gcd(x, y):
		while y:
			x, y = y, x % y
		return x

### Lowest Common Multiple

This algorithm is dependent on the above Greatest Common Divisor function being implement. If it is, use the following version:

	def lcm(x, y):
		if x == y == 0: return 0
		return int((x / gcd(x, y) * y))

If gcd() is not implemented, it can be baked into lcm() as follows:

	def lcm(x, y):
		if x == y == 0:
			return 0
		else:
			a, b = x, y
		while b:
			a, b = b, a % b
		return int((x / a) * y)

### Palindrome Check

A [palindrome](https://en.wikipedia.org/wiki/Palindrome) is any string that reads the same reversed as it does forward. Most languages include a function for reversing a string, and a simple comparison between these two states can determine whether a string is a palindrome or not.

	def palindrome_check(s):
		return s == s[::-1]

### Primality Check

Note: This algorithm uses a languages standard square root function. Most languages have efficient implementations of the function that are faster than anything else that could be coded by hand.

	from math import sqrt
	
	def prime_check(n):
		if n <= 1: return False
		if n % 2 == 0: return n == 2
		if n % 3 == 0: return n == 3
		r = int(sqrt(n))
		f = 5
		while f <= r:
			if n % f == 0 or n % (f+2) == 0: return False
			f += 6
		return True

### Prime Numbers Using the Sieve of Eratosthenes

The [sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) returns all prime numbers up to the value n provided to the function. This implementation returns the values as an array.

Note: For large enough values of n, some environments might run out of memory due to the initial large boolean array. If this is the case, running all numbers against the above mentioned primality check is faster than modifying this algorithm to check against known primes.

	def prime_sieve(n):
		if n <= 1:
			return []
		c = [True] * (n + 1)
		p = []
		for i in range(2, n + 1, 1):
			if c[i] == True:
				p.append(i)
				for x in range(i + i, n + 1, i):
					c[x] = False
		return p
