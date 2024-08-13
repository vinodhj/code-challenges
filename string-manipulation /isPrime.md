# Prime Number Checker in JavaScript

This document provides a JavaScript function to check if a number is prime. The function uses an efficient method to determine the primality of a given number.

## Prime Number Definition

A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself.

## JavaScript Function

The following JavaScript function checks if a number is prime:

```javascript
function isPrime(num) {
    if (num <= 1) return false; // Numbers less than or equal to 1 are not prime
    if (num <= 3) return true;  // 2 and 3 are prime numbers

    // Eliminate even numbers and multiples of 3
    if (num % 2 === 0 || num % 3 === 0) return false;

    // Check for factors up to the square root of the number
    for (let i = 5; i * i <= num; i += 6) {
        if (num % i === 0 || num % (i + 2) === 0) return false;
    }

    return true;
}

// Test the function with the example input
console.log(isPrime(41)); // Output: true
console.log(isPrime(100)); // Output: false
```
