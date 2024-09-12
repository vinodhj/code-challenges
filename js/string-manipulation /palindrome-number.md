Given an integer x, return true if x is a palindrome, and false otherwise.

## Example 1:

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.

## Example 2:

Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

## Example 3:

Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */

// using string
var isPalindrome = function (x) {
  Negative numbers cannot be palindromes
  if (x < 0) return false;
  return x.toString() === x.toString().split('').reverse().join('');
};

// solve it without converting the integer to a string
var isPalindrome = function (x) {
  // Negative numbers and numbers that end with 0 but are not 0 cannot be palindromes
  if (x < 0 || (x % 10 === 0 && x !== 0)) return false;

  let reversed = 0;
  let original = x;

  while (x > 0) {
    // Get the last digit of the number and add it to the reversed number
    reversed = reversed * 10 + (x % 10);
    x = Math.floor(x / 10); // Remove the last digit from x
  }

  // Compare the reversed number to the original number
  return original === reversed;
};
```
