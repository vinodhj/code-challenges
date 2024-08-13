# Palindrome

## Description

The `isPalindrome` function checks if a given string is a palindrome. A palindrome is a word, phrase, number, or other sequence of characters that reads the same forward and backward, ignoring spaces, punctuation, and case sensitivity.

### Input

- A string `str` consisting of any characters.

### Output

- Return `true` if the input string is a palindrome, otherwise return `false`.

## Function Definition

```javascript
function isPalindrome(str) {
  // Convert the string to lowercase and remove non-alphanumeric characters
  const cleanStr = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  
  // Check if the cleaned string is equal to its reverse
  return cleanStr === cleanStr.split('').reverse().join('');
}

// Test cases
console.log(isPalindrome("A man, a plan, a canal, Panama")); // Output: true
console.log(isPalindrome("racecar")); // Output: true
console.log(isPalindrome("hello")); // Output: false
console.log(isPalindrome("No 'x' in Nixon")); // Output: true
console.log(isPalindrome("12321")); // Output: true
```
