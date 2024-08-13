# PrimeChecker Function

## Problem Statement

The `PrimeChecker` function takes an integer `num` and checks if any permutation of the digits in `num` results in a prime number. If at least one permutation is prime, the function returns `1`; otherwise, it returns `0`.

### Example

- **Input:** `910`
- **Output:** `1` (because `910` can be rearranged to form `109` or `019`, both of which are prime numbers)

- **Input:** `100`
- **Output:** `0` (no permutation of `100` forms a prime number)

## Solution

Here’s the JavaScript implementation:

```javascript
function PrimeChecker(num) {
  // Helper function to check if a number is prime
  function isPrime(n) {
    if (n <= 1) return false; // 0 and 1 are not prime numbers
    if (n <= 3) return true; // 2 and 3 are prime numbers

    // Eliminate even numbers and multiples of 3
    if (n % 2 === 0 || n % 3 === 0) return false;

    // Check for factors up to the square root of the number
    for (let i = 5; i * i <= n; i += 6) {
      if (n % i === 0 || n % (i + 2) === 0) return false;
    }
    return true;
  }

  // Helper function to generate all permutations of a string
  function generatePermutations(str) {
    if (str.length <= 1) return [str];
    let permutations = [];
    for (let i = 0; i < str.length; i++) {
      let char = str[i];
      let remainingChars = str.slice(0, i) + str.slice(i + 1);
      for (let permutation of generatePermutations(remainingChars)) {
        permutations.push(char + permutation);
      }
    }
    return permutations;
  }

  // Convert the number to a string to generate permutations
  let strNum = num.toString();
  let permutations = generatePermutations(strNum);

  // Check each permutation to see if it forms a prime number
  for (let permutation of permutations) {
    if (isPrime(parseInt(permutation, 10))) {
      return 1;
    }
  }

  return 0;
}

// Test the function with the example input
console.log(PrimeChecker(910)); // Output: 1
console.log(PrimeChecker(100)); // Output: 0
```
