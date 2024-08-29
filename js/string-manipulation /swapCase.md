# Swap Case

## Problem Description

The `swapCase` function takes a string as input and returns a new string where each character's case is swapped. Uppercase letters are converted to lowercase, and lowercase letters are converted to uppercase. Non-alphabet characters remain unchanged.

## Implementation

The function uses JavaScript's `split`, `map`, and `join` methods to iterate through each character in the string, swap its case, and then recombine the characters into a new string.

## Function Definition

```javascript
function swapCase(str) {
  return str.split('').map((e) => {
    if (e === e.toUpperCase()) {
      return e.toLowerCase();
    } else {
      return e.toUpperCase();
    }
  }).join('');
}


console.log(swapCase("Hello World"));  // Output: "hELLO wORLD"
console.log(swapCase("JavaScript"));   // Output: "jAVAsCRIPT"
console.log(swapCase("123abcABC"));    // Output: "123ABCabc"
console.log(swapCase(""));             // Output: ""
console.log(swapCase("aBcD"));         // Output: "AbCd"
